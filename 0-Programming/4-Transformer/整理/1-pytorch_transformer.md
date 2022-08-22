# Pytorch版的 transformer


key_padding_mask: is used to block attending to PAD tokens
attn_mask: is used to block speicfic positions from attention

- True: 意味着 对应位置上的值将会被忽略




## TransformerEncoderLayer
1. 子模块

- self.self_attn = MultiheadAttention
- Feedforward model

2. 重要参数
- norm_first：控制 LN 的位置 是 Post-LN(默认, 原文) 还是 Pre-LN(效果更好)


3. 输入与输出
- 输入:
  - x          : input sequence
  - src_mask
  - src_key_padding_mask


4. 逻辑运算

- self._sa_block: 调用 MultiheadAttention 模块
- self._ff_block


## MultiheadAttention

1. 输入:
  - q=k=v=x (如果使用 TransformerEncoderLayer 那 q=k=v. 可以单独只使用 MultiheadAttention)

2. 核心运算代码

**Step 1**  公式 $Q W_{i}^{Q}$

```python
q, k, v = _in_projection_packed(query, key, value, in_proj_weight, in_proj_bias)
```
> 返回值为 linear(q, w, b).chunk(3, dim=-1) -> self-attention

- w 的 shape 为 [3E， E]， q = [S, B, E]
- 函数 linear 的运算为 y = xA^T + b.  因此 y 为 [S, B, 3E]
- chunck 后的结果为 q, k, v 大写都是 [S, B, E]

**Step 2** 准备多头
1. q 由 [S, B, E] 变为 $[S, B*num_heads, head_dim]$ 再修改为 $[B*num_heads, S, head_dim]$

*若* add_zero_attn:

- k 由 $[B*num_heads, S, head_dim]$, 变成 $[B*num_heads, S+1, head_dim]$
> 在 S 的末尾补 0

- attn_mask = [L, S]  做 pad 得到 [L, S+1]; key_padding_mask [B, S] 变成 [B, S+1]

2. 更新 src_len = k.size(1)

3. key_padding_mask [B, S]
   - 由 view 变为 [B, 1, 1, S], 
   - 由 expand 操作变成 [B, num_heads, 1, S] 
   - 由 reshape 变成 [B * num_heads, 1, src_len]

    expand 的作用: 考虑 多头的问题, 因为多头是将 hid_dim 切分, seq_len 没变, 因此要针每个头复制一个 mask

4. attn_mask = attn_mask.masked_fill(key_padding_mask, float("-inf")) 函数理解
   
   attn_mask 是 [L, S], key_padding_mask 是 [B * num_heads, 1, S]

    - attn_mask 先复制成 [B * num_heads, L, S]

    假设 key_padding_mask = tensor([[1, 1, 0, 0],
                                    [1, 0, 0, 0],
                                    [0, 1, 0, 0]])
    
那么 attn_mask 的 第一个块 到 第 head 块 的第一列 全为 -inf


**Step 3** _scaled_dot_product_attention 运算

attn_output, attn_output_weights = _scaled_dot_product_attention(q, k, v, attn_mask, dropout_p)
> 输入 q = [bsz * num_heads, tgt_len, head_dim]
> 输出 attn_output = [B', L, E]

```python
q = q / math.sqrt(E)
if attn_mask is not None:
    attn = torch.baddbmm(attn_mask, q, k.transpose(-2, -1))
else:
    attn = torch.bmm(q, k.transpose(-2, -1))

attn = softmax(attn, dim=-1)

if dropout_p > 0.0:
    attn = dropout(attn, p=dropout_p)

output = torch.bmm(attn, v) # [B', L, S] * [B', S, E] -> [B', L, E]
return output, attn
```
attn_mask = [B', L, S]
q = [B', L, E]
k = [B', S, E]

torch.baddbmm:
1. q 和 k.transpose(-2, -1) 进行矩阵乘 得到 [B', L, S]
2. 然后 结果再和attn_mask 进行元素对应相乘 -> [B', L, S]

> 针对 Encoder attn_mask 为 0 或者不为 0 没有影响

**Step 4** 后处理. 将多个头进行 cat 
1. attn_output = attn_output.transpose(0, 1).contiguous().view(tgt_len * bsz, embed_dim)

attn_output [B', L, E]:
- 由 transpose 变成 [L, bsz * num_heads, head]
- 由 view 变成 [tgt_len * bsz, embed_dim]  embed_dim= num_heads * head

2. attn_output = linear(attn_output, out_proj_weight, out_proj_bias)
> 送入一个全连接层 -> 对应的是 Concat(head..)W   这个里面的 W

3. attn_output = attn_output.view(tgt_len, bsz, attn_output.size(1)) -> [L, B, embed_dim]

# Mask 难点理解

```python
    # merge key padding and attention masks
    if key_padding_mask is not None:
        assert key_padding_mask.shape == (bsz, src_len), \
            f"expecting key_padding_mask shape of {(bsz, src_len)}, but got {key_padding_mask.shape}"
        key_padding_mask = key_padding_mask.view(bsz, 1, 1, src_len).   \
            expand(-1, num_heads, -1, -1).reshape(bsz * num_heads, 1, src_len) # 对应 head 复制 mask
        if attn_mask is None:
            attn_mask = key_padding_mask
        elif attn_mask.dtype == torch.bool:
            attn_mask = attn_mask.logical_or(key_padding_mask)
        else:
            attn_mask = attn_mask.masked_fill(key_padding_mask, float("-inf"))

    # convert mask to float
    if attn_mask is not None and attn_mask.dtype == torch.bool:
        new_attn_mask = torch.zeros_like(attn_mask, dtype=q.dtype)
        new_attn_mask.masked_fill_(attn_mask, float("-inf"))
        attn_mask = new_attn_mask
```


## 情况 1: key_padding_mask 有值, attn_mask = None
key_padding_mask 为 [B, S]

**Step 1**: 为 num_head 做准备 -> [B*num_head, 1, src_len]
```python
key_padding_mask = key_padding_mask.view(bsz, 1, 1, src_len).   \
    expand(-1, num_heads, -1, -1).reshape(bsz * num_heads, 1, src_len)
```

> 因为有 num_head, 它是将 hid_dim 进行了切分, 因此，对应位置要复制 key_padding_mask

**Step 2**: 将 key_padding_mask 融入到 attn_mask
由于 atten_mask = None, 因此 attn_mask = key_padding_mask

convert mask to float 是把 attn_mask的值转化为 float

## 情况 2: key_padding_mask 有值, attn_mask 有值

执行下面的代码
attn_mask = attn_mask.masked_fill(key_padding_mask, float("-inf"))
# MultiheadAttention

## 理论知识
该模块的作用是：

第一步：
对于 Q, K, V 先进行分解，Q = [q1, q2, ...], K = [k1, k2, ...], V = [v1, v2, ...]

第二步：
对 [qi, ki, vi] 进行 attention (scaled Dot-Product Attention)
> 当 K=Q=V 时，就可以理解为 self-attention


第三步：
对 i 份值进行 concat 输出最终结果

## 源码

### 参数
embed_dim: 
> 它将会被分割成 num_heads 份, 那么没份儿的大小为 embed_dim / num_heads

num_heads: 多少个平行计算的头


### 输入
- L =  target sequence length; 
- N = batch size; 
- E_q = query_embedding = embed_dim
- S = source sequence length

**query**: 
(L, N, E_q) -> batch_first=False

(N, L, E_q) -> batch_first=True

**key_padding_mask**:
(N, S)
非零元素值 意味着 对应位置的 key 值为 0 

**need_weights**
True -> 返回 attn_outputs, attn_output_weights

**attn_mask**
(N * n_heads L,S)

1 -> 对应位置的值 将不被 attend

**average_attn_weights**
True: attn_weights 的值将会被 heads 进行平均

### 输出

**attn_output**
(L, N, E_q) -> batch_first=False

(N, L, E_q) -> batch_first=True

**attn_output_weights**
(N, L, S)
need_weights=True 时才返回该值

average_weights=True
>attention weights averaged across heads of shape :math:`(L, S)`

average_weights=False
>returns attention weights per head of shape :math:`(\text{num\_heads}, L, S)`



## 源码解析

```python
is_batched = query.dim() == 3 # 是否是 Batchde 数据
if self.batch_first and is_batched: # [B, ,]
    # make sure that the transpose op does not affect the "is" property
    if key is value:
        if query is key: # q = k = v
            query = key = value = query.transpose(1, 0)
        else:
            query, key = [x.transpose(1, 0) for x in (query, key)] # q, k=v
            value = key
    else:
        query, key, value = [x.transpose(1, 0) for x in (query, key, value)] # q, k, v

if not self._qkv_same_embed_dim: # q, k, v 不相等时
    attn_output, attn_output_weights = F.multi_head_attention_forward(
        query, key, value, self.embed_dim, self.num_heads,
        self.in_proj_weight, self.in_proj_bias,
        self.bias_k, self.bias_v, self.add_zero_attn,
        self.dropout, self.out_proj.weight, self.out_proj.bias,
        training=self.training,
        key_padding_mask=key_padding_mask, need_weights=need_weights,
        attn_mask=attn_mask, use_separate_proj_weight=True,
        q_proj_weight=self.q_proj_weight, k_proj_weight=self.k_proj_weight,
        v_proj_weight=self.v_proj_weight, average_attn_weights=average_attn_weights)
else:   # q=k=v 时
    attn_output, attn_output_weights = F.multi_head_attention_forward(
        query, key, value, self.embed_dim, self.num_heads,
        self.in_proj_weight, self.in_proj_bias,
        self.bias_k, self.bias_v, self.add_zero_attn,
        self.dropout, self.out_proj.weight, self.out_proj.bias,
        training=self.training,
        key_padding_mask=key_padding_mask, need_weights=need_weights,
        attn_mask=attn_mask, average_attn_weights=average_attn_weights)
if self.batch_first and is_batched:
return attn_output.transpose(1, 0), attn_output_weights
else:
return attn_output, attn_output_weights
```


# key_padding_mask 和 attn_mask 的区别

## key_padding_mask
[N, S] 对于 输入的 input, 它的padding指被忽略.  这个 key_padding_mask 用于忽略 sentence 中的padding

`源码` 

```python
if key_padding_mask is not None:
    assert key_padding_mask.size(0) == bsz
    assert key_padding_mask.size(1) == src_len

attn_output_weights = torch.bmm(q, k.transpose(1, 2))
attn_output_weights = attn_output_weights.view(bsz, self.num_heads, tgt_len, src_len)
attn_output_weights = attn_output_weights.masked_fill(
                key_padding_mask.unsqueeze(1).unsqueeze(2),
                float('-inf'),
            )
"""
attn_output_weights 是 Q 和 K 的乘积, shape =[B, num_head, tgt_len, src_len]
key_padding_mask.unsqueeze(1).unsqueeze(2) 的 shape = [B, 1, 1, S]

masked_fill 对 key_padding_mask 位置为0的填充0
"""
```
## attn_mask 
> 阻止对 某些位置的元素  attention

[L, S]

**源码**

```python
if attn_mask.dim() == 2:
    attn_mask = attn_mask.unsqueeze(0) # [1, L, S]
    attn_output_weights.masked_fill_(attn_mask, float('-inf'))  # 也是进行填充, 0的位置填充为 -inf
```

因此, 构造 attn_mask 即可 忽略某些位置的值
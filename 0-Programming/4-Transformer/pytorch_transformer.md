# src_mask & src_key_padding_mask 

## src_key_padding_mask 
用于解决 batch_data 中的 PDA   [Batch_size, Seq_len]

## src_mask
做 Decoder 的时候,  当前的 token 只能看见前面所有的 token
[a, b, c, 'pad']

a 看见 a
b 看见 a, b
c 看见 a, b, c

[L, S]


### 控制参数

1. self._qkv_same_embed_dim
self._qkv_same_embed_dim = self.kdim == embed_dim and self.vdim == embed_dim  -> True

    self.kdim = kdim if kdim is not None else embed_dim
    self.vdim = vdim if vdim is not None else embed_dim
    > 关乎 MultiheadAttention 的初始化生成

    在 TransformerEncoderLayer 中 
       self.self_attn = MultiheadAttention(d_model, nhead, dropout=dropout)
       kdim, vdim 是 None



# 计算步骤

## 1. 主要参数
q = [L, N, E]  L: target sequence length
k = [S, N, E]  S: source sequence length
v = [S, N, E]

key_padding_mask = [N, S]

attn_mask = [L, S] or = [N*num_heads, L, S]
>attn_mask ensures that position i is allowed to attend the unmasked positions


## 2. 核心步骤
q, k, v = _in_projection_packed(query, key, value, in_proj_weight, in_proj_bias)
> 这类的q, k, v 对应的是 Q, K, V

Q = q*W

### 2.1
self.in_proj_weight = Parameter(torch.empty(3 * embed_dim, embed_dim))
self.register_parameter('q_proj_weight', None)
self.register_parameter('k_proj_weight', None)
self.register_parameter('v_proj_weight', None)

if bias:
    self.in_proj_bias = Parameter(torch.empty(3 * embed_dim))
else:
    self.register_parameter('in_proj_bias', None)


### 2.2 _in_projection_packed 运行逻辑
- 若 k=v=q: self-attention, 返回 linear(q, w, b) -> y=kq+b 随后的 chunk(3, dim=-1) 将 y 分成三份
- 若 k=v 且 q != k  w_q, w_kv = w.split([E, E * 2]), w_q = [E, E], w_kv=[E, E*2]
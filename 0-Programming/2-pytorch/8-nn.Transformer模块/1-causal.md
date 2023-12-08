# TransformerEncoder
输入:
- src
- mask:                  the mask for the src sequence (optional).  preventing attention to certain positions.
- src_key_padding_mask:  the mask for the src keys per batch (optional).
- is_causal

mask: [L, S] 在 Encoder 中就是 [S, S]

`True` 相应位置的值是 不被 attend

src_key_padding_mask: [N, S]
>which elements within key to ignore for the purpose of attention

`True` 相应的值会被 ignore

## mask 和 src_key_padding_mask 的区别

mask 表征 输入序列的哪部分 被 Model 运行 attention (它可以用来制作 causal mask)

src_key_padding_mask: 解决 Padding 用的


## mask
>  

## src_key_padding_mask 

# is_causal 

> 用来检测 mask 是否是  causal mask. 默认值是 False

1. 当 is_causal: None,  mask 存在时

返回 True, 检测到当前使用的是  causal mask


2. 当 is_causal: False, 不论 mask

返回 False

3. 当 is_causal: True, mask 存在时
   
返回 True

_detect_is_causal_mask:
- mask
- is_causal
- size:  seq_len

综上所述, 我同时需要给模型输入 mask 和 src_key_padding_mask 才能满足我的需求

is_causal 

`_canonical_mask` 
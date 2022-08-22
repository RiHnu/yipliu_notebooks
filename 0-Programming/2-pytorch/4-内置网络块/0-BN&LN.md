# 使用 Norm 的原因

归一化数据，减小训练时间

## BatchNorm
输入  (N, C, L)
N 是 batch size
C 是 the number of features
L 是 the sequence length

沿着 C 计算每个 batch 的均值和方差

## LayerNorm

```python
nn.LayerNorm(
            normalized_shape, 
            eps=1e-05,
            elementwise_affine=True,
            device=None,
            dtype=None
            )
```
- 对 normalized_shape 求均值和放差
- normalized_shape 可以是 int, list, torch.Size
- 如果是 int 的话，int 必须是 Data 的最后一个维度
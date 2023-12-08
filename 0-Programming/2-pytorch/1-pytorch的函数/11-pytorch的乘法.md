torch.bmm

batch 的 矩阵与矩阵的  矩阵乘法


torch.mul  对应位置上的 元素相乘


contiguous()

对于 tensor, 若此前执行过 permute or transpose ，想执行 view, 我们需要先执行 contiguous()

# torch.matmul
 矩阵乘

- 若都是 1-D 返回 scalar

- 若都是 2-D 那么进行 矩阵乘

```python
tensorA @ tensorB
```


[einsum](https://zhuanlan.zhihu.com/p/361209187)

c = torch.einsum("ik,kj->ij", [a, b])

`@` 是矩阵乘法.  [5, 3] @ [3, 10] = [5, 10]
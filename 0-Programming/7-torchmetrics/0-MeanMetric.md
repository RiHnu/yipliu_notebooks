# 通用

- `reset()` 方法在每个 epoch 后都会自动调用

- `self.log` 只支持 scalar-tensors

- 可以直接 log `object` 也能 log `metrics.compute()`

如果 on_epoch=True 将自动 log the end of epoch metric value by calling .compute()
[官网](https://torchmetrics.readthedocs.io/en/stable/pages/lightning.html)


Benefits:
1. data will always be placed on the same device as your metrics
2. 支持 self.log
3. **reset()** 方法将会在 the end of an epoch 自动被调用


# self.log

self.log 仅仅支持 scalar-tensors  因此，我们需要注意计算发返回值

reset method 将会自动 at the end of an epoch 被调用


# DP
如果在 Data parallel mode 这使用 metrics, the metric update/logging 需要在 <mode>_step_end 这使用


# MaxMetric
> 记录 val_best_acc
利用 update 方法加入当前值
利用 compute 求出至今为止的最大值
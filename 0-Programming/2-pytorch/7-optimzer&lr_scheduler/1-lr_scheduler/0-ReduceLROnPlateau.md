# ReduceLROnPlateau
>当 metric 停止时，减少 rl

该 lr_scheduler 通过监控一个 metric 当其值在 patience of epoch 没有变化时，减小 lr

## 参数

**optimizer**

**mode**:
- min:  当 metric 停止减小时，减小 lr
- max:  当 metric 停止增大时，减小 lr

**factor**: 0.1
new_lr = lr*factor  

**patience**:
可容忍的 epoch 值

**threshold**
衡量最优值的阈值

**min_lr**
lr 的最小值

**verbose** False
> True 对于每次更新，输出 message
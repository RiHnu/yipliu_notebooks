[官网博客](https://pytorch-lightning.readthedocs.io/en/latest/common/lightning_module.html#configure-optimizers)


返回值有 6 种：
- Single optimizer: 没有 lr scheduler
>return Adam(self.parameters(), lr=1e-3)

- 多个 optimizer: 针对 GANs

- optimizer + lr scheduler



# lr_scheduler_config

**scheduler**: ReduceLROnPlateau(optimizer, ...)
> 具体的 lr_scheduler 实例

**interval**: "epoch"
> 是以 epoch 更新 还是以 step 更新

**frequency**: 1
> 更新频率 1 是 updating the learning rate after every epoch

**monitor**: "val_loss"

**strict**: True
> 当监控的值 monitor 没有时，停止训练
> False: 若没有 monitor 时，仅仅发出 warning

**name**: None
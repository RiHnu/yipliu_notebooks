`use_distributed_sampler`
> 是否使用 torch.utils.data.DistributedSampler 重写 DataLoader 的 sampler

如果没有指定该参数，它将根据 strategies 自动调整.

默认情况下:
- shuffle=True -> train
- shuffle=False -> validation/test/predict

当重写时候, 设置`use_distributed_sampler=False`



`For iterable-style datasets, we don’t do this automatically`

注意使用 `__iter__` 的 dataset
在 Pytorch 中 Dataset 支持两种类型
- Map-style datasets
- iterable-style datasets

## Map-style datasets

我们一般重写下面两个函数

- __len__()

- __getitem__(self, key)

调用的话，一般是 key: value 形式. data[key]


## Iterable-style datasets



# Dataloader

drop_last:
    当 len(dataset) 除于 batch_size 不等于整数时，最后一个 batch_size 的数据小于 batch_size 的值
- True: 舍掉 the last incomplete batch
- False: 最后一个 batch 是 smaller 的


[官网](https://pytorch.org/docs/stable/data.html?highlight=dataloader#torch.utils.data.DataLoader)


## shuffle
如果设置为 True: 数据将在每个 epoch 被重新打乱
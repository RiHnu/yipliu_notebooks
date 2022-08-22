[Blog](https://stanford.edu/~shervine/blog/pytorch-how-to-generate-data-parallel)


## __init__

初始化函数，一般给出 data_dir

## __len__
返回 the number of samples in our dataset

## __getitem__

对于给定 idx 的 sample, 该函数需要

1. 加载相应的 sample
2. 对这个 sample 进行处理，得到 tensor
3. 以 (x, y) 的形式返回


[官网网站](https://pytorch-lightning.readthedocs.io/en/stable/extensions/datamodules.html?highlight=lightningDataModule)

Datamodule 包含以下五步
1. Download / tokenize / process
2. 清洗并保存数据于 Disk
3. Load inside Dataset
4. Apply transforms (rotate, tokenize, etc...)
5. Wrap inside a DataLoader



# 1. 为什么需要 DataModule?
一般代码中，数据处理代码分布混乱， pl 将其整理在一起

# 2. 一般步骤
1. prepare_data
    (how to download(), tokenize, etc...)
https://github.com/PyTorchLightning/pytorch-lightning/issues/3175
2. setup 
    (how to split, etc)
    * count number of classes
    * build vocabulary
    * perform train/val/test splits
    * apply transforms
    * etc...


3. train_dataloader

4. val_dataloader

5. test_dataloader


## 1. prepare_data
> 主要写 下载 载数据集
> 该函数仅仅在 a single process(GPU 0) 中被调用

## 2. setup
> 该函数能在 every GPU 上被调用(即在 every process 上都被调用)
> teardown 函数用于 clean up state


```python
def class DataModule(pl.LightningDataModule):
    def setup(self, stage: Optinal[str] = None):
        
        # 这里设置 train/val 的数据集
        if stage in (None, "fit"):
        
        # 这里设置 test 的数据集
        if stage in (None, "test"):
```


## 3. train_dataloader
用这个函数生成 the train dataloader
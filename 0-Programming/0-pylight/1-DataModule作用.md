# DataModule
> src/datamodules
[官网网站](https://pytorch-lightning.readthedocs.io/en/stable/extensions/datamodules.html?highlight=lightningDataModule)

Datamodule 包含以下五步
1. Download / tokenize / process
2. 清洗并保存数据于 Disk
3. Load inside Dataset
4. Apply transforms (rotate, tokenize, etc...)
5. Wrap inside a DataLoader


## __init__
数据集路径
batch_size
vocab_size


## prepare_data
1. 下载数据集
    (how to download(), tokenize, etc...)
https://github.com/PyTorchLightning/pytorch-lightning/issues/3175

这里面的代码只在 Single GPU 上运行

## setup
(how to split, etc)
* count number of classes
* build vocabulary
* perform train/val/test splits
* apply transforms
* etc...


1. 数据集划分：得到 train_data, val_data, test_data


2. 创建字典
分别得到 input, target 的 vocabulary 

相应的 pad_idx, vocab_size 均可得到

3. 将 train_data 送入到类 Dataset  里面 得到 self.train
> torch.utils.data.Dataset



# DataLoader




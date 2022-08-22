[Blog_1](https://github.com/PyTorchLightning/pytorch-lightning/issues/10349)

pytorch lightning 默认 tensor 的 dim=0 处为 Batch_Size

产生这个 Warning 的原因是 自己设计 __getitem__ 函数结构
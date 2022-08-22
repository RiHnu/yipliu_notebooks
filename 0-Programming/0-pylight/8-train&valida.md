[官网解释](https://pytorch-lightning.readthedocs.io/en/latest/common/lightning_module.html)

# training_step_end
如果我们使用了 strategy (DP, or DDP2) 训练模型, 那么我们就需要用这个函数

```python
def training_step_end(self, batch_parts):
    # predictions from each GPU
    predictions = batch_parts["pred"]
    # losses from each GPU
    losses = batch_parts["loss"]

    gpu_0_prediction = predictions[0]
    gpu_1_prediction = predictions[1]

    # do something with both outputs
    return (losses[0] + losses[1]) / 2
```

# validation_epoch_end

每次 **validation_step** 的输出 都会去 validation_epoch_end 

如果我们需要对这些输出进行操作，我们需要调用这个函数
> validation_epoch_end 的调用先于 training_epoch_end


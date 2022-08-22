里面能设置是否在 GPU 上运行代码
gpus: 
- 当为 值为 int 时候，意味着 用多少个 GPU 进行训练

- 当 为 list or str 指的是用哪个GPU 进行训练

# Trainer
[官方文档](https://pytorch-lightning.readthedocs.io/en/latest/common/trainer.html)

- 自动进行 enabling/disabling grads
- 运行 training, validation and test dataloaders
- 在适当时候自动运行 Callbacks
- 自动将 batches 和 计算 放在正确的 devices 上

## 伪代码 -> train
trainer 基本能自动实现如下功能

```python
# 1. 将 model 设置 train mode
model.train()
torch.set_grad_enable(True)

losses = []

# 输入数据，计算 loss
for batch in train_dataloader:
    
    on_train_batch_start()

    loss = training_step(batch)

    # 清零梯度值
    optimizer.zero_grad()

    # 反向传播
    loss.backward()

    # 更新参数
    optimizer.step()

    losses.append(loss)
```


# Validation sanity check
当 执行完 def configure_optimizer 后会自动执行 [validation sanity check](https://pytorch-lightning.readthedocs.io/en/latest/common/trainer.html?highlight=num_sanity_val_steps#num-sanity-val-steps)

代码会自动跑一下,默认跑 2 steps 在 Trainer 里面可以进行设置

num_sanity_val_steps:

2  -> 默认值
0  -> 关闭该功能
-1 -> check all validation data


## 参数

## auto_lr_find
True: 允许使用 trainer.tune() 找到一个 lr

### default_root_dir
当 logger/ckpt_callback 没有提供路径时候时，logs and weights 的默认路径 os.getcwd()

### resume_from_checkpoint: 
Path of the checkpoint from which training is resumed

V.17后 使用方式 直接在这个里[面写](https://pytorch-lightning.readthedocs.io/en/latest/api/pytorch_lightning.trainer.trainer.html?highlight=trainer#pytorch_lightning.trainer.trainer.Trainer)
Trainer.fit(..., ckpt_path=..)

### gradient_clip_val
0.0 意味着不进行 clip


### callbacks
add a callback or list of callbacks
[官方文档](https://pytorch-lightning.readthedocs.io/en/stable/extensions/logging.html)

```python
def training_step(self, batch, batch_idx):
    self.log("my_loss", loss, on_step=True, on_epoch=True, prog_bar=True, logger=True)
```

**on_step**: 记录当前 step 的值 (默认为 True)

**on_epoch**: 在每个 epoch 结束的时候自动累计和记录

**prog_bar**: Logs to the progress bar

**logger**: Logs to the logger

**reduc_fx**: 


## NOTE

当 on_epoch 为 True 时



# MLFLOW

[教程](https://bytepawn.com/automatic-mlflow-logging-for-pytorch.html)
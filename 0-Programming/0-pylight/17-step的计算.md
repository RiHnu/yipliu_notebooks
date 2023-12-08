`estimated_stepping_batches`
> 完

- total_batches = self.num_training_batches: 训练多少个 batch
- dataset_len / batch_size  -> 一个 epoch 有多少 step

```python
def estimated_stepping_batches(self):
    """"""
    # 如果 max_epochs 为 -1  返回 max_step 值
    if self.max_epochs == -1:
        return float("inf") if self.max_steps == -1 else self.max_steps    
    
    total_batches = self.num_training_batches # total training batches: 一个 epoch 有多少 step

    return total_batches* self.max_epochs
```





`global_step`: The number of optimizer steps taken (does not reset each epoch)
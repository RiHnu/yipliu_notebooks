[参考博客](https://wandb.ai/wandb_fc/tips/reports/How-to-Implement-Gradient-Accumulation-in-PyTorch--VmlldzoyMjMwOTk5)

伪代码:
1. 计算得到 loss
2. normalize the gradients: loss = loss / NUM_ACCUMULATION   -> normalize the gradients
3. loss.backward() -> 反向传播
4. if (idx+1) % num_accumulation_steps ==0  optimizer.step() -> 累计到次数才进行 step
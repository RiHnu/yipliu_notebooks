# 关联参数解释

**global_step**:
> 该参数是等于 optimizer.step 的次数, 并不是 loss.backward 的次数

对于 accumulate gradients 而言, 假设 batch_size = N, accumulate_grad_batches = K, 即我们需要累计 K 个 batch_size 产生的 Loss, 每个 batch_size 产生的梯度是由 loss.backward() 产生


[github issue](https://github.com/Lightning-AI/lightning/issues/5405)
根据这个 issue 讨论的, WB 里面的 step 为 optimization step
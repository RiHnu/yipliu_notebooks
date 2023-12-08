# DDP Distributed Data Parallel
> 官网建议使用 DDP

# DDP_Spawn Distributed Data Parallel Spawn
> 官网不建议使用 DDP_SPAWN



batch_size=n  accumulate_grad_batches=k, gpus=p

每个 GPU 单独 accumulates -> 那么每个 GPU 最终就是 n*k

对于 p 个 GPU, 最终结果就是 `p*n*k`


```markdown2
GPU1 processes one batch of size 16.
GPU1 processes another batch of size 16
GPU1 averages the gradients of the two batches.

GPU2 processes one batch of size 16.
GPU2 processes another batch of size 16
GPU2 averages the gradients of the two batches.

average the averaged gradients from GPU1 and GPU2 and apply weight update
```

[issue](https://github.com/Lightning-AI/lightning/discussions/5796)



# ISSUE

当 model 里面包含不用结构, 例如

```python
if a:
    decoder = B1
else:
    decoder = B2
```

这种情况下，只能使用 `find_unused_parameters=True`

[issues](https://github.com/Lightning-AI/lightning/issues/17212)


当使用 batch_size=B 在 N 个 GPU 上时候，那么 有效的 batch_size= B*N

[issue](https://lightning.ai/forums/t/effective-learning-rate-and-batch-size-with-lightning-in-ddp/101/15)


每个 GPU 看见 1/N dataset [issue](https://github.com/Lightning-AI/lightning/discussions/16548)

当使用自定义 sampler 时
`use_distributed_sampler: False` 
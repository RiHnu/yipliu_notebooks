# deepspeed_stage_1
> doc 建议直接用 stage_2

https://lightning.ai/docs/pytorch/stable/advanced/model_parallel/deepspeed.html

通过将 `optimizer states` 切分到 GPUs 从而减少单个GPU的内存


# deepspeed_stage_2

将 `optimizer states` 和 `gradients` 切分到 GPUs 以减少内存

# deepspeed_stage_2_offload

额外的利用了 CPU 减少内存

`allgather_bucket_size`

`reduce_bucket_size`
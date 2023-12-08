
## FSDP
Fully Shared Data Parallel (FSDP)

默认情况下, FSDP 会共享
- Model Weights
- 反向传播时候的 梯度
- GPUs 所有的 Optimizer states  通过 auto-wrap-policy

建议按照 `epoch` 保存 checkpoint


## FSDPStrategy

`activation_checkpointing_policy`

`cpu_offload`: 计算极其慢


`state_dict_type`
- full: 默认值
- sharded: 加速保存 (2.1版本不建议使用)

`limit_all_gathers`
>模型训练时, 防止将 GPU 处于接近耗尽状态

- False: 默认值. 
- True: 当 GPU 接近最大值时, 启用

### sharding_strategy

`FULL_SHARD`: Shard weights, gradients, optimizer state

`SHARD_GRAD_OP`: Shard gradients, optimizer state

`HYBRID_SHARD`:  Full-shard within a machine, replicate across machines

`NO_SHARD`: Don't shard anything (similar to DDP)

- 首先应该尝试 `FULL_SHARD`: 它最慢, 但是会 节约 最多的 memory

- 再尝试 `SHARD_GRAD_OP`, 能提升计算速度

- 如果在多台 `machines`, 使用 `HYBRID_SHARD`




### Activation checkpointing
> 能大量减少内存使用

针对 transformer layer 使用






## DeepSpeed
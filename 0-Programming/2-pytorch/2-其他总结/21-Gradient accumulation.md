# Gradient accumulation
[blog](https://towardsdatascience.com/how-to-break-gpu-memory-boundaries-even-with-large-batch-sizes-7a9c27a400ce)

GPU的大小限制了 Batch size 的增加。解决这个问题常用两种方法：
- Data-parallelism(多个GPU)
1. 把一个 Batch size 上的数据分成多组 Mini-Batch
2. 把上诉数据放在多个 GPU 平行计算
3. 汇集所有的 loss，以更新 Model 的参数

- Gradient accumulation(仅需一个 GPU)
1. 依次计算 mini-batch
2. 汇总上诉 Loss 以更新模型参数
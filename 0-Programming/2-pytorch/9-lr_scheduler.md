# StepLR

每 step_size 以 gamma 大小 衰减学习率

## 参数
- optimizer: 优化器
- step_size: 学习率调整步长
- gamma: (default=0.1)  衰减率
- last_epoch: -1
- verbose: (default=False) 是否在终端输出信息

scheduler = StepLR(optimizer, step_size=30, gamma=0.1)

每 30 个 step 以0.1倍 减少 learning_rate
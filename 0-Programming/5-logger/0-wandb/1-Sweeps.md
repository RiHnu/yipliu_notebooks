# Sweeps: 找到最佳超参

- 第一步：定义 sweep
- 第二步：初始化 sweep
- 第三步：运行

## 第一步：定义 Sweep

1. 选择参数搜素策略
- grid
- random (选这个就行)
- bayes

2. 定义需要优化的 **参数**

如下：
```python
parameters_dict = {
    'optimizer': {
        'values': ['adam', 'sgd']
        },
    'fc_layer_size': {
        'values': [128, 256, 512]
        },
    'dropout': {
          'values': [0.3, 0.4, 0.5]
        },
    }

sweep_config['parameters'] = parameters_dict
```

# 第二步 初始化
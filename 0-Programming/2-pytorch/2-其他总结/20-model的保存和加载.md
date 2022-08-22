[官网博客](https://pytorch.org/tutorials/beginner/saving_loading_models.html)


## model.parameters()

所有训练的参数(weights,biases) 都保存在 model.parameters() 里面

## state_dict
layers: parameter tensor

如上的字典映射


## Buffers
[原文解释](https://discuss.pytorch.org/t/what-is-the-difference-between-register-buffer-and-register-parameter-of-nn-module/32723)
如果参数不被 Optimizer 进行训练，那么它们就会被 register 为 buffer.

Buffers 并不会在 model.parameters() 中被返回，因此，它们并不会被 Optimizer 进行优化
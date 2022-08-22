# Parameter
对一个 tensor 使用 Parameter 后，它可以出现在 parameters() 中


# Variable 
已经被丢弃了

现在，我们只需要设置 tensor 的 requires_grad = True, 只支持 float型

# buffer

如果有参数，我们希望它们被保存下来，但是又不希望它们被 optimizer 优化，那么我们就把它注册为 buffer

被注册为 buffer 的参数 也不会在 model.parrameters() 中
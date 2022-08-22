Model.eval() VS torch.no_grad()
https://discuss.pytorch.org/t/model-eval-vs-with-torch-no-grad/19615

# eval()
它会告诉 layers Model 进入了 Eval 模式。Batchnorm 和 dropout layers 将会进入 eval mode，而不是 training mode



# no_grad()
它将减少 memory usage and speed up computations。 同时 loss 也不会进入反向传播
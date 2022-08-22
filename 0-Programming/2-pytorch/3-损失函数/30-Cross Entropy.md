# 0. Cross-Entropy

# 1. 作用
Cross-entropy loss: 对于一个用于分类的 Model（这类模型的输出是概率值）, CEloss的值 衡量了 Model 的性能

# 2. 性质
- Model 的输出越接近1，CEloss的值越接近0
- Model 的输出越接近0，CEloss的值越接大

# 3. 数学公式
$$
-\sum_{c=1}^{M} y_{o, c} \log \left(p_{o, c}\right)
$$
其中：
- M 是类别的数量
- y Binary Indicator. 如果预测的 label c 是正确的，y=1，否则为0
- p 针对观测值 o 所预测出其标签为 c 的概率


# 4. 具体应用

## 4.1 Softmax Loss
>Softmax activation + CEloss

> 特点：所有值之和为 1
这种情况下，模型对输入的 IMG，输出其分别在 C 个 label 上的概率

对于 IMG-1, 它的 Label 有且仅有1个

## 4.2 Binary Cross-Entropy Loss
>Sigmoid activation + CEloss

> 与 Softmax Loss，它的值相互之间是独立的. 因此，它适合于 Multi-label classification

对于 IMG-1， 它的 Label 可能有多个


## 实际代码

在实际代码中，我们把 output_layer 产生的 logits（不要送入 softmax） 直接送入 CE



# Reference
- [1-Machine Learning Glossary](https://ml-cheatsheet.readthedocs.io/en/latest/loss_functions.html)
- [2-Blog](https://gombru.github.io/2018/05/23/cross_entropy_loss/)


CE 主要针对 multi-class classification   也可以用于 Binary classification


BCELoss 主要是对 binary classification

## 不同点
CE 用于二分类，输出是有两个 logits=[-2.34, 3.45]  Argmax(logits) -> class 1
BCEloss  用于二分类，输出是一个 logits=[-2.34] < 0 -> class0,  如果是 logits=[3.45] > 0 -> class 1 

BCEloss 的输出可以看作是 概率，例如，是 class 1 的概率为 p,  是class 0  的概率为 1-p

CE 使用了 softmax 它更适合于 multi-class classification


https://medium.com/dejunhuang/learning-day-57-practical-5-loss-function-crossentropyloss-vs-bceloss-in-pytorch-softmax-vs-bd866c8a0d23

在 pytorch 中

loss.item()的值指的是 是在一个 batch 中，所有loss处于 sample 的个数。因此

the total loss per batch = loss * batch_size = loss.item() * x.size(0)

那么 对于整个数据集的 the average loss 是  total_loss / total_size

在对比 train_loss, val_loss 的时候，它们的数据规模不一样，我们需要在 a meaningful scale 上对比，因此，我们需要执行以下两步

1. 收集整个 train_loss, val_loss

train_loss += loss.item() * batch_size

ave_loss = train_loss /len(train_dataset)



# Cross Entropy Loss in Pytorch
[blog](https://sparrow.dev/cross-entropy-loss-in-pytorch/)
[中文博客](https://blog.csdn.net/wuliBob/article/details/104119616)
[源码理解](https://zhang-yang.medium.com/understanding-cross-entropy-implementation-in-pytorch-softmax-log-softmax-nll-cross-entropy-416a2b200e34)
单标签二值分类问题
单标签的目标分类
多标签的目标分类



x: Input
yhat: predict value
y: gt 真实值 [2,1,1,0,2]

如果 y 的编码采用 One-hot 编码， 那么使用 **F.cross_entropy** 函数

**E.g.**:

Batch_size = 5
n_class = 3  label 有三个: cls1, cls2, cls3

x.shape = [5, 3]
y = softmax(x) -> shape [5, 3] 每行的和为 1.

对于第一行：
[p11, p12, p13] -> p11 + p12 + p13 = 1

p11 是 模型对于输入 x[0], 预测其值为 cls1 的概率
p12 是 模型对于输入 x[0], 预测其值为 cls2 的概率
p13 是 模型对于输入 x[0], 预测其值为 cls3 的概率
> yhat 是 模型对输入 x 在每个类别上得到的概率 

如果 y = [1, 1, 3, 3, 2]

y0=1 表明, x[0] 的真实值是 cls1
y1=1 表明，x[1] 的真实值是 cls1
y2=3 表明，x[3] 的真实值是 cls3
                                    0    1     2
                                  cls1, cls2, cls3
对于 y[0]=2, 其真实 one-hot 编码为 [0,    0,    1]
     y[1]=1,                      [0,    1,    0]
     y[2]=1,                      [0,    1,    0]
     y[3]=0,                      [1,    0,    0]
     y[4]=2,                      [0,    0,    1]

因为 CrossEntropy 的公式可知, 只有非零元素才对 Loss 有贡献

对于预测值 yhat 的第一行而言 [p11, p12, p13]， 选取 p13 为最终预测的值 送入 CrossEntropy 函数

对于 F.cross_entropy 函数[而言](https://pytorch.org/docs/stable/generated/torch.nn.functional.cross_entropy.html?highlight=cross_entropy#torch.nn.functional.cross_entropy)
- Input: shape = [Batch_size, n_class]
- target: shape = [Batch_size].  这个值为 真实值的 one-hot 编码
target = [2, 1, 1, 0, 2] -> t0=2 x[0] 的真实值为 cls3
loss = F.cross_entropy(logits, target)
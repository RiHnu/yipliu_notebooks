# MSELOSS
[Blog](https://pytorch.org/docs/stable/generated/torch.nn.MSELoss.html?highlight=mseloss)

预测值和真实值的均分误差

$$
\ell(x, y)=L=\left\{l_{1}, \ldots, l_{N}\right\}^{\top}, \quad l_{n}=\left(x_{n}-y_{n}\right)^{2}
$$

$$
\ell(x, y)= \begin{cases}\operatorname{mean}(L), & \text { if reduction }=\text { 'mean' } \\ \operatorname{sum}(L), & \text { if reduction }=\text { 'sum' }\end{cases}
$$
# Transformer

## 网络结构

### Encoder
- multi-head self-attention mechanism
- position-wise fully connected feed-forward network

> Employ a residual connection around each of the two sub-layers, followed by layer normalization. 输出可表示为:

LayerNorm(x + Sublayer(x))

#### Attention
- Scaled Dot-Product Attention

$$
\operatorname{Attention}(Q, K, V)=\operatorname{softmax}\left(\frac{Q K^{T}}{\sqrt{d_{k}}}\right) V
$$

> Q 和 K 的维度为 $d_{k}$. V 的维度为 $d_{v}$


- Multi-Head Attention
> MHA 让模型在不同的位置上 共同关注来自不同表征子空间的信息。
> Multi-head attention allows the model to jointly attend to information from different representation
subspaces at different positions.

$$
\begin{aligned}
\text { MultiHead }(Q, K, V) &=\operatorname{Concat}\left(\operatorname{head}_{1}, \ldots, \text { head }_{\mathrm{h}}\right) W^{O} \\
\text { where } \text { head }_{\mathrm{i}} &=\operatorname{Attention}\left(Q W_{i}^{Q}, K W_{i}^{K}, V W_{i}^{V}\right)
\end{aligned}
$$
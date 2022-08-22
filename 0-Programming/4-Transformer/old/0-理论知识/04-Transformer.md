# Multi-head attention 在 Transformer 中有三种方式:

1. 在 Encoder-Decoder 层

- queries come from the previous decoder layer
> q 来自前一个 decoder layer

- the memory keys and values come from the output of the encoder
> k, v 来自 encoder 的输出

- 作用：这使得 decoder 的每个位置 attention over all positions in the input sequence
- 这模仿了典型的 encoder-decoder attention机制


2. Encoder contains self-attention layers

这里 k,q,v 来自 the same place, 也就是 encoder 中 前一层的输出

> 作用: Each position in the encoder can attend to all positions in the previous layer of the encoder

3. Decoder


# Positional Encoding

## 位置编码的要求
1. 句子中每个单词的位置编码要是独一无二的
2. 位置编码值的间隔要一致
3. 能衍生至任意长度的句子

Transformer 使用的是 a fixed static embedding, 但是最近先进的Model（例如 Bert） 使用的是 learn positional embeddings
> self.pos_embedding = nn.Embedding(max_length, hid_dim)

[证明-1](https://github.com/bentrevett/pytorch-seq2seq/blob/master/6%20-%20Attention%20is%20All%20You%20Need.ipynb)

[BERT源码](https://github.com/huggingface/transformers/blob/c2dc89be6246de85fa7085d46a8a746a9ace66cc/src/transformers/models/bert/modeling_bert.py#L172)

[知乎讲解原文](https://zhuanlan.zhihu.com/p/338592312)



# Position-wise Feed-Forward Networks
> 为什么需要 FFN

Transformer 有很多层，层和层之间有 FFN， 它就是个权重矩阵，想让前一层的结果更好的适应于下一层
# CLS

- 每个 Sentence 的第一个 token 都是 [CLS]

- [CLS] 对应的 Final hidden state is used as the aggregate sequence representation for **classification task**

- [CLS] 对应的**output hidden state**是 outputs.pooler_output 或者使用 outputs[1]

在 huggingface 中指出：BERT-family of models 中的 pooler_output 是 $h_{cls}$ 进行进一步处理得到的值：将其依次送入 **a linear layer**, **a tanh activation function**. 其中 **linear layer**的 weights 是在预训练中的 NSP 过程中得到的
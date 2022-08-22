# Language Modeling
[Blog 1](https://towardsdatascience.com/language-modeling-c1cf7b983685)

假若我们知道单词序列相互跟随的概率以及理解这种依赖关系需要哪些特定的特征，这对我们处理文本数据来说是很有帮助的


Embeddings:
当我们处理文本数据时候，我们需要把每个 word 转化为一个 Sparse Vector(one-hot encoding or else dense vectors) 这就是 **Embeddings**
> Embeddings 经常是根据下游任务进行微调的



Word2vec and Glove 

Pre-trained LMs 常常会进一步的对其进行微调，使这些 embeddings 成为 task-specific representation

我们一般会用大量数据对 LMs 进行 pre-train, 期望它们能从中学习到 the inherent word and sentence level relationships between varying contexts and subjects. 当训练结束后，这就意味着 the model has learned the structure of the language, 也就是说 the language has been modeled in some latent vector/embedding space.
> 当我们拥有 LMs 后，我们即可使用它处理下游任务



[Blog 2](https://towardsdatascience.com/language-modelingii-ulmfit-and-elmo-d66e96ed754f)

## ELMo
当我们使用 Glove 时候，且固定，那么每个单词将一直是在 Glove 中的 Representation, 并不会考虑它所在的当前语境。

### Contextualized word embeddings
同时包含 the word meaning 和 the information available in the context 被称为 contextual embeddings

GloVe 使用的是 Static word representation 
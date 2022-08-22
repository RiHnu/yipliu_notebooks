文字需要被转化为数字形式才能被模型处理

# One-hot Vector
最直接的是使用这个形式，但是它无法捕获字与字之间的语义联系

# Static word embeddings
Word2Vec, Glove 等, 他们捕获了token 与 token 之间的 relationship

# Contextualized word embeddings
the word meaning + contextal information

例如：
在 SWE 中，Stick 的值是固定的。然而，在不同的语境中，Stick 拥有不同的意思

## ELMo


# Reference
[Blog](http://jalammar.github.io/illustrated-bert/)
[Blog2](https://mccormickml.com/2019/05/14/BERT-word-embeddings-tutorial/#3-extracting-embeddings)
[code](https://discuss.huggingface.co/t/generate-raw-word-embeddings-using-transformer-models-like-bert-for-downstream-process/2958)
[Bert](https://jalammar.github.io/illustrated-transformer/)
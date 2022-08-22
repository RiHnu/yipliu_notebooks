[为什么将nn.Embedding的值乘以常数](https://stackoverflow.com/questions/56930821/why-does-embedding-vector-multiplied-by-a-constant-in-transformer-model)


```python
class Embeddings(nn.Module):
    def __init__(self, d_model, vocab):
        super().__init__()
        self.lut = nn.Embedding(vocab, d_model)
        self.d_model = d_model

    def forward(self, x):
        return self.lut(x) * math.sqrt(self.d_model)
```

可以看见当 Embedding 得到后，乘以了一个常数(math.sqrt(self.d_model))

这么做的原因是，让 Embedding 的值比 Position Embedding 的值大，保留 Sentence 的语义含义
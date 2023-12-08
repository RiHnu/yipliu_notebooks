```python
from sklearn.feature_extraction.text import TfidfVectorizer

vect = TfidfVectorizer(ngram_range=(1, 3), min_df=5, max_features=2**21)

"""
ngram_range: 提取 单词的长度 min_n <= n <= max_n

min_df: 建立 vocabulary 时 忽略 terms 频率 小于 5

max_features: 建立 vocabulary 时候 仅考虑 top 2**21 的

"""
```

`TfidfVectorizer` 是一个文本特征提取器

TF-IDF: 词频-逆文档频率  Term Frequency-Inverse Document Frequency

计算一个 word 在 Document 中的重要性:
- 一个单词出现的越频繁, 它对文档的重要性就越大
- 一个单词在语料库中出现的频率越高，它对文档的区分能量就越小

用TF-IDF向量来计算查询与文档之间的相似度，以确定最相关的文档


# 输入和输出

## tokenizer
[官网博客](https://huggingface.co/docs/transformers/preprocessing)
```python
    tokenizer = AutoTokenizer.from_pretrained('bert-base-uncased')
```

1. 直接把 string 转换为 tensor

```python
tokenizer(sentence, padding='max_length', truncation='longest_first', max_length=10, return_tensors="pt")
```

**sentence**: 
- 可以是 单个 string
sentence = 'I love Xiaojie Ning! This is true'

- 也可以是 string 组成的 list
[s1, s2, ..., s_batch_size]  string 组成的 list

batch_sentences = ["Hello I'm a single sentence",
                    "And another sentence",
                    "And the very very last one"]



## model
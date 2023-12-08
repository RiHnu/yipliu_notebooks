```python
sent = 'I love hunan universtsa'
encoded = tokenizer(sent, return_tensors='pt')
encode2.word_ids()
# [None, 0, 1, 2, 3, 3, 3, 3, None]
```
word_ids 能得到该 token 在 tokenizer中被分割的 id 位置

I 对应于 id 0
love 对应于 id 1
hunan 对应于 id 2
universtasa 被分割成了三块 

```python
RobertaTokenizerFast.from_pretrained(f'{self.data_path}roberta-base/', local_files_only=True)
```
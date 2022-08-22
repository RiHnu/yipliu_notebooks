# BERT 的解释




BERT 有 1 个 embedding output 和 12 个 transformers layer




[BERTmodel](https://huggingface.co/docs/transformers/master/en/model_doc/bert#transformers.BertModel)

## last_hidden_state
> Sequence of hidden-states at the output of the last layer of the model

## pooler_output

## hidden_states
> 当 output_hidden_states=True 时，才有该值返回  Tuple. len = 13. Model 的每层输出 + 1个 embedding

13 = 1 个 embeddings + 12 个 transformer layers

[batch_size, sequence_length, hidden_size]

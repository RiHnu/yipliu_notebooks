# Bert
> 基础款

## Bert 定义时的输入参数
inputs_embeds: [batch_size, sequence_length, hidden_size]. 传统输入是 input_ids, 但是我们可以用这个参数直接输入 an embedded representation. 这样，我们就不用Bert自己的 "convert input_ids to vector"

output_attentions: 是否输出 所有层的 the attentions tensors

output_hidden_states: 是否输出 the hidden states of all layers

## BertModel 的输出参数

last_hidden_state: Model 最后一层的输出
[Batch_size, sequence_length, hidden_size]

pooler_output: 把 h_cls 送入 [nn.Linear + tanh] 后得到的值. nn.Linear 的参数由 Next sentence prediction 预训练所得
[Batch_size, hidden_size]

hidden_states: output_hidden_states=True 时，输出该值.  输出每层(nn.Embedding + each layer)的值
tuple -> [B, S, H]

attentions: output_attentions=True
[B, num_heads, S, S]



# BertForSequenceClassification
> Bert + 

## 输入

labels: 用于计算 分类 的 Loss. 值为 [0, ..., config.num_labels -1]
[B,]

## 输出
loss: 当提供 labels 的时候，返回 Loss

logits:  分类得分 (Before SoftMax)
[B, config.num_labels]


流程：
1. 将输入 input 送入 Bert
2. 得到 pooled_output
3. 将 pooled_output 送入 Dropout -> classifier(nn.Linear)
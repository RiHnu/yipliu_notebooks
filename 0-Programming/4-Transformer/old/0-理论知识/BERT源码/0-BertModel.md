## 0. 源码

```python
class BertModel(BertPreTrainedModel):

    def __init__(self, config, add_pooling_layer=True)
        self.config = config

        self.embeddings = BertEmbeddings(config)

        self.encoder = BertEncoder(config)

        self.pooler = BertPooler(config) 

        # Initialize weights and apply final processing
        self.post_init()

def forward(
        self,
        input_ids=None,           # 输入的 sentence 被 tokenizer处理后的值
        attention_mask=None,      # 0：not masked;   1: masked
        token_type_ids=None,      # 0: sentence A;   1: sentence B
        position_ids=None,        
        head_mask=None,
        inputs_embeds=None,
        encoder_hidden_states=None,
        encoder_attention_mask=None,
        past_key_values=None,
        use_cache=None,
        output_attentions=None,    # bool 是否输出 the attentions tensors of all attention layers
        output_hidden_states=None, # bool 是否输出 the hidden states of all layers
        return_dict=None,
    ):



```
# 使用 GPT-J 的细则

1. 大小 For RAM
   需要消耗 2倍的 RAM，大约 48G 

为了减少内存消耗的方法:
model = GPTJForCausalLM.from_pretrained(
    "EleutherAI/gpt-j-6B", revision="float16", torch_dtype=torch.float16, low_cpu_mem_usage=True
)
- 使用 torch_dtype 初始化 model in half-precision
- low_cpu_mem_usage: 从48 -> 24


2. 大小 For GPU

16 GB for inference

GPTJForCausalLM
> The GPT-J Model transformer with a language modeling head on top.

输出:
- loss. 当提供 labels 的时 输出 loss for next-token prediction
- logits [batch_size, sequence_length, config.vocab_size]  SoftMax之前, 对 vocab 中的预测得分


# generate()

sampling_params = \
        {
            "max_tokens": 10,
            "temperature": 0.1, # [0.1, 0.3, 0.6]
            "top_p": 0.9,
            "num_return_sequences": 10,
            "repetition_penalty": 1.2, # [1.0, 1.2, 1.5, 1.8]
            'use_cache': True,
            'output_scores': True,
            'return_dict_in_generate': True,
            'do_sample': True,
        }

输入:
- do_sample: 是否使用 sampling, 否则使用 greedy decoding
- temperature: 
  如果有下面的输出结果 'apple'=0.6, 'shoes'=0.2, 'pants'=0.3
  temperature 值越低, 那么输出为 apple 的可能性越高.
  temperature 值越高, 输出其他值的可能性就越高
  > temperature 值越高，输出的多样性越大

- top_p:  
  只使用 top_p 和 temperature 中的一个. 当使用其中一个时, 另一个设置为 1

- max_length: 生成tokens 的最大长度=prompt + max_new_tokens

- repetition_penalty：惩罚重复。1.0 意味着没有惩罚
- num_return_sequences: 
- use_cache: 是否使用 cache to speed up decoding
- output_scores: 是否输出 socres
  
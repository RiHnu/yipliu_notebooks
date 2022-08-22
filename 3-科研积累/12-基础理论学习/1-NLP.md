# 0 预训练


## 1. Masked Language Model Explained

对于给定  Sentence 以一定的概率 对其中的 word 进行 Masked. 然后让 Model 基于这个 Sentence 预测这些 masked word


## 2. Causal Language Model Explained
> 预测 the masked token in a given sentence

与 MLM 不同的是，这种预测 要么基于 Masked word 左边的 words, 要么基于右边的 words


##
https://machinelearningmastery.com/beam-search-decoder-natural-language-processing/
https://zhuanlan.zhihu.com/p/28048246

# 1. Greedy Search Decoder
返回 最大值 Max

# 2. Beam Search Decoder
Return a list of most likely output sequences


与 Greedy 不同的是，Beam 返回 the K most likely (K 是用户自定义的参数)

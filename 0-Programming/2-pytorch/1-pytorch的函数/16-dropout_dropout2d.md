`Dropout2d`: Each channel will be zeroed out independently with probability p
    Input: (N, C, H, W) or (N, C, L)
> 只有 channel 位的元素会以 P 的概率变为 0

`Dropout`: randomly zeroes some of the elements of the input tensor with probability p 
> 一个 tensor 每个位置上的元素都有 p 的可能变为 0
    Input: any shape
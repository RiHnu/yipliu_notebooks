# 在 py 文件中设置

os.environ['CUDA_VISIBLE_DEVICES']='0,1,2'
> 该命令要放在 最前面

# 使用 with 语句
with torch.cuda.device(0):
    text, audio, vision, eval_attr = text.cuda(), audio.cuda(), vision.cuda(), eval_attr.cuda()
[model checkpointing](https://pytorch-lightning.readthedocs.io/en/latest/api/pytorch_lightning.callbacks.model_checkpoint.html?highlight=modelcheck#pytorch_lightning.callbacks.model_checkpoint.ModelCheckpoint)
> 通过监控指标， 训练时自动保存模型

模型中只要写了 log() 或者 log_dict() 的，均可作为指标候选值

当训练完成后，可使用:
- best_model_path 返回 the path to the best checkpoint file
- best_model_score 返回 相应的 score

**dirpath**: 保存文件路径
默认值为 None, 直接等于 Trainer 的 default_root_dir

**filename**: checkpoint filename


**monitor**: 健康的指标

**save_last**: True 时候 save the model at the end of the epoch to a file *last.ckpt*
                保存最后的 checkpoints, 名称为 last.ckpt


**save_top_k**: 最好的 K 个 model 将会被保存, 名称为 **filename**

**mode**: max or min. max 意味着 越大的 monitor值将是最好的

**auto_insert_metric_name** 
    True: checkpoint 的名称将包含 the metric name  例如 checkpoint_{epoch: 02d}-{acc:02d}
    当 epoch=1, acc=80 时，上式为 checkpoint_epoch=01-acc-80.ckp

    如果我们 metric name 包含 '/' 时候，需要把它设置为 False

**save_weights_only**
    True: 将只保存模型的 weights
    False: the optimizer states, lr 等等都会被保存在 checkpoint

**every_n_train_steps**
    None or 0: 训练时，我们将跳过 saving 它与 train_time_interval 和 every_n_epochs 互斥



# [Early Stopping]

> 监控某个指标，并在它不增加时时停止训练

**monitor** 监控的指标

**min_delta**: 最小的变化值，即可被认为是改进了的。也就是说该变量必须 大于/小于 min_delta

**patience**: 再 patience 次内，monitor 若没做出改变 则停止训练

patience 的值是 validation checks 的值，并不是 training epochs 的值
若 check_val_every_n_epoch=10，patience=3. 那么 trainer 将会执行至少 40 个 epochs

**mode** max or min

**strict**: 当 monitor 的值没有找到时，是否报错。默认为 True



# StochasticWeightAveraging

swa_epoch_start: 若给的是 int, 那么将要从 -th epoch 开始生效
                若给的是 float, 那么从 swa_epoch_start * max_epoch 开始生效

swa_lrs:

annealing_epochs: 默认为 10

annealing_strategy: cos, linear  默认为 cos

avg_fn
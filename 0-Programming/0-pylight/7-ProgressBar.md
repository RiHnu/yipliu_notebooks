v_num = the version number of experiment
[v_num 官网解释](https://github.com/PyTorchLightning/pytorch-lightning/issues/1595)



# 参数解析
[官网](https://pytorch-lightning.readthedocs.io/en/latest/extensions/logging.html?highlight=tracking_uri)


on_step: logs the metric at the current step

on_epoch: automatically accumulates and logs at the end of the epoch

prog_bas: 是否在 progress bar 上显示 （默认为 False)

logger: 是否 log 到 logger （默认为 True)
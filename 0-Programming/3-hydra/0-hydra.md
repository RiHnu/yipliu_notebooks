# hydra
[最好的博客](https://towardsdatascience.com/complete-tutorial-on-how-to-use-hydra-in-machine-learning-projects-1c00efcc5b9b)
## hydra.utils.instantiate

omegaconf: 仅仅是用来提供类型

当运行 hydra 会修改 working directory

当在 src/main.py 运行代码时， hydra 会自动把它移动到 src/outputs/YYYY-mm-dd/HH-MM-SS/main.py
-> 这就要提醒我们保存路径的时候一定要使用绝对路径.
-> 使用相对路径的话，需要考虑所需路径和 src/outputs/../../main.py 的相对路径


hydra.utils.get_original_cwd(): get the original current working directory. -> src

hydra.utils.to_absolute_path(file_name)



# output

config.yaml: 本次实验所使用的参数 

hydra.yaml: Copy of the hydra config file

overrides.yaml. 本次实验，在 command line 输入的参数

main.log - output of the logger would be stored herer

# config

/# @package _group_
在一个文件夹中有两个 xxx.yaml  可以在每个文件的开头写上 这个代码，表示：
这两个文件是独立的，只能选择其中一个


defaults:
  - db: mysql

解释：defaults 是一个特殊的指令。它告诉 Hydra 使用 mysql.yaml

当文件们没有一个共同的 parent path 时候使用 # @package _global_
当文件们有一个共同的 parent path 的时候使用 # @package _group_

# How
当执行 python main.py 时候，Hydra 会自动创建 outputs 目录 outputs/YYYY-mm-dd/HH-MM-SS

# package _group_
config.groups: 每个 config file 相互独立。我们只能选择它们其中的一个

Hydra 1.1 _group_ will become the default package and there will be no need to add the special comment

# package _global_
设置为 _global_ 后，我们就只能在这个文件中修改 参数，不能在 experiment 里面修改
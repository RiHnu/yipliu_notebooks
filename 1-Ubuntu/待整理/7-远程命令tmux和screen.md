# tmux 

## 创建一个新会话

tmux new -s name

## 离开当前会话

`ctrl+b` 然后再安 `d`

## 离开并关闭当前会话

`ctrl+d`

## 显示当前存在的进程

`tmux ls`

## 关闭某个会话

tmux kill-session -t session_name

## 进入某个会话

**tmux** attach -t session_name
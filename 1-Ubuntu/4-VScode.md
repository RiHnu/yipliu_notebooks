# 1. 远程配置

**Step 1:** 检查本地电脑是否有 SSH，没有的话 用命令生成
[官网步骤](https://code.visualstudio.com/docs/remote/troubleshooting#_quick-start-using-ssh-keys)
>Win10: C:\Users\your-user\.ssh\id_rsa.pub

**Step 2:** 赋予权限


**Step 3:** 本地 config 文件配置
>C:\Users\your-user\.ssh\cofing
添加如下信息

Host Server
	Hostname IP
	User user_name
	IdentityFile C:/Users/your-user/.ssh/id_rsa-remote-ssh


# 2. VScode 中使用 screen 命令
[博客参考](https://www.autodl.com/docs/daemon/)

**第一步**
直接在 终端处执行 screen, 随后会跳转一个新的 终端. 该终端处执行的命令将会被保护

**第二步**
关闭 Vscode 后 想再次进入 那个被保护的终端，使用 screen -ls 找到那个终端
使用 screen -r xxx 即可进入

常见命令

screen -S : 指定 screen 的名称

screen -r: 回复screen
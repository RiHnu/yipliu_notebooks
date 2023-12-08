# 0. 简介

账号名: cl
密码:   1

在 `/mnt/HDD3` 中创建一个 `cl` 的文件夹就行, 以后自己的相关代码和文件都放在这里, 大约还有 `570G` 不够用再联系我


本文记录开发过程中使用过的远程工具

**Key Words**: FileZilla, X2GO, Termius, cmd/SSH, VScode




## 0.2 远程传输文件

- 安装 FileZilla

  - Windows 下安装[客户端](https://zhuanlan.zhihu.com/p/35846871)
  
  - Ubuntun安装[openssh-server](https://blog.csdn.net/baidu_38505667/article/details/103029510?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control)

# 1. GUI界面大法

## 1.1 X2GO

- 远程控制 ==> 安装 X2GO
   - 服务器上安装[X2GO Server](https://wiki.x2go.org/doku.php/doc:installation:x2goserver)
   - 服务器上安装XFCE4作为服务器的虚拟化桌面："sudo apt-get install xfce4"
   - 在本地安装[X2GO Client](http://ithelp.physics.ucdavis.edu/kb/x2go)
   - 在Client登录时候，登录界面要与你安装的(XFCE)一致

## 1.2 Win10 远程桌面
Win10 自带的远程桌面

# 2. 命令终端法

## 2.1 Termius

> 终端远程，无GUI界面

这个非常厉害，手机也能用。同时也具有远程传输文件的功能


# 3. 其他软件远程使用

## 3.1 VScode

> VScode 的远程开发需要使用插件：Remote-SSH
> 后期使用这个 方便的

安装和使用教程请看第三章[VScode远程](https://github.com/yipliu/KeyPointInLearning/blob/main/3-VScode/3.2-VScode%E8%BF%9C%E7%A8%8B.md)





# 下面 VScode 远程配置方法 不一定全对，我记录完了也没及时修改

# 1. 远程配置

**Step 1:** 检查本地电脑是否有 SSH，没有的话 用命令生成
[官网步骤](https://code.visualstudio.com/docs/remote/troubleshooting#_quick-start-using-ssh-keys)
>Win10: C:\Users\your-user\.ssh\id_rsa.pub

**Step 2:** 赋予权限
**第一步**
把 win 中的公匙 `C:\Users\xx\.ssh\id_rsa-remote-ssh.pub`  复制到 ubuntu 中 `.ssh` 文件夹中. 

**第二步**
在服务器中执行
```
cat id_rsa-remote-ssh.pub >> authorized_keys
```
chmod 700 ./.ssh
chmod 600 ./.ssh/authorized_keys
```

**第三步***
删除 win 中 known_hosts 中对于IP的记录

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


新版本的 VScode 放弃了对 python3.6的 debug 支持
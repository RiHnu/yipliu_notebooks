# 注意 g++ 和 gcc 的版本 -> 10
> 系统默认是 9 需要切换到 10

1. 查询系统中所有 gcc

ls /usr/bin/gcc*

2. gcc 和 g++ 的安装与切换

https://www.fosslinux.com/39386/how-to-install-multiple-versions-of-gcc-and-g-on-ubuntu-20-04.htm#google_vignette


# 重新编译时候删除已编译文件
rm -rf build/ **/*.so

[官网安装教程](https://www.fast-downward.org/ObtainingAndRunningFastDownward)
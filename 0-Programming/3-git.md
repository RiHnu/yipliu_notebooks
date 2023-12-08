使用
git clone --recurse-submodules 
命令时，部分子模块因为网络原因下载失败，使用下面命令继续下载
git submodule update --init --recursive

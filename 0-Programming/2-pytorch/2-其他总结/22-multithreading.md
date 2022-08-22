# Multiprocessing
> 如果想充分利用 CPU 的多内核特性

1. 规避 Global Interpreter Lock 的限制


# Multithreading
> if your particular task is Input/Output bound, then you’ll generally want to use multithreading to improve the performance of your applications.


## Process

依据不同的 Platform, multiprocessing 支持三种 start methods

- spawn
> unnecessary file descriptors and handles from the parent process will not be inherited

- fork
> 只支持 Unix

- forkserver
> No unnecessary resources are inherited.


mp.set_start_method('spawn'): 选择一种方法. 只能使用一次

get_context('spawn'): 该方法允许在统一个 program 中 使用不同的 start methods

## 通讯

## Queues
> 用于 processes 间的通讯

## Pipes

## Sharing state between processes

# Server process

## manager


# 函数介绍

## Process

**group**: None. 必须为此值

**target**: the callable object

**name**: the process name

**args**: the argument tuple for the target invocation


- run(): 

- start(): 启动 process

- join()
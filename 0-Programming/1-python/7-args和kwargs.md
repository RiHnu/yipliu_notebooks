当我们不确定 *arguments* 的数量时候使用 `*args` 和 `**kwargs` 

`*args`: 允许我们输入任意长度的 non keyword arguments

参数前面加 `*` 让输入打包为一个 tuple


`**kwargs`: 允许我们输入任意长度的  keyword arguments

输入的参数被打包为 dictionary

```python

def intro(**data):
    print(type(data))

intro(Firstname="Sita", Lastname="Sharma", Age=22, Phone=1234567890)
```
实际上, 传入的 data 是一个 dict. data={'Firstname': "Sita", 'Lastname': "Sharma", 'Age':22, 'Phone':1234567890}

[参考博客](https://www.programiz.com/python-programming/args-and-kwargs#:~:text=*args%20passes%20variable%20number%20of,a%20dictionary%20can%20be%20performed.)
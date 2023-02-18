# Abstract Base Classes

```python
class Action(ABC):
    def __init__(self):
        ...

    @abstractmethod
    def is_stop(self) -> bool:
        """
        :return: True if this is a STOP-action, False otherwise.
        """
        ...
```


`Action` 就是一个 abstract class

`is_stop` 就是一个 abstractmethod


那么, 我们再创建 Action 的子类时候, `is_stop` 需要具体化, 如下

```python
class ChildAction(ABC):
    def __init__(self):
        ...

    @abstractmethod
    def is_stop(self) -> bool:
        """
        :return: True if this is a STOP-action, False otherwise.
        """
        print("I have been create !")
        ...
```
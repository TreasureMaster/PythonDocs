# functools.partialmethod\(\)

###  \(_class\)_ functools.partialmethod\(_func_, _/_, _\*args_, _\*\*keywords_\)

Вернуть новый дескриптор **partialmethod**, который ведет себя как [partial](functools.partial.md), за исключением того, что он предназначен для использования в качестве определения метода, а не для прямого вызова.

_**func**_ должен быть [дескриптором](https://docs.python.org/3/glossary.html#term-descriptor) или вызываемым \(оба объекта, как и обычные функции, обрабатываются как дескрипторы\).

Когда _**func**_ является дескриптором \(например, обычная функция Python, [classmethod \(\)](https://docs.python.org/3/library/functions.html#classmethod), [staticmethod \(\)](https://docs.python.org/3/library/functions.html#staticmethod), **abstractmethod \(\)** или другой экземпляр **partialmethod**\), вызовы `__get__` делегируются базовому дескриптору, а в качестве результата возвращается соответствующий [объект partial](obekty-partial.md).

Когда _**func**_ вызывается без дескриптора, соответствующий связанный метод создается динамически. Это ведет себя как обычная функция Python при использовании в качестве метода: аргумент _**self**_ будет вставлен в качестве первого позиционного аргумента, даже перед _**args**_ и _**keywords**_, предоставленными конструктору **partialmethod**.

Пример:

```python
>>> class Cell:
...     def __init__(self):
...         self._alive = False
...     @property
...     def alive(self):
...         return self._alive
...     def set_state(self, state):
...         self._alive = bool(state)
...     set_alive = partialmethod(set_state, True)
...     set_dead = partialmethod(set_state, False)
...
>>> c = Cell()
>>> c.alive
False
>>> c.set_alive()
>>> c.alive
True
```

_Новое в версии 3.4_.


# functools.partial\(\)

###  functools.partial\(_func_, _/_, _\*args_, _\*\*keywords_\)

Возвращает новый [объект partial](obekty-partial.md), который при вызове будет вести себя как _**func**_, вызываемый с позиционными аргументами _**args**_ и ключевыми аргументами _**keywords**_. Если вызову передаются дополнительные аргументы, они добавляются к _**args**_. Если предоставляются дополнительные аргументы ключевого слова, они расширяют и переопределяют ключевые слова. Примерно эквивалентно:

```python
def partial(func, /, *args, **keywords):
    def newfunc(*fargs, **fkeywords):
        newkeywords = {**keywords, **fkeywords}
        return func(*args, *fargs, **newkeywords)
    newfunc.func = func
    newfunc.args = args
    newfunc.keywords = keywords
    return newfunc
```

**partial \(\)** используется для частичного приложения функции, которое «замораживает» некоторую часть аргументов функции и/или ключевых слов, в результате чего создается новый объект с упрощенной подписью. Например, **partial \(\)** можно использовать для создания вызываемого объекта, который ведет себя как функция [int \(\)](https://docs.python.org/3/library/functions.html#int), где базовый аргумент по умолчанию равен двум:

```python
>>> from functools import partial
>>> basetwo = partial(int, base=2)
>>> basetwo.__doc__ = 'Convert base 2 string to an int.'
>>> basetwo('10010')
18
```


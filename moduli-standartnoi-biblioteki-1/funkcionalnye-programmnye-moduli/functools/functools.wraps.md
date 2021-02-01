# functools.wraps\(\)

####  @functools.wraps\( _wrapped_, _assigned=WRAPPER\_ASSIGNMENTS_, _updated=WRAPPER\_UPDATES_ \)

Это удобная функция для вызова [update\_wrapper \(\)](functools.update_wrapper.md) в качестве декоратора функции при определении функции-оболочки. Это эквивалентно `partial(update_wrapper, wrapped=wrapped, assigned=assigned, updated=updated)`. Например:

```python
>>> from functools import wraps
>>> def my_decorator(f):
...     @wraps(f)
...     def wrapper(*args, **kwds):
...         print('Calling decorated function')
...         return f(*args, **kwds)
...     return wrapper
...
>>> @my_decorator
... def example():
...     """Docstring"""
...     print('Called example function')
...
>>> example()
Calling decorated function
Called example function
>>> example.__name__
'example'
>>> example.__doc__
'Docstring'
```

Без использования этой фабрики декораторов имя функции примера было бы `'wrapper'`, а строка документации исходного **example \(\)** была бы потеряна.


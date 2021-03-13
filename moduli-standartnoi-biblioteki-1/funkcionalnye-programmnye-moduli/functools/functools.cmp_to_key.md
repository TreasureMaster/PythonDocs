# functools.cmp\_to\_key\(\)

###  functools.cmp\_to\_key\(_func_\)

Преобразует функцию сравнения старого стиля в [ключевую функцию](https://docs.python.org/3/glossary.html#term-key-function). Используется с инструментами, которые принимают ключевые функции \(например, [sorted \(\)](https://docs.python.org/3/library/functions.html#sorted), [min \(\)](https://docs.python.org/3/library/functions.html#min), [max \(\)](https://docs.python.org/3/library/functions.html#max), [heapq.nlargest \(\)](https://docs.python.org/3/library/heapq.html#heapq.nlargest), [heapq.nsmallest \(\)](https://docs.python.org/3/library/heapq.html#heapq.nsmallest), [itertools.groupby \(\)](https://docs.python.org/3/library/itertools.html#itertools.groupby)\). Эта функция в основном используется как инструмент перехода для программ, конвертируемых из Python 2, которые поддерживают использование функций сравнения.

Функция сравнения - это любой вызываемый объект, который принимает два аргумента, сравнивает их и возвращает отрицательное число, если меньше, чем равенство, или положительное число, если больше. Ключевая функция - это вызываемая функция, которая принимает один аргумент и возвращает другое значение, которое будет использоваться в качестве ключа сортировки.

Пример:

```python
sorted(iterable, key=cmp_to_key(locale.strcoll))  # порядок сортировки с учетом локали
```

Примеры сортировки и краткое руководство по сортировке см. в разделе [Сортировка КАК](https://docs.python.org/3/howto/sorting.html#sortinghowto).

_Новое в версии 3.2_.


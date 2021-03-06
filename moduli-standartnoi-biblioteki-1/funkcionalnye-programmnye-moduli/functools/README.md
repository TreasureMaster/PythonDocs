# functools

**functools** - Функции высшего порядка и операции с вызываемыми объектами.

Модуль **functools** предназначен для функций высшего порядка: функций, которые действуют или возвращают другие функции. В общем, любой вызываемый объект можно рассматривать как функцию для целей этого модуля.

Модуль **functools** определяет следующие функции:

*  [@functools.cache\(\)](functools.cache.md) - кеширует функции
*  [@functools.cached\_property\(\)](functools.cached_property.md) - преобразует метод класса в кешированное свойство
*  [functools.cmp\_to\_key\(\)](functools.cmp_to_key.md) - преобразует функцию сравнения старого стиля в ключевую функцию
*  [@functools.lru\_cache\(\)](functools.lru_cache.md) - декоратор для обертывания функции мемоизирущим объектом
*  [@functools.total\_ordering](functools.total_ordering.md) - дополняет методы упорядочивания \(больше, меньше, равно и т.п.\)
*  [functools.partial\(\)](functools.partial.md) - возвращает объект partial, похожий на функцию с доп. аргументами.
*  [_class_ functools.partialmethod\(\)](functools.partialmethod.md) - то же, что и **partial**, но для методов классов
*  functools.reduce\(\)
*  @functools.singledispatch
*  _class_ functools.singledispatchmethod\(\)
*  [functools.update\_wrapper\(\)](functools.update_wrapper.md) - обновляет обернутую функцию до оборачиваемой
*  [@functools.wraps\(\)](functools.wraps.md) - удобная функция вызова [update\_wrapper\(\)](functools.update_wrapper.md), декоратор

Объекты partial

* partial.func
* partial.args
* partial.keywords


# functools.total\_ordering

###  @functools.total\_ordering

Дает для класса, определяющего один или несколько методов упорядочения с расширенными возможностями сравнения, этот декоратор класса предоставляет все остальное. Это упрощает работу по указанию всех возможных операций расширенного сравнения:

Класс должен определять одно из `__lt__()`, ****`__le__()`, `__gt__()` или ****`__ge__()`. Кроме того, класс должен предоставлять метод `__eq__()`.

Например:

```python
@total_ordering
class Student:
    def _is_valid_operand(self, other):
        return (hasattr(other, "lastname") and
                hasattr(other, "firstname"))
    def __eq__(self, other):
        if not self._is_valid_operand(other):
            return NotImplemented
        return ((self.lastname.lower(), self.firstname.lower()) ==
                (other.lastname.lower(), other.firstname.lower()))
    def __lt__(self, other):
        if not self._is_valid_operand(other):
            return NotImplemented
        return ((self.lastname.lower(), self.firstname.lower()) <
                (other.lastname.lower(), other.firstname.lower()))
```

{% hint style="info" %}
Хотя этот декоратор упрощает создание полностью упорядоченных типов с хорошим поведением, он все же достигается за счет более медленного выполнения и более сложных трассировок стека для производных методов сравнения. Если бенчмаркинг производительности показывает, что это узкое место для данного приложения, реализация вместо этого всех шести разнообразных методов сравнения, скорее всего, обеспечит легкий прирост скорости.
{% endhint %}

_Новое в версии 3.2_.

_Изменено в версии 3.4:_ теперь поддерживается возврат **NotImplemented** из базовой функции сравнения для нераспознанных типов.


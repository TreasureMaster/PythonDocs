# socket.timeout

### socket.timeout exception

Подкласс OSError, это исключение возникает, когда тайм-аут происходит в сокете, для которого были включены тайм-ауты с помощью предыдущего вызова [settimeout \(\)](../obekty-soketov/socket.settimeout.md) \(или неявно через [setdefaulttimeout \(\)](../funkcii-soketov/socket.setdefaulttimeout.md)\). Сопутствующее значение - это строка, значение которой в настоящее время всегда «истекло».

_Изменено в версии 3.3:_ Этот класс был сделан подклассом OSError.


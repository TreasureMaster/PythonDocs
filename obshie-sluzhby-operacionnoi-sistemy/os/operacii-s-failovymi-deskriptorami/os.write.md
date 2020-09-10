# os.write \(\)

### os.write \( _fd_, _str_ \)

Записывает байтовую строку в _**str**_ в файловый дескриптор _**fd**_.

Возвращает количество фактически записанных байтов.

{% hint style="info" %}
Эта функция предназначена для низкоуровневого ввода-вывода и должна применяться к файловому дескриптору, возвращаемому [os.open \(\)](os.open.md) или [pipe \(\)](os.pipe.md). Чтобы записать «файловый объект», возвращаемый встроенной функцией [open \(\)](../../../vstroennye-funkcii/open.md), [popen \(\)](../upravlenie-processami/os.popen.md) или [fdopen \(\)](../sozdanie-failovogo-obekta/os.fdopen.md), или [sys.stdout](../../../moduli-standartnoi-biblioteki/sluzhby-sredy-vypolneniya-python/sys/sys.stdin-sys.stdout-sys.stderr.md) или [sys.stderr](../../../moduli-standartnoi-biblioteki/sluzhby-sredy-vypolneniya-python/sys/sys.stdin-sys.stdout-sys.stderr.md), используйте его метод write \(\).
{% endhint %}

_Изменено в версии 3.5:_ если системный вызов прерывается и обработчик сигнала не вызывает исключения, функция теперь повторяет системный вызов вместо того, чтобы вызывать исключение InterruptedError \(объяснение см. в [PEP 475](https://www.python.org/dev/peps/pep-0475/)\).


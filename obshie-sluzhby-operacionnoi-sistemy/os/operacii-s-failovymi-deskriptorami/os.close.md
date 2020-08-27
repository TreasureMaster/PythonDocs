# os.close \(\)

### os.close \( _fd_ \)

Закрывает файловый дескриптор _**fd**_.

{% hint style="info" %}
Эта функция предназначена для низкоуровневого ввода-вывода и должна применяться к файловому дескриптору, возвращаемому [os.open \(\)](os.open.md) или [pipe \(\)](os.pipe.md). Чтобы закрыть «файловый объект», возвращаемый встроенной функцией [open \(\)](../../../vstroennye-funkcii/open.md), [popen \(\)](../upravlenie-processami/os.popen.md) или [fdopen \(\)](../sozdanie-failovogo-obekta/os.fdopen.md), используйте его метод close \(\).
{% endhint %}


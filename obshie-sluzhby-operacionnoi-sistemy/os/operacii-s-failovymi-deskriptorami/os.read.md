# os.read \(\)

### os.read \( _fd_, _n_ \)

Читает не более _**n**_ байтов из файлового дескриптора _**fd**_.

Возвращает байтовую строку, содержащую прочитанные байты. Если достигнут конец файла, на который указывает _**fd**_, возвращается пустой объект байтов.

{% hint style="info" %}
Эта функция предназначена для низкоуровневого ввода-вывода и должна применяться к файловому дескриптору, возвращаемому [os.open \(\)](os.open.md) или [pipe \(\)](os.pipe.md). Чтобы прочитать «файловый объект», возвращаемый встроенной функцией [open \(\)](../../../vstroennye-funkcii/open.md), [popen \(\)](../upravlenie-processami/os.popen.md), [fdopen \(\)](../sozdanie-failovogo-obekta/os.fdopen.md) или [sys.stdin](../../../moduli-standartnoi-biblioteki/sluzhby-sredy-vypolneniya-python/sys/sys.stdin-sys.stdout-sys.stderr.md), используйте его методы `read ()` или `readline ()`.
{% endhint %}


# stat

### Интерпретация результатов os.stat \(\)

Модуль **stat** определяет константы и функции для интерпретации результатов [os.stat \(\)](../obshie-sluzhby-operacionnoi-sistemy/os/faily-i-direktorii/os.stat.md), [os.fstat \(\)](../obshie-sluzhby-operacionnoi-sistemy/os/operacii-s-failovymi-deskriptorami/os.fstat.md) и [os.lstat \(\)](../obshie-sluzhby-operacionnoi-sistemy/os/faily-i-direktorii/os.lstat.md) \(если они существуют\). Для получения полной информации о вызовах `stat ()`, `fstat ()` и `lstat ()` обратитесь к документации для вашей системы.

_Изменено в версии 3.4:_ модуль **stat** поддерживается реализацией C.

Модуль **stat** определяет следующие функции для проверки определенных типов файлов:

* **stat.S\_ISDIR \(**_**mode**_**\)** - возвращает ненулевое значение, если _**mode**_ является каталогом
* stat.S\_ISCHR \(mode\)
* stat.S\_ISBLK \(mode\)
* **stat.S\_ISREG \(**_**mode**_**\)** - возвращает ненулевое значение, если _**mode**_ является обычным файлом
* не заполнено...

Обычно вы используете функции `os.path.is* ()` для проверки типа файла; приведенные здесь функции полезны, когда вы выполняете несколько тестов одного и того же файла и хотите избежать накладных расходов на системный вызов `stat ()` для каждого теста. Они также полезны при проверке информации о файле, который не обрабатывается [os.path](os.path/), например при проверке блочных и символьных устройств.

Пример:

```python
import os, sys
from stat import *

def walktree(top, callback):
    '''рекурсивно спускается по дереву каталогов с корнем вверху,
    исполняет функции обратного вызова для каждого обычного файла'''

    for f in os.listdir(top):
        pathname = os.path.join(top, f)
        mode = os.stat(pathname).st_mode
        if S_ISDIR(mode):
            # Это каталог, заходим в него
            walktree(pathname, callback)
        elif S_ISREG(mode):
            # Это файл, вызываем функцию обратного вызова
            callback(pathname)
        else:
            # Неизвестный тип файла, печатаем сообщение
            print('Skipping %s' % pathname)

def visitfile(file):
    print('visiting', file)

if __name__ == '__main__':
    walktree(sys.argv[1], visitfile)
```

Предоставляет дополнительную служебную функцию для преобразования режима файла в удобочитаемую строку:

* stat.filemode \(\)

Все перечисленные ниже переменные - это просто символические индексы в кортеже из 10, возвращаемом [os.stat \(\)](../obshie-sluzhby-operacionnoi-sistemy/os/faily-i-direktorii/os.stat.md), [os.fstat \(\)](../obshie-sluzhby-operacionnoi-sistemy/os/operacii-s-failovymi-deskriptorami/os.fstat.md) или [os.lstat \(\)](../obshie-sluzhby-operacionnoi-sistemy/os/faily-i-direktorii/os.lstat.md).

* **stat.ST\_MODE** - режим защиты _**inode**_
* не заполнено...
* **stat.ST\_SIZE** - размер простого файла в байтах; количество данных, ожидающих некоторых специальных файлов
* не заполнено...


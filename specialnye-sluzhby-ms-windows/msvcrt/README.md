# msvcrt

Эти функции обеспечивают доступ к некоторым полезным возможностям на платформах Windows. Некоторые модули более высокого уровня используют эти функции для создания реализаций своих служб Windows. Например, модуль getpass использует это в реализации функции getpass \(\).

Дополнительную документацию по этим функциям можно найти в документации API платформы.

Модуль реализует как обычные, так и широкие варианты посимвольного консольного ввода-вывода. Обычный API работает только с символами ASCII и имеет ограниченное использование для интернационализированных приложений. По возможности следует использовать широкий API символов.

_Изменено в версии 3.3:_ операции в этом модуле теперь вызывают ошибку OSError там, где возникла ошибка IOError.

#### Файловые операции

* locking \(\)
* не заполнено...

#### Консольный ввод-вывод

* kbhit \(\)
* [getch \(\)](https://treasuremaster.gitbook.io/python-docs/specialnye-sluzhby-ms-windows/msvcrt/msvcrt.getch) - возвращает значение Unicode
* getwch \(\)
* [getche \(\)](https://treasuremaster.gitbook.io/python-docs/specialnye-sluzhby-ms-windows/msvcrt/msvcrt.getche) - возвращает значение Unicode, если оно представляет печатный символ
* getwche \(\)
* [putch \(\)](https://treasuremaster.gitbook.io/python-docs/specialnye-sluzhby-ms-windows/msvcrt/msvcrt.putch) - вывести на консоль строковый символ
* putwch \(\)
* ungetch \(\)
* ungetwch \(\)

#### Другие функции

* heapmin \(\)


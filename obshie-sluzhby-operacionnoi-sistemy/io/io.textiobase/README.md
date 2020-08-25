# io.TextIOBase

#### class io.TextIOBase

Базовый класс для текстовых потоков. Этот класс предоставляет символьный и строковый интерфейс для потокового ввода-вывода. Он наследует IOBase. Общедоступного конструктора нет.

**TextIOBase** предоставляет или переопределяет эти атрибуты данных и методы в дополнение к атрибутам IOBase:

* encoding
* errors
* newlines
* buffer
* detach \(\)
* read \(\)
* [readline \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.textiobase/io.textiobase.readline) - читает до новой строки или EOF и возвращает одну строку
* seek \(\)
* tell \(\)
* [write \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.textiobase/io.textiobase.write) - пишет строку в поток и возвращает количество записанных символов


# io.BufferedIOBase

#### _class_ io.BufferedIOBase

Базовый класс для двоичных потоков, поддерживающих буферизацию. Он наследует IOBase. Общедоступного конструктора нет.

Основное отличие от RawIOBase заключается в том, что методы read \(\), readinto \(\) и write \(\) будут пытаться \(соответственно\) прочитать столько ввода, сколько запрошено, или использовать весь данный вывод, возможно, за счет выполнения более одного системного вызова.

Вдобавок эти методы могут вызывать исключение BlockingIOError, если базовый необработанный поток находится в неблокирующем режиме и не может принимать или передавать достаточно данных; в отличие от своих аналогов RawIOBase, они никогда не вернут `None`.

Кроме того, у метода read \(\) нет реализации по умолчанию, которая полагается на readinto \(\).

Типичная реализация **BufferedIOBase** не должна наследовать от реализации RawIOBase, а должна оборачиваться, как это делают BufferedWriter и BufferedReader.

**BufferedIOBase** предоставляет или переопределяет эти методы и атрибуты в дополнение к IOBase:

* raw
* detach \(\)
* [read \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bufferediobase/io.bufferediobase.read) - читает и возвращает байты
* read1 \(\)
* readinto \(\)
* readinto1 \(\)
* [write \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bufferediobase/io.bufferediobase.write) - записывает байтовый объект и возвращает количество записанных байтов




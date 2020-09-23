# io.IOBase

### _class_ io.IOBase

Абстрактный базовый класс для всех классов ввода-вывода, воздействующий на потоки байтов. Общедоступного конструктора нет.

Этот класс предоставляет пустые абстрактные реализации для многих методов, которые производные классы могут выборочно переопределять; реализации по умолчанию представляют собой файл, который нельзя прочитать, записать или найти.

Несмотря на то, что **IOBase** не объявляет read \(\) или write \(\), поскольку их сигнатуры будут различаться, реализации и клиенты должны рассматривать эти методы как часть интерфейса. Кроме того, реализации могут вызывать ошибку ValueError \(или UnsupportedOperation\), когда вызываются операции, которые они не поддерживают.

Базовый тип, используемый для двоичных данных, считываемых из файла или записываемых в файл, - это байты. Другие байтовые объекты \(_bytes-like object_ \) также принимаются в качестве аргументов метода. Классы текстового ввода-вывода [Text I/O](../io.textiobase/) работают с данными типа str.

Обратите внимание, что вызов любого метода \(даже запросов\) в закрытом потоке не определен. В этом случае реализации могут вызвать ошибку ValueError.

**IOBase** \(и его подклассы\) поддерживают протокол итератора, что означает, что объект **IOBase** может быть повторен, давая строки в потоке. Строки определяются немного по-разному, в зависимости от того, является ли поток двоичным потоком \(дающим байты\) или текстовым потоком \(дающим строки символов\). См. readline \(\) ниже.

**IOBase** также является диспетчером контекста и поэтому поддерживает оператор with. В этом примере файл закрывается после завершения набора операторов with, даже если возникает исключение:

```python
with open('spam.txt', 'w') as file:
    file.write('Spam and eggs!')
```

**IOBase** предоставляет следующие атрибуты и методы данных:

* [close \(\)](io.iobase.close.md) - выталкивает и закрывает поток
* closed
* [fileno \(\)](io.iobase.fileno.md) - возвращает базовый файловый дескриптор
* [flush \(\)](io.iobase.flush.md) - выталкивает содержимое буфера для записи в поток
* [isatty \(\)](io.iobase.isatty.md) - поток подключен к терминалу?
* readable \(\)
* [readline \(\)](io.iobase.readline.md) - читает и возвращает одну строку из потока
* [readlines \(\)](io.iobase.readlines.md) - читает и возвращает список строк из потока
* [seek \(\)](io.iobase.seek.md) - изменяет позицию потока на заданное смещение
* seekable \(\)
* tell \(\)
* truncate \(\)
* writable \(\)
* [writelines \(\)](io.iobase.writelines.md) - записывает список строк в поток
* \_\_del\_\_ \(\)

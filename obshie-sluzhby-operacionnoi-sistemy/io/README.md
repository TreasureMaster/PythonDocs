# io

### io - основные инструменты для работы с потоками

#### Обзор

Модуль **io** предоставляет основные возможности Python для работы с различными типами ввода-вывода. Существует три основных типа ввода-вывода: _**text I/O**_ \(текстовый ввод-вывод\), _**binary I/O**_ \(двоичный ввод-вывод\) и _**raw I/O**_ \(необработанный ввод-вывод\). Это общие категории, и для каждой из них можно использовать различные резервные хранилища. Конкретный объект, принадлежащий к любой из этих категорий, называется файловым объектом. Другие общие термины - поток _**stream**_ и файловый объект _**file-like object**_.

Независимо от своей категории, каждый конкретный объект потока также будет иметь различные возможности: он может быть доступен только для чтения, только для записи или чтения-записи. Он также может разрешать произвольный произвольный доступ \(поиск вперед или назад в любое место\) или только последовательный доступ \(например, в случае сокета или канала\).

Все потоки бережно относятся к типу данных, которые вы им предоставляете. Например, передача объекта str методу `write ()` двоичного потока вызовет ошибку TypeError. Таким образом, мы передадим объект bytes методу `write ()` текстового потока.

_Изменено в версии 3.3:_ операции, которые раньше вызывали IOError, теперь вызывают OSError, поскольку IOError теперь является псевдонимом OSError.

#### Text I/O \(текстовый ввод-вывод\)

#### Binary I/O \(двоичный ввод-вывод\)

#### Raw I/O \(необработанный ввод-вывод\)

#### [Высокоуровневый интерфейс модуля](vysokourovnevyi-interfeis-modulya/)

* [io.DEFAULT\_BUFFER\_SIZE](vysokourovnevyi-interfeis-modulya/io.default_buffer_size.md) - размер буфера по умолчанию
* не заполнено...

#### Иерархия классов

#### Базовые классы ввода-вывода

* [io.**IOBase**](io.iobase/) class - абстрактный базовый класс для всех классов ввода-вывода
  * [close \(\)](io.iobase/io.iobase.close.md) - выталкивает и закрывает поток
  * closed
  * [fileno \(\)](io.iobase/io.iobase.fileno.md) - возвращает базовый файловый дескриптор
  * [flush \(\)](io.iobase/io.iobase.flush.md) - выталкивает содержимое буфера для записи в поток
  * [isatty \(\)](io.iobase/io.iobase.isatty.md) - поток подключен к терминалу?
  * readable \(\)
  * [readline \(\)](io.iobase/io.iobase.readline.md) - читает и возвращает одну строку из потока
  * [readlines \(\)](io.iobase/io.iobase.readlines.md) - читает и возвращает список строк из потока
  * [seek \(\)](io.iobase/io.iobase.seek.md) - изменяет позицию потока на заданное смещение
  * seekable \(\)
  * tell \(\)
  * truncate \(\)
  * writable \(\)
  * [writelines \(\)](io.iobase/io.iobase.writelines.md) - записывает список строк в поток
  * \_\_del\_\_ \(\)
* [io.**RawIOBase**](io.rawiobase/) class
  * [read \(\)](io.rawiobase/io.rawiobase.read.md) - читает заданное количество байтов из объекта и возвращает их
  * [readall \(\)](io.rawiobase/io.rawiobase.readall.md) - читает и возвращает все байты из потока
  * [readinto \(\)](io.rawiobase/io.rawiobase.readinto.md) - считывает байты в заданный объект и возвращает их количество
  * [write \(\)](io.rawiobase/io.rawiobase.write.md) - записывает байтовый объект в необработанный поток и возвращает количество записанных байтов
* [io.**BufferedIOBase**](io.bufferediobase/) class - базовый класс для двоичных потоков, поддерживающих буферизацию
  * raw
  * detach \(\)
  * [read \(\)](io.bufferediobase/io.bufferediobase.read.md) - читает и возвращает байты
  * read1 \(\)
  * readinto \(\)
  * readinto1 \(\)
  * [write \(\)](io.bufferediobase/io.bufferediobase.write.md) - записывает байтовый объект и возвращает количество записанных байтов

#### Ввод-вывод необработанных файлов

* io.**FileIO** class

#### Буферизованные потоки

Буферизованные потоки ввода-вывода обеспечивают интерфейс более высокого уровня для устройства ввода-вывода, чем необработанный ввод-вывод.

* [io.**BytesIO**](io.bytesio/) class - реализация потока с использованием байтового буфера в памяти
  * getbuffer \(\)
  * [getvalue \(\)](io.bytesio/io.bytesio.getvalue.md) - возвращает все байты, содержащиеся в буфере
  * read1 \(\)
  * readinto1 \(\)
* [io.**BufferedReader**](io.bufferedreader/) class
  * peek \(\)
  * [read \(\)](io.bufferedreader/io.bufferedreader.read.md) - читает и возвращает количество байтов заданного размера
  * read1 \(\)
* [io.**BufferedWriter**](io.bufferedwriter/) class
  * [flush \(\)](io.bufferedwriter/io.bufferedwriter.flush.md) - переводит байты, хранящиеся в буфере в необработанный поток
  * [write \(\)](io.bufferedwriter/io.bufferedwriter.write.md) - записывает байтовый поток и возвращает количество записанных байтов
* io.**BufferedRandom** class
* io.**BufferedRWPair** class

#### Текстовый ввод-вывод \(Text I/O\)

* [io.**TextIOBase**](io.textiobase/) class - базовый класс для текстовых потоков
  * encoding
  * errors
  * newlines
  * buffer
  * detach \(\)
  * [read \(\)](io.textiobase/io.textiobase.read.md) - читает и возвращает заданное количество символов из строки \(или весь текст\)
  * [readline \(\)](io.textiobase/io.textiobase.readline.md) - читает до новой строки или EOF и возвращает одну строку
  * [seek \(\)](io.textiobase/io.textiobase.seek.md) - меняет положение указателя потока на заданное смещение
  * tell \(\)
  * [write \(\)](io.textiobase/io.textiobase.write.md) - пишет строку в поток и возвращает количество записанных символов
* io.**TextIOWrapper** class
  * line\_buffering
  * write\_through
  * reconfigure \(\)
* [io.**StringIO**](io.stringio/) class - поток в памяти для текстового ввода-вывода
  * [getvalue \(\)](io.stringio/io.stringio.getvalue.md) - метод возвращает строку, содержащую все содержимое буфера
* io.**IncrementalNewlineDecoder** class


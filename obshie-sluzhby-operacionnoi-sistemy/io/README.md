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

#### Интерфейс модуля высокого уровня

#### Иерархия классов

#### Базовые классы ввода-вывода

* io.**IOBase** class - абстрактный базовый класс для всех классов ввода-вывода
  * close \(\)
  * не заполнено...
  * \_\_del\_\_ \(\)
* io.**RawIOBase** class
* [io.**BufferedIOBase**](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bufferediobase) class - базовый класс для двоичных потоков, поддерживающих буферизацию
  * raw
  * detach \(\)
  * [read \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bufferediobase/io.bufferediobase.read) - читает и возвращает байты
  * read1 \(\)
  * readinto \(\)
  * readinto1 \(\)
  * [write \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bufferediobase/io.bufferediobase.write) - записывает байтовый объект и возвращает количество записанных байтов

#### Ввод-вывод необработанных файлов

* io.**FileIO** class

#### Буферизованные потоки

Буферизованные потоки ввода-вывода обеспечивают интерфейс более высокого уровня для устройства ввода-вывода, чем необработанный ввод-вывод.

* io.**BytesIO** class - реализация потока с использованием байтового буфера в памяти
  * getbuffer \(\)
  * [getvalue \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bytesio/io.bytesio.getvalue) - возвращает все байты, содержащиеся в буфере
  * read1 \(\)
  * readinto1 \(\)
* io.**BufferedReader** class
* io.**BufferedWriter** class
* io.**BufferedRandom** class
* io.**BufferedRWPair** class

#### Текстовый ввод-вывод \(Text I/O\)

* [io.**TextIOBase**](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.textiobase) class - базовый класс для текстовых потоков
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
* io.**TextIOWrapper** class
* [io.**StringIO**](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.stringio) class - поток в памяти для текстового ввода-вывода
  * [getvalue \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.stringio/io.stringio.getvalue) - метод возвращает строку, содержащую все содержимое буфера
* io.**IncrementalNewlineDecoder** class


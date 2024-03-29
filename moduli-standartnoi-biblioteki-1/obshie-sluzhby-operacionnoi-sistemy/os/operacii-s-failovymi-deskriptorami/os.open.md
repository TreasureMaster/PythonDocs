# os.open ()

### os.open ( _path_, _flags_, _mode=0o777_, _\*_, _dir\_fd=None _)

Открывает путь _**path**_ к файлу и устанавливает различные флаги в соответствии с _**flags**_ и, возможно, его режим в соответствии с _**mode**_. Когда _**mode**_ вычисляется, текущее значение umask сначала маскируется. Возвращает файловый дескриптор для вновь открытого файла. Новый дескриптор файла не наследуется.

Описание значений _**flags**_ и _**mode**_ см. в документации среды выполнения C; константы флагов (например, O\_RDONLY и O\_WRONLY) определены в модуле os. В частности, в Windows добавление O\_BINARY необходимо для открытия файлов в двоичном режиме.

Эта функция может поддерживать пути относительно дескрипторов каталогов с параметром _**dir\_fd**_.

Вызывает событие аудита, открытое с аргументами `path`, `mode`, `flags`.

_Изменено в версии 3.4:_ новый дескриптор файла теперь не наследуется.

{% hint style="info" %}
Эта функция предназначена для ввода/вывода низкого уровня. Для нормального использования используйте встроенную функцию [open ()](../../../../vstroennye-obekty/vstroennye-funkcii/open.md), которая возвращает объект файла с помощью методов `read ()` и `write ()` (и многих других). Чтобы обернуть файловый дескриптор в файловый объект, используйте [fdopen ()](../sozdanie-failovogo-obekta/os.fdopen.md).
{% endhint %}

_Новое в версии 3.3:_ аргумент _**dir\_fd**_.

_Изменено в версии 3.5:_ если системный вызов прерывается и обработчик сигнала не вызывает исключения, функция теперь повторяет системный вызов вместо того, чтобы вызывать исключение InterruptedError (объяснение см. в [PEP 475](https://www.python.org/dev/peps/pep-0475/)).

_Изменено в версии 3.6:_ Принимает объект, подобный пути (_path-like object _).

Следующие константы являются опциями для параметра _**flags**_ функции [open ()](os.open.md). Их можно объединить с помощью побитового оператора ИЛИ `|`. Некоторые из них доступны не на всех платформах. За описанием их доступности и использования обратитесь к странице руководства [open (2)](https://manpages.debian.org/buster/manpages-dev/open.2.en.html) в Unix или в [MSDN](https://docs.microsoft.com/en-us/cpp/c-runtime-library/reference/open-wopen?redirectedfrom=MSDN\&view=vs-2019) в Windows.

#### Эти константы доступны в Unix и Windows:

* **os.O\_RDONLY**  - открыть файл только для чтения
* **os.O\_WRONLY** - открыть файл только для записи
* **os.O\_RDWR**     - открыть файл для чтения и записи
* **os.O\_APPEND** - открыть файл в режиме добавления
* **os.O\_CREAT**    - создает файл и открывает его для записи
* **os.O\_EXCL**       - разрешает создание файла, только если он не существует
* **os.O\_TRUNC**   - открывает файл и обрезает его до нулевой длины

#### Константы, доступные только в Unix:

* os.O\_DSYNC&#x20;
* os.O\_RSYNC&#x20;
* os.O\_SYNC&#x20;
* **os.O\_NDELAY** - по возможности открывает файл в неблокирующем режиме (синоним)
* **os.O\_NONBLOCK** - по возможности открывает файл в неблокирующем режиме (синоним)
* **os.O\_NOCTTY** - процесс не станет управляющим терминалом процесса (даже если терминальное устройство tty присутствует в команде)
* **os.O\_CLOEXEC** - включает флаг закрытия при запуске нового дескриптора файла

_Изменено в версии 3.3:_ Добавлена константа **O\_CLOEXEC**.

#### Константы, доступные только в Windows:

* **os.O\_BINARY** - открывает файл в двоичном режиме
* **os.O\_NOINHERIT** - предотвращает создание общего файлового дескриптора
* **os.O\_SHORT\_LIVED** - создает файл как временный и по возможности не сбрасывает на диск
* **os.O\_TEMPORARY** - создает файл как временный, файл удаляется при закрытии дескриптора
* **os.O\_RANDOM** - кеширование оптимизировано для произвольного доступа с диска
* **os.O\_SEQUENTIAL** - кеширование оптимизировано для последовательного доступа с диска
* **os.O\_TEXT** - открывает файл в текстовом режиме

#### Эти константы являются расширениями и отсутствуют, если они не определены библиотекой C:

* os.O\_ASYNC&#x20;
* os.O\_DIRECT&#x20;
* os.O\_DIRECTORY&#x20;
* os.O\_NOFOLLOW&#x20;
* os.O\_NOATIME&#x20;
* os.O\_PATH&#x20;
* os.O\_TMPFILE&#x20;
* os.O\_SHLOCK&#x20;
* os.O\_EXLOCK

_Изменено в версии 3.4:_ Добавлен **O\_PATH** в системах, которые его поддерживают. Добавлен **O\_TMPFILE**, доступный только в Linux Kernel 3.11 или новее.

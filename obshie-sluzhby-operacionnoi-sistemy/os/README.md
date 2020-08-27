# os

Этот модуль обеспечивает переносимый способ использования функций, зависящих от операционной системы. Если вы просто хотите прочитать или записать файл, см. open\( \), если вы хотите манипулировать путями, см. модуль [os.path](https://treasuremaster.gitbook.io/python-docs/dostup-k-failam-i-papkam/os.path), а если вы хотите прочитать все строки во всех файлах в командной строке, см. модуль fileinput . Для создания временных файлов и каталогов см. модуль tempfile, а для высокоуровневой обработки файлов и каталогов см. модуль shutil.

{% hint style="info" %}
Примечание о доступности функций:

* Дизайн всех встроенных модулей Python, зависящих от операционной системы, таков, что, пока доступна одна и та же функциональность, он использует один и тот же интерфейс; например, функция os.stat \(path\) возвращает статистическую информацию о пути в том же формате \(который, как оказалось, возник из интерфейса POSIX\).
* Расширения, характерные для конкретной операционной системы, также доступны через модуль os, но их использование, конечно, угрожает переносимости.
* Все функции, принимающие путь или имена файлов, принимают как байтовые, так и строковые объекты и приводят к объекту того же типа, если возвращается путь или имя файла.
* В VxWorks os.fork, os.execv и os.spawn\*p\* __ не поддерживаются.
{% endhint %}

{% hint style="warning" %}
Все функции в этом модуле вызывают ошибку OSError \(или ее подклассы\) в случае недопустимых или недоступных имен файлов и путей или других аргументов, которые имеют правильный тип, но не принимаются операционной системой.
{% endhint %}

#### не заполнено...

### Имена файлов, аргументы командной строки и переменные среды

не заполнено...

#### Параметры процесса

Эти функции и элементы данных предоставляют информацию и работают с текущим процессом и пользователем.

* os.ctermid \(\)
* [os.environ](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/environ) - словарь переменных окружения
* не заполнено...
* [os.getcwd \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/getcwd) - функция описана ниже
* не заполнено...
* os.PathLike class
* [os.getenv \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.getenv) - возвращает значение ключа переменной среды
* не заполнено...
* [os.getpid \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.getpid) - возвращает текущий идентификатор процесса
* не заполнено...
* [os.putenv \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.putenv) - задает значение ключа для переменной среды

#### Создание файлового объекта

Эти функции создают новые файловые объекты. \(см. также open \(\) для открытия файловых дескрипторов.\)

* os.fdopen \(\)

#### Операции с файловым дескриптором

Эти функции работают с потоками ввода-вывода, на которые ссылаются файловые дескрипторы.

Дескрипторы файлов - это небольшие целые числа, соответствующие файлу, который был открыт текущим процессом. Например, стандартный ввод - это дескриптор файла 0, стандартный вывод - 1, а стандартная ошибка - 2. Далее файлам, открытым процессом, будут присвоены 3, 4, 5 и т. д. Название «файловый дескриптор» немного обманчиво; на платформах Unix на сокеты и каналы также ссылаются файловые дескрипторы.

При необходимости метод fileno \(\) может использоваться для получения дескриптора файла, связанного с файловым объектом. Обратите внимание, что использование файлового дескриптора напрямую приведет к обходу методов файлового объекта, игнорируя такие аспекты, как внутренняя буферизация данных.

* [os.close \(\)](operacii-s-failovymi-deskriptorami/os.close.md) - закрывает файловый дескриптор
* не заполнено...
* [os.isatty \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.isatty) - открыт ли файловый дескриптор и подключен к tty?
* os.lockf \(\)
* os.F\_LOCK
* os.F\_TLOCK
* os.F\_ULOCK
* os.F\_TEST
* [os.lseek \(\)](operacii-s-failovymi-deskriptorami/os.lseek.md) - устанавливает текущую позицию файлового дескриптора
* [os.SEEK\_SET](operacii-s-failovymi-deskriptorami/os.seek_set.md) - параметр функции os.lseek \(\)
* [os.SEEK\_CUR](operacii-s-failovymi-deskriptorami/os.seek_cur.md) - параметр функции os.lseek \(\)
* [os.SEEK\_END](operacii-s-failovymi-deskriptorami/os.seek_end.md) - параметр функции os.lseek \(\)
* [os.open \(\)](operacii-s-failovymi-deskriptorami/os.open.md) - открывает файл
* os.O\_RDONLY
* os.O\_WRONLY
* os.O\_RDWR
* os.O\_APPEND
* os.O\_CREAT
* os.O\_EXCL
* os.O\_TRUNC
* не заполнено...
* os.O\_NONBLOCK
* os.\_NOCTTY
* os.O\_CLOEXEC
* os.O\_BINARY
* не заполнено...
* os.pipe \(\)
* не заполнено...
* [os.read \(\)](operacii-s-failovymi-deskriptorami/os.read.md) - читает байты из файлового дескриптора
* не заполнено...
* [os.write \(\)](operacii-s-failovymi-deskriptorami/os.write.md)
* os.writev \(\)

#### Файлы и директории

На некоторых платформах Unix многие из этих функций поддерживают одну или несколько из следующих возможностей:

* не заполнено...
* не заполнено...
* не заполнено...

Описание функций для использования с файлами и директориями:

* os.access \(\)
* не заполнено...
* os.chmod \(\)
* os.chown \(\)
* os.chroot \(\)
* os.fchdir \(\)
* [os.getcwd \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/getcwd) - возвращает текущий рабочий каталог
* не заполнено...
* os.remove \(\)
* os.removedirs \(\)
* os.rename \(\)
* os.renames \(\)
* os.replace \(\)
* os.rmdir \(\)
* os.scandir \(\)
* os.DirEntry class
* os.stat \(\)
* не заполнено...
* os.unlink \(\)
* os.utime \(\)
* os.walk \(\)
* os.fwalk \(\)
* os.memfd\_create \(\)
* не заполнено...

#### Управление процессами

Эти функции могут использоваться для создания процессов и управления ими.

Различные функции exec\* принимают список аргументов для новой программы, загруженной в процесс. В каждом случае первый из этих аргументов передается новой программе как ее собственное имя, а не как аргумент, который пользователь мог ввести в командной строке. Для программиста на C это `argv[0]`, переданный в main \(\) программы. Например, `os.execv ('/bin/echo', ['foo', 'bar'])` будет печатать только `bar` на стандартном выводе; `foo` будет казаться проигнорированным.

* os.abort \(\)
* не заполнено...
* [os.popen \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.popen) - открывает канал команды исполнения оболочки shell
* не заполнено...
* [os.startfile \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.startfile) - запускает файл с помощью связанного с ним приложения
* [os.system \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.system) - исполняет команду \(строку\) в новой оболочке shell
* не заполнено...

#### Интерфейс планировщика

#### Разные службы операционной системы

* os.confstr \(\)
* не заполнено...
* os.sysconf\_names

Следующие значения данных используются для поддержки операций манипулирования путями. Они определены для всех платформ. Операции более высокого уровня с именами путей определены в модуле os.path.

* [os.curdir](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.curdir) - строка, используемая операционной системой для ссылки на текущий каталог
* [os.pardir](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.pardir) - строка, используемая операционной системой для ссылки на родительский каталог
* [os.sep](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.sep) - символ, используемый операционной системой для разделения компонентов пути
* os.altsep
* os.extsep
* [os.pathsep](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/pathsep) - символ разделения компонентов пути поиска в операционной системе
* os.defpath
* [os.linesep](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.linesep) - строка, используемая для разделения \(завершения\) строк на текущей платформе
* os.devnull
* не заполнено...

#### Случайные числа


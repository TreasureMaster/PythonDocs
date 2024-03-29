# os

Этот модуль обеспечивает переносимый способ использования функций, зависящих от операционной системы. Если вы просто хотите прочитать или записать файл, см. [open( )](../../../vstroennye-obekty/vstroennye-funkcii/open.md), если вы хотите манипулировать путями, см. модуль [os.path](../../dostup-k-failam-i-papkam/os.path/), а если вы хотите прочитать все строки во всех файлах в командной строке, см. модуль [fileinput](../../dostup-k-failam-i-papkam/fileinput.md) . Для создания временных файлов и каталогов см. модуль [tempfile](../../dostup-k-failam-i-papkam/tempfile.md), а для высокоуровневой обработки файлов и каталогов см. модуль [shutil](../../dostup-k-failam-i-papkam/shutil/).

{% hint style="info" %}
Примечание о доступности функций:

* Дизайн всех встроенных модулей Python, зависящих от операционной системы, таков, что, пока доступна одна и та же функциональность, он использует один и тот же интерфейс; например, функция `os.stat (path)` возвращает статистическую информацию о пути в том же формате (который, как оказалось, возник из интерфейса POSIX).
* Расширения, характерные для конкретной операционной системы, также доступны через модуль os, но их использование, конечно, угрожает переносимости.
* Все функции, принимающие путь или имена файлов, принимают как байтовые, так и строковые объекты и приводят к объекту того же типа, если возвращается путь или имя файла.
* В VxWorks os.fork, os.execv и os.spawn\*p\*_ _ не поддерживаются.
{% endhint %}

{% hint style="warning" %}
Все функции в этом модуле вызывают ошибку OSError (или ее подклассы) в случае недопустимых или недоступных имен файлов и путей или других аргументов, которые имеют правильный тип, но не принимаются операционной системой.
{% endhint %}

* os.error exception
* os.name ()

### Имена файлов, аргументы командной строки и переменные среды

не заполнено...

### [Параметры процесса](parametry-processa/)

Эти функции и элементы данных предоставляют информацию и работают с текущим процессом и пользователем.

* os.ctermid ()
* [os.environ](parametry-processa/environ.md) - словарь переменных окружения
* os.environb
* [os.chdir ()](./#faily-i-direktorii) - функция описана ниже
* os.fchdir ()
* [os.getcwd ()](./#faily-i-direktorii) - функция описана ниже
* os.fsencode ()
* os.fsdecode ()
* os.fspath ()
* os.PathLike class
* [os.getenv ()](parametry-processa/os.getenv.md) - возвращает значение ключа переменной среды
* os.getenvb ()
* не заполнено...
* [os.getpid ()](parametry-processa/os.getpid.md) - возвращает текущий идентификатор процесса
* [os.getppid ()](parametry-processa/os.getppid.md) - возвращает идентификатор родительского процесса
* не заполнено...
* [os.putenv ()](parametry-processa/os.putenv.md) - задает значение ключа для переменной среды
* не заполнено...
* os.uname ()
* os.unsetenv ()

### [Создание файлового объекта](sozdanie-failovogo-obekta/)

Эти функции создают новые файловые объекты. (см. также [os.open ()](operacii-s-failovymi-deskriptorami/os.open.md) для открытия файловых дескрипторов.)

* [os.fdopen ()](sozdanie-failovogo-obekta/os.fdopen.md) - возвращает файловый объект, связанный с файловым дескриптором

### [Операции с файловым дескрипторами](operacii-s-failovymi-deskriptorami/)

Эти функции работают с потоками ввода-вывода, на которые ссылаются файловые дескрипторы.

Дескрипторы файлов - это небольшие целые числа, соответствующие файлу, который был открыт текущим процессом. Например, стандартный ввод - это дескриптор файла 0, стандартный вывод - 1, а стандартная ошибка - 2. Далее файлам, открытым процессом, будут присвоены 3, 4, 5 и т. д. Название «файловый дескриптор» немного обманчиво; на платформах Unix на сокеты и каналы также ссылаются файловые дескрипторы.

При необходимости метод fileno () может использоваться для получения дескриптора файла, связанного с файловым объектом. Обратите внимание, что использование файлового дескриптора напрямую приведет к обходу методов файлового объекта, игнорируя такие аспекты, как внутренняя буферизация данных.

* [os.close ()](operacii-s-failovymi-deskriptorami/os.close.md) - закрывает файловый дескриптор
* os.closerange ()
* os.\_copy\_file\_range ()
* os.device\_encoding ()
* os.dup ()
* [os.dup2 ()](operacii-s-failovymi-deskriptorami/os.dup2.md) - копирует один файловый дескриптор в другой
* не заполнено...
* os.fstat ()
* os.fstatvfs ()
* os.fsync ()
* не заполнено...
* [os.isatty ()](operacii-s-failovymi-deskriptorami/os.isatty.md) - открыт ли файловый дескриптор и подключен к tty?
* os.lockf ()
* os.F\_LOCK
* os.F\_TLOCK
* os.F\_ULOCK
* os.F\_TEST
* [os.lseek ()](operacii-s-failovymi-deskriptorami/os.lseek.md) - устанавливает текущую позицию файлового дескриптора
* [os.SEEK\_SET](operacii-s-failovymi-deskriptorami/os.seek\_set.md) - параметр функции os.lseek ()
* [os.SEEK\_CUR](operacii-s-failovymi-deskriptorami/os.seek\_cur.md) - параметр функции os.lseek ()
* [os.SEEK\_END](operacii-s-failovymi-deskriptorami/os.seek\_end.md) - параметр функции os.lseek ()
* [os.open ()](operacii-s-failovymi-deskriptorami/os.open.md) - открывает файл
* os.openpty ()
* не заполнено...
* [os.pipe ()](operacii-s-failovymi-deskriptorami/os.pipe.md) - создает канал и возвращает пару файловых дескрипторов
* не заполнено...
* [os.read ()](operacii-s-failovymi-deskriptorami/os.read.md) - читает байты из файлового дескриптора
* не заполнено...
* [os.write ()](operacii-s-failovymi-deskriptorami/os.write.md) - записывает байтовую строку в файловый дескриптор
* os.writev ()

### [Файлы и директории](faily-i-direktorii/)

На некоторых платформах Unix многие из этих функций поддерживают одну или несколько из следующих возможностей:

* **указание дескриптора файла:** Обычно аргумент пути _**path**_, предоставляемый функциям в модуле os, должен быть строкой, определяющей путь к файлу. Однако некоторые функции теперь альтернативно принимают дескриптор открытого файла в качестве аргумента _**path**_. Затем функция будет работать с файлом, на который ссылается дескриптор. (Для систем POSIX Python вызовет вариант функции с префиксом `f` (например, вызовет `fchdir` вместо `chdir`).) Вы можете проверить, можно ли указать _**path**_ как файловый дескриптор для конкретной функции на вашей платформе, используя [os.supports\_fd](faily-i-direktorii/os.supports\_fd.md). Если эта функция недоступна, ее использование вызовет NotImplementedError. Если функция также поддерживает аргументы _**dir\_fd**_ или _**follow\_symlinks**_, указывать один из них при указании пути в качестве дескриптора файла является ошибкой.
* **пути относительно дескрипторов каталогов:** если _**dir\_fd**_ не равно `None`, это должен быть дескриптор файла, ссылающийся на каталог, а путь для работы должен быть относительным; тогда путь будет относиться к этому каталогу. Если путь абсолютный, _**dir\_fd**_ игнорируется. (Для систем POSIX Python вызовет вариант функции с суффиксом `at` и, возможно, с префиксом `f` (например, вызов `faccessat` вместо `access`). Вы можете проверить, поддерживается ли _**dir\_fd**_ для конкретной функции на вашей платформе, используя [os.supports\_dir\_fd](faily-i-direktorii/os.supports\_dir\_fd.md). Если он недоступен, его использование вызовет NotImplementedError.
* **не следовать символическим ссылкам:** если _**follow\_symlinks**_ имеет значение `False`, а последний элемент пути для работы является символической ссылкой, функция будет работать с самой символической ссылкой, а не с файлом, на который указывает ссылка. (Для систем POSIX Python вызовет `l...` вариант функции.). Вы можете проверить, поддерживается ли _**follow\_symlinks**_ для конкретной функции на вашей платформе, используя [os.supports\_follow\_symlinks](faily-i-direktorii/os.supports\_follow\_symlinks.md). Если он недоступен, его использование вызовет NotImplementedError.

Описание функций для использования с файлами и директориями:

* os.access ()
* не заполнено...
* [os.chdir ()](faily-i-direktorii/os.chdir.md) - изменяет текущую рабочую директорию на заданную
* os.chflags ()
* [os.chmod ()](faily-i-direktorii/os.chmod.md) - изменяет режим доступа к файлу
* [os.chown ()](faily-i-direktorii/os.chown.md) - изменяет идентификатор владельца/группы файла
* os.chroot ()
* os.fchdir ()
* [os.getcwd ()](faily-i-direktorii/getcwd.md) - возвращает текущий рабочий каталог
* os.getcwdb ()
* os.lchflags ()
* os.lchmod ()
* os.lchown ()
* os.link ()
* [os.listdir ()](faily-i-direktorii/os.listdir.md) - возвращает список, содержащий имена записей в каталоге
* os.lstat ()
* os.mkdir ()
* os.makedirs ()
* [os.mkfifo ()](faily-i-direktorii/os.mkfifo.md) - создает именованный канал в заданном режиме
* не заполнено...
* [os.remove ()](faily-i-direktorii/os.remove.md) - удаляет файл или каталог по заданному пути (синоним unlink () )
* os.removedirs ()
* [os.rename ()](faily-i-direktorii/os.rename.md) - переименовывает файл или каталог
* os.renames ()
* os.replace ()
* os.rmdir ()
* os.scandir ()
* os.DirEntry class
* [os.stat ()](faily-i-direktorii/os.stat.md) - получает статистическую информацию о файле
* [os.stat\_result class](faily-i-direktorii/os.stat\_result.md) - объект, атрибуты которого примерно соответствуют членам stat
* os.statvfs ()
* os.supports\_dir\_fd
* os.supports\_effective\_ids
* os.supports\_fd
* os.supports\_follow\_symlinks
* не заполнено...
* [os.unlink ()](faily-i-direktorii/os.unlink.md) - удаляет файл или каталог по заданному пути (синоним remove () )
* os.utime ()
* [os.walk ()](faily-i-direktorii/os.walk.md) - возвращает список файлов/подкаталогов рекурсивного обхода каталога
* os.fwalk ()
* os.memfd\_create ()
* не заполнено...

### [Управление процессами](upravlenie-processami/)

Эти функции могут использоваться для создания процессов и управления ими.

Различные функции exec\* принимают список аргументов для новой программы, загруженной в процесс. В каждом случае первый из этих аргументов передается новой программе как ее собственное имя, а не как аргумент, который пользователь мог ввести в командной строке. Для программиста на C это `argv[0]`, переданный в main () программы. Например, `os.execv ('/bin/echo', ['foo', 'bar'])` будет печатать только `bar` на стандартном выводе; `foo` будет казаться проигнорированным.

* os.abort ()
* os.add\_dll\_directory ()
* [os.execl ()](upravlenie-processami/os.execl.md) - запускает новый процесс, заменяя текущий
* [os.execle ()](upravlenie-processami/os.execle.md) - запускает новый процесс, заменяя текущий
* [os.execlp ()](upravlenie-processami/os.execlp.md) - запускает новый процесс, заменяя текущий
* [os.execlpe ()](upravlenie-processami/os.execlpe.md) - запускает новый процесс, заменяя текущий
* [os.execv ()](upravlenie-processami/os.execv.md) - запускает новый процесс, заменяя текущий
* [os.execve ()](upravlenie-processami/os.execve.md) - запускает новый процесс, заменяя текущий
* [os.execvp ()](upravlenie-processami/os.execvp.md) - запускает новый процесс, заменяя текущий
* [os.execvpe ()](upravlenie-processami/os.execvpe.md) - запускает новый процесс, заменяя текущий
* [os.\_exit ()](upravlenie-processami/os.\_exit.md) - выходит из процесса с переданным статусом
* [os.fork ()](upravlenie-processami/os.fork.md) - ответвляет дочерние процессы
* os.forkpty ()
* [os.kill ()](upravlenie-processami/os.kill.md) - отправляет сигнал процессу, определенному идентификатором
* os.killpg ()
* os.nice ()
* os.plock ()
* [os.popen ()](upravlenie-processami/os.popen.md) - открывает канал команды исполнения оболочки shell
* не заполнено...
* [os.startfile ()](upravlenie-processami/os.startfile.md) - запускает файл с помощью связанного с ним приложения
* [os.system ()](upravlenie-processami/os.system.md) - исполняет команду (строку) в новой оболочке shell
* не заполнено...
* [os.waitpid ()](upravlenie-processami/os.waitpid.md) - дождаться завершения процесса, заданного идентификатором
* не заполнено...
* [os.WNOHANG](upravlenie-processami/os.wnohang.md) - немедленный возврат из **waitpid()**, если процесс недоступен
* не заполнено...

#### Интерфейс планировщика

### [Разные службы операционной системы](raznye-sluzhby-os/)

* os.confstr ()
* не заполнено...
* os.sysconf\_names

Следующие значения данных используются для поддержки операций манипулирования путями. Они определены для всех платформ. Операции более высокого уровня с именами путей определены в модуле os.path.

* [os.curdir](raznye-sluzhby-os/os.curdir.md) - строка, используемая операционной системой для ссылки на текущий каталог
* [os.pardir](raznye-sluzhby-os/os.pardir.md) - строка, используемая операционной системой для ссылки на родительский каталог
* [os.sep](raznye-sluzhby-os/os.sep.md) - символ, используемый операционной системой для разделения компонентов пути
* os.altsep
* os.extsep
* [os.pathsep](raznye-sluzhby-os/pathsep.md) - символ разделения компонентов пути поиска в переменной окружения ОС
* os.defpath
* [os.linesep](raznye-sluzhby-os/os.linesep.md) - строка, используемая для разделения (завершения) строк на текущей платформе
* os.devnull
* не заполнено...

#### Случайные числа

# os.stat\_result

### _class_ os.stat\_result

Объект, атрибуты которого примерно соответствуют членам структуры `stat`. Он используется для результатов[ os.stat \(\)](os.stat.md), [os.fstat \(\)](../operacii-s-failovymi-deskriptorami/os.fstat.md) и [os.lstat \(\)](os.lstat.md).

#### Атрибуты:

* **st\_mode** - режим файла: тип файла и биты режима файла \(разрешения\)
* **st\_ino** - зависит от платформы, но если не равен нулю, однозначно идентифицирует файл для данного значения **st\_dev**. Обычно:
  * номер _**inode**_ в Unix
  * индекс файла в Windows
* **st\_dev** - идентификатор устройства, на котором находится этот файл
* **st\_nlink** - количество жестких ссылок
* **st\_uid** - идентификатор пользователя владельца файла
* **st\_gid** - идентификатор группы владельца файла
* **st\_size** - размер файла в байтах, если это обычный файл или символическая ссылка. Размер символической ссылки - это длина содержащегося в ней имени пути без завершающего нулевого байта.

#### Отметки времени:

* **st\_atime** - время последнего доступа в секундах
* **st\_mtime** - время последнего изменения содержимого в секундах
* **st\_ctime** - в зависимости от платформы:
  * время последнего изменения метаданных в Unix
  * время создания в Windows, выраженное в секундах
* **st\_atime\_ns** - время последнего доступа, выраженное в наносекундах в виде целого числа
* **st\_mtime\_ns** - время последней модификации содержимого, выраженное в наносекундах в виде целого числа
* **st\_ctime\_ns** - в зависимости от платформы:
  * время последнего изменения метаданных в Unix
  * время создания в Windows, выраженное в наносекундах в виде целого числа

{% hint style="info" %}
Точное значение и разрешение атрибутов **st\_atime**, **st\_mtime** и **st\_ctime** зависят от операционной системы и файловой системы. Например, в системах Windows, использующих файловые системы FAT или FAT32, **st\_mtime** имеет разрешение 2 секунды, а **st\_atime** имеет разрешение только 1 день. Подробности см. в документации по вашей операционной системе.

Точно так же и для наносекундных атрибутов, хотя **st\_atime\_ns**, **st\_mtime\_ns** и **st\_ctime\_ns** всегда выражаются в наносекундах, многие системы не обеспечивают наносекундную точность. В системах, которые обеспечивают точность до наносекунд, объект с плавающей запятой, используемый для хранения **st\_atime**, **st\_mtime** и **st\_ctime**, не может сохранить все это, и поэтому будет немного неточным. Если вам нужны точные отметки времени, вы всегда должны использовать **st\_atime\_ns**, **st\_mtime\_ns** и **st\_ctime\_ns**.
{% endhint %}

#### В некоторых системах Unix \(например, Linux\) также могут быть доступны следующие атрибуты:

* **st\_blocks** - количество 512-байтовых блоков, выделенных для файла. Это может быть меньше `st_size / 512`, если в файле есть пустые пространства
* **st\_blksize** - «предпочтительный» размер блока для эффективного ввода-вывода файловой системы. Запись в файл небольшими порциями может вызвать неэффективное чтение-изменение-перезапись
* **st\_rdev** - тип устройства, если это устройство является _**inode**_
* **st\_flags** - пользовательские флаги для файла

#### В других системах Unix \(таких как FreeBSD\) могут быть доступны следующие атрибуты \(но могут быть заполнены только в том случае, если root пытается их использовать\):

* **st\_gen** - номер поколения файла
* **st\_birthtime** - время создания файла

#### В Solaris и производных версиях также могут быть доступны следующие атрибуты:

* **st\_fstype** - строка, которая однозначно определяет тип файловой системы, содержащей файл

#### В системах Mac OS также могут быть доступны следующие атрибуты:

* **st\_rsize** - реальный размер файла
* **st\_creator** - создатель файла
* **st\_type** - тип файла

#### В системах Windows также доступны следующие атрибуты:

* **st\_file\_attributes** - атрибуты файлов Windows: член `dwFileAttributes` структуры `BY_HANDLE_FILE_INFORMATION`, возвращаемый GetFileInformationByHandle \(\). См. константы `FILE_ATTRIBUTE_*` в модуле [stat](../../../dostup-k-failam-i-papkam/stat.md)
* **st\_reparse\_tag** - когда **st\_file\_attributes** имеет установленный `FILE_ATTRIBUTE_REPARSE_POINT`, это поле содержит тег, определяющий тип точки повторной обработки. См. константы `IO_REPARSE_TAG_*` в модуле [stat](../../../dostup-k-failam-i-papkam/stat.md)

Стандартный модуль [stat](../../../dostup-k-failam-i-papkam/stat.md) определяет функции и константы, которые полезны для извлечения информации из структуры `stat`. \(В Windows некоторые элементы заполнены фиктивными значениями.\)

Для обратной совместимости экземпляр **stat\_result** также доступен как кортеж из не менее 10 целых чисел, дающих наиболее важные \(и переносимые\) члены структуры `stat`, в порядке **st\_mode**, **st\_ino**, **st\_dev**, **st\_nlink**, **st\_uid**, **st\_gid**, **st\_size**, **st\_atime**, **st\_mtime**, **st\_ctime**. Некоторые реализации могут добавить больше элементов в конце. Для совместимости со старыми версиями Python доступ к **stat\_result** как кортежу всегда возвращает целые числа.

_Новое в версии 3.3:_ добавлены члены **st\_atime\_ns**, **st\_mtime\_ns** и **st\_ctime\_ns**.

_Новое в версии 3.5:_ добавлен член **st\_file\_attributes** в Windows.

_Изменено в версии 3.5:_ Windows теперь возвращает индекс файла как **st\_ino**, если он доступен.

_Новое в версии 3.7:_ Добавлен член **st\_fstype** в Solaris и ее производные ОС.

_Новое в версии 3.8:_ Добавлен член **st\_reparse\_tag** в Windows.

_Изменено в версии 3.8:_ В Windows член **st\_mode** теперь идентифицирует специальные файлы как S\_IFCHR, S\_IFIFO или S\_IFBLK в зависимости от ситуации.


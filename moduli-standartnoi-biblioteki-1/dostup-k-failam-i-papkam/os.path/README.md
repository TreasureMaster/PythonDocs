# os.path

### Общие манипуляции с путями

Этот модуль реализует некоторые полезные функции для имен путей. Для чтения или записи файлов см. open \(\), а для доступа к файловой системе см. модуль [os](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os). Параметры пути могут передаваться в виде строк или байтов. Приложениям рекомендуется представлять имена файлов как строки символов \(Unicode\). К сожалению, некоторые имена файлов могут не быть представлены в виде строк в Unix, поэтому приложения, которым необходимо поддерживать произвольные имена файлов в Unix, должны использовать байтовые объекты для представления имен путей. И наоборот, использование байтовых объектов не может представлять все имена файлов в Windows \(в стандартной кодировке mbcs\), поэтому приложения Windows должны использовать строковые объекты для доступа ко всем файлам.

В отличие от оболочки Unix, Python не выполняет никаких автоматических расширений пути. Такие функции, как expanduser \(\) и expandvars \(\) могут быть вызваны явно, когда приложению требуется расширение пути, подобное оболочке. \(см. также модуль [glob](https://treasuremaster.gitbook.io/python-docs/dostup-k-failam-i-papkam/glob).\)

{% hint style="warning" %}
**Смотрите также: м**одуль [pathlib](https://treasuremaster.gitbook.io/python-docs/dostup-k-failam-i-papkam/pathlib) предлагает высокоуровневые объекты пути.
{% endhint %}

{% hint style="info" %}
Все эти функции принимают в качестве параметров только байты или только строковые объекты. Результат - объект того же типа, если возвращается путь или имя файла.
{% endhint %}

{% hint style="info" %}
Поскольку разные операционные системы имеют разные соглашения об именах путей, в стандартной библиотеке есть несколько версий этого модуля. Модуль **os.path** всегда является модулем пути, подходящим для операционной системы, в которой работает Python, и поэтому может использоваться для локальных путей. Однако вы также можете импортировать и использовать отдельные модули, если хотите управлять путем, который всегда находится в одном из разных форматов. Все они имеют одинаковый интерфейс:

* posixpath - для путей в стиле UNIX
* ntpath - для путей Windows
{% endhint %}

_Изменено в версии 3.8:_ exists \(\), lexists \(\), isdir \(\), isfile \(\), islink \(\) и ismount \(\) теперь возвращают `False` вместо того, чтобы вызывать исключение для путей, содержащих символы или байты, не представленные на уровне ОС.

Список атрибутов **os.path**:

* [os.path.abspath \(\)](os.path.abspath.md) - возвращает абсолютный путь к файлу
* [os.path.basename \(\)](os.path.basename.md) - возвращает базовое имя пути \(вторая часть [os.path.split \(\)](os.path.split.md#os-path-split-path)\)
* os.path.commonpath \(\)
* os.path.commonprefix \(\)
* [os.path.dirname \(\)](os.path.dirname.md) - возвращает имя каталога пути \(первая часть [os.path.split \(\)](os.path.split.md#os-path-split-path) \)
* [os.path.exists \(\)](os.path.exists.md) - отвечает на вопрос: "Существует ли заданный путь или дескриптор файла?"
* os.path.lexists \(\)
* os.path.expanduser \(\)
* os.path.expandvars \(\)
* os.path.getatime \(\)
* os.path.getmtime \(\)
* os.path.getctime \(\)
* [os.path.getsize \(\)](os.path.getsize.md) - возвращает размер файла в байтах
* os.path.isabs \(\)
* [os.path.isfile \(\)](os.path.isfile.md) - отвечает на вопрос: "Существует ли файл по заданному пути?"
* [os.path.isdir \(\)](os.path.isdir.md) - отвечает на вопрос: "Существует ли каталог по заданному пути?"
* os.path.islink \(\)
* os.path.ismount \(\)
* [os.path.join \(\)](os.path.join.md) - соединяет несколько компонентов пути в один с учетом ОС
* os.path.normcase \(\)
* [os.path.normpath \(\)](os.path.normpath.md) - нормализует путь для данной операционной системы
* os.path.realpath \(\)
* os.path.relpath \(\)
* os.path.samefile \(\)
* os.path.sameopenfile \(\)
* os.path.samestat \(\)
* [os.path.split \(\)](os.path.split.md) - разделяет путь к файлу на имя файла и путь к нему
* os.path.splitdrive \(\)
* [os.path.splitext \(\)](os.path.splitext.md) - разделяет путь на имя файла плюс путь к нему и расширение файла
* os.path.supports\_unicode\_filenames


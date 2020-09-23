# sys.argv

#### sys.argv

Список аргументов командной строки, переданных скрипту Python. `argv [0]` - это имя сценария \(зависит от операционной системы, является ли это полным путем или нет\). Если команда была выполнена с использованием параметра командной строки `-c` для интерпретатора, `argv [0]` устанавливается в строку `'-c'`. Если интерпретатору Python не было передано имя сценария, `argv [0]` - это пустая строка.

Чтобы просмотреть стандартный ввод или список файлов в командной строке, см. модуль fileinput.

{% hint style="info" %}
В Unix аргументы командной строки передаются из ОС в байтах. Python декодирует их с помощью кодировки файловой системы и обработчика ошибок «surrogateescape». Если вам нужны исходные байты, вы можете получить их с помощью `[os.fsencode(arg) for arg in sys.argv]`.
{% endhint %}

# os.dup2 ()

### os.dup2 ( _fd_, _fd2_, _inheritable=True _)

Дублирует файловый дескриптор _**fd**_ в _**fd2**_, закрыв первый, если необходимо. Возвращает _**fd2**_. Новый дескриптор файла наследуемый по умолчанию или ненаследуемый, если _**inheritable**_ имеет значение `False`.

_Изменено в версии 3.4:_ добавлен необязательный параметр _**inheritable**_.

_Изменено в версии 3.7:_ Возвращает _**fd2**_ в случае успеха. Раньше всегда возвращалось `None`.

{% hint style="success" %}
Копирует всю системную информацию, связанную с файлом, заданным дескриптором _**fd**_, в файл, заданный дескриптором _**fd2**_.
{% endhint %}

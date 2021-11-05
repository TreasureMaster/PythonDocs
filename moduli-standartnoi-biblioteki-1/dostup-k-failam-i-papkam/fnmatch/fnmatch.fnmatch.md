# fnmatch.fnmatch ()

### fnmatch.fnmatch ( _filename_, _pattern _)

Проверяет, соответствует ли строка имени файла _**filename**_ строке шаблона _**pattern**_, возвращая `True` или `False`. Оба параметра нормализованы по регистру с помощью [os.path.normcase ()](../os.path/os.path.normcase.md). [fnmatchcase ()](fnmatch.fnmatchcase.md) можно использовать для сравнения с учетом регистра, независимо от того, является ли это стандартом для операционной системы.

В этом примере будут напечатаны все имена файлов в текущем каталоге с расширением `.txt`:

```python
import fnmatch
import os

for file in os.listdir('.'):
    if fnmatch.fnmatch(file, '*.txt'):
        print(file)
```

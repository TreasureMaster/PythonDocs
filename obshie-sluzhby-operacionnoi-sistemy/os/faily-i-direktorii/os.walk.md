# os.walk \(\)

### os.walk \( _top_, _topdown=True_, _onerror=None_, _followlinks=False_ \)

Генерирует имена файлов в дереве каталогов, перемещаясь по дереву сверху вниз или снизу вверх. Для каждого каталога в дереве, имеющего корень на вершине каталога \(включая сам верх\), он дает кортеж из трех \(`dirpath`, `dirnames`, `filenames`\).

`dirpath` - это строка, путь к каталогу. `dirnames` - это список имен подкаталогов в `dirpath` \(исключая `'.'` и `'..'`\). `filenames` - это список имен файлов, не являющихся каталогами, в `dirpath`. Обратите внимание, что имена в списках не содержат компонентов пути. Чтобы получить полный путь \(который начинается с _**top**_\) к файлу или каталогу в `dirpath`, выполните `os.path.join(dirpath, name)`.

Если необязательный аргумент _**topdown**_ имеет значение `True` или не указан, тройка для каталога генерируется перед тройками для любого из его подкаталогов \(каталоги создаются сверху вниз\). Если _**topdown**_ имеет значение `False`, тройка для каталога создается после троек для всех его подкаталогов \(каталоги создаются снизу вверх\). Независимо от значения _**topdown**_, список подкаталогов извлекается до создания кортежей для каталога и его подкаталогов.

Когда _**topdown**_ имеет значение `True`, вызывающий объект может изменять список `dirnames` на месте \(возможно, используя del или использование срезов списков\), а **walk \(\)** будет рекурсивно переходить только в подкаталоги, имена которых остаются в `dirnames`; это можно использовать для сокращения поиска, установления определенного порядка посещения или даже для информирования **walk \(\)** о каталогах, которые вызывающий объект создает или переименовывает, прежде чем он снова возобновит **walk \(**\). Изменение `dirnames`, когда _**topdown**_ имеет значение `False`, не влияет на поведение обхода, потому что в восходящем режиме каталоги в `dirnames` создаются до создания самого `dirpath`.

По умолчанию ошибки вызова [scandir \(\)](os.scandir.md) игнорируются. Если указан необязательный аргумент _**onerror**_, это должна быть функция; она будет вызываться с одним аргументом - экземпляром OSError. Она может сообщить об ошибке, чтобы продолжить обход, или вызвать исключение, чтобы прервать обход. Обратите внимание, что имя файла доступно как атрибут `filename` объекта исключения.

По умолчанию **walk \(\)** не переходит по символическим ссылкам, ведущим к каталогам. Установите для _**followlinks**_ значение `True`, чтобы посещать каталоги, на которые указывают символические ссылки, в системах, которые их поддерживают.

{% hint style="info" %}
Имейте в виду, что установка для _**followlinks**_ в значение `True` может привести к бесконечной рекурсии, если ссылка указывает на свой родительский каталог. `walk()` не отслеживает уже посещенные каталоги.
{% endhint %}

{% hint style="info" %}
Если вы передаете относительный путь, не меняйте текущий рабочий каталог между продолжениями работы **walk \(\)**. **walk \(\)** никогда не изменяет текущий каталог и предполагает, что его вызывающая сторона тоже не меняет.
{% endhint %}

В этом примере отображается количество байтов, занятых файлами, не являющимися каталогами, в каждом каталоге в начальном каталоге, за исключением того, что он не просматривает ни один подкаталог CVS:

```python
import os
from os.path import join, getsize
for root, dirs, files in os.walk('python/Lib/email'):
    print(root, "consumes", end=" ")
    print(sum(getsize(join(root, name)) for name in files), end=" ")
    print("bytes in", len(files), "non-directory files")
    if 'CVS' in dirs:
        dirs.remove('CVS')  # не сканировать каталог CVS
```

В следующем примере \(простая реализация [shutil.rmtree \(\)](../../../dostup-k-failam-i-papkam/shutil/shutil.rmtree.md)\) необходимо обходить дерево снизу вверх, [rmdir \(\)](os.rmdir.md) не позволяет удалить каталог, пока он не станет пустым:

```python
# Удалите все доступное из каталога, указанного в "top",
# при условии, что нет символических ссылок.
# ВНИМАНИЕ:  Это опасно!  Например, если top == '/',
# он может удалить все файлы на вашем диске.
import os
for root, dirs, files in os.walk(top, topdown=False):
    for name in files:
        os.remove(os.path.join(root, name))
    for name in dirs:
        os.rmdir(os.path.join(root, name))
```

_Изменено в версии 3.5:_ эта функция теперь вызывает [os.scandir \(\)](os.scandir.md) вместо [os.listdir \(\)](os.listdir.md), что ускоряет работу за счет уменьшения количества вызовов [os.stat \(\)](os.stat.md).

_Изменено в версии 3.6:_ Принимает объект, подобный пути \(_path-like object_ \).

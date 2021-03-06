# sys.platform

#### sys.platform

Эта строка содержит идентификатор платформы, который можно использовать, например, для добавления компонентов, зависящих от платформы, в [sys.path](sys.path.md).

Для систем Unix, за исключением Linux и AIX, это имя ОС в нижнем регистре, возвращаемое `uname -s`, с добавлением первой части версии, возвращаемой `uname -r`, например `'sunos5'` или `'freebsd8'` во время создания Python. Поэтому рекомендуется использовать следующую идиому, если вы не хотите тестировать конкретную версию системы:

```python
if sys.platform.startswith('freebsd'):
    # FreeBSD-specific code here...
elif sys.platform.startswith('linux'):
    # Linux-specific code here...
elif sys.platform.startswith('aix'):
    # AIX-specific code here...
```

Для других систем это значения:

| System | `platform` value |
| :--- | :--- |
| AIX | `'aix'` |
| Linux | `'linux'` |
| Windows | `'win32'` |
| Windows/Cygwin | `'cygwin'` |
| macOS | `'darwin'` |

_Изменено в версии 3.3:_ в Linux **sys.platform** больше не содержит основную версию. Это всегда `'linux'`, а не `'linux2'` или `'linux3'`. Поскольку более старые версии Python включают номер версии, рекомендуется всегда использовать идиому `startswith`, представленную выше.

_Изменено в версии 3.8:_ В AIX **sys.platform** больше не содержит основную версию. Это всегда `'aix'`, а не `'aix5'` или `'aix7'`. Поскольку более старые версии Python включают номер версии, рекомендуется всегда использовать идиому `startswith`, представленную выше.

{% hint style="warning" %}
**Смотрите также:**

[os.name \(\)](../../obshie-sluzhby-operacionnoi-sistemy/os/os.name.md) имеет более грубую детализацию. [os.uname \(\)](../../obshie-sluzhby-operacionnoi-sistemy/os/parametry-processa/os.uname.md) предоставляет информацию о версии, зависящую от системы.

Модуль [platform](../../obshie-sluzhby-operacionnoi-sistemy/platform.md) обеспечивает детальную проверку идентичности системы.
{% endhint %}


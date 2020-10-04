# ctypes

### Библиотека сторонних функций для Python

**ctypes** - это библиотека внешних функций для Python. Она предоставляет типы данных, совместимые с C, и позволяет вызывать функции в библиотеках DLL или совместно используемых библиотеках. Его можно использовать для обертывания этих библиотек на чистом Python.

### Учебник ctypes

{% hint style="info" %}
В примерах кода в этом руководстве используется [doctest](../instrumenty-razrabotki/doctest.md), чтобы убедиться, что они действительно работают. Поскольку некоторые образцы кода ведут себя по-разному в Linux, Windows или Mac OS X, они содержат директивы doctest в комментариях.
{% endhint %}

{% hint style="info" %}
Некоторые примеры кода ссылаются на тип **ctypes** c\_int. На платформах, где `sizeof(long) == sizeof(int)` является псевдонимом для c\_long. Таким образом, вы не должны запутаться, если c\_long напечатан, если вы ожидаете c\_int - на самом деле они одного типа.
{% endhint %}

### Загрузка библиотек динамической компоновки

**ctypes** экспортирует _**cdll**_, а в объектах Windows _**windll**_ и _**oledll**_ для загрузки библиотек динамической компоновки.

Вы загружаете библиотеки, обращаясь к ним как к атрибутам этих объектов. _**cdll**_ загружает библиотеки, которые экспортируют функции, используя стандартное соглашение о вызовах `cdecl`, в то время как библиотеки _**windll**_ вызывают функции с использованием соглашения о вызовах `stdcall`. _**oledll**_ также использует соглашение о вызовах `stdcall` и предполагает, что функции возвращают код ошибки Windows `HRESULT`. Код ошибки используется для автоматического создания исключения OSError при сбое вызова функции.

_Изменено в версии 3.3_: ошибки Windows, используемые для возникновения ошибки WindowsError, которая теперь является псевдонимом OSError.

Вот несколько примеров для Windows. Обратите внимание, что [msvcrt](../specialnye-sluzhby-ms-windows/msvcrt/) - это стандартная библиотека C MS, содержащая большинство стандартных функций C и использующая соглашение о вызовах `cdecl`:

```python
>>> from ctypes import *
>>> print(windll.kernel32)  
<WinDLL 'kernel32', handle ... at ...>
>>> print(cdll.msvcrt)      
<CDLL 'msvcrt', handle ... at ...>
>>> libc = cdll.msvcrt      
>>>
```

Windows автоматически добавляет обычный суффикс файла `.dll`.

{% hint style="info" %}
Доступ к стандартной библиотеке C через `cdll.msvcrt` будет использовать устаревшую версию библиотеки, которая может быть несовместима с той, которая используется Python. По возможности используйте встроенные функции Python или импортируйте и используйте модуль [msvcrt](../specialnye-sluzhby-ms-windows/msvcrt/).
{% endhint %}

В Linux требуется указать имя файла, включая расширение, для загрузки библиотеки, поэтому доступ к атрибутам не может использоваться для загрузки библиотек. Либо следует использовать метод `LoadLibrary ()` загрузчиков dll, либо загрузить библиотеку, создав экземпляр CDLL, вызвав конструктор:

```python
>>> cdll.LoadLibrary("libc.so.6")  
<CDLL 'libc.so.6', handle ... at ...>
>>> libc = CDLL("libc.so.6")       
>>> libc                           
<CDLL 'libc.so.6', handle ... at ...>
>>>
```

### Доступ к функциям из загруженных dll

Функции доступны как атрибуты объектов dll:

```python
>>> from ctypes import *
>>> libc.printf
<_FuncPtr object at 0x...>
>>> print(windll.kernel32.GetModuleHandleA)  
<_FuncPtr object at 0x...>
>>> print(windll.kernel32.MyOwnFunction)     
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "ctypes.py", line 239, in __getattr__
    func = _StdcallFuncPtr(name, self)
AttributeError: function 'MyOwnFunction' not found
>>>
```

Обратите внимание, что системные dll win32, такие как `kernel32` и `user32`, часто экспортируют ANSI, а также UNICODE версии функции. Версия UNICODE экспортируется с добавлением `W` к имени, а версия ANSI экспортируется с добавлением `A` к имени. Функция Win32 `GetModuleHandle`, которая возвращает дескриптор модуля для данного имени модуля, имеет следующий прототип C, и макрос используется для предоставления одного из них как `GetModuleHandle` в зависимости от того, определен ли UNICODE или нет:

```python
/* ANSI version */
HMODULE GetModuleHandleA(LPCSTR lpModuleName);
/* UNICODE version */
HMODULE GetModuleHandleW(LPCWSTR lpModuleName);
```

_**windll**_ не пытается выбрать один из них волшебным образом, вы должны получить доступ к нужной версии, явно указав `GetModuleHandleA` или `GetModuleHandleW`, а затем вызвать ее с байтовыми или строковыми объектами соответственно.

Иногда библиотеки DLL экспортируют функции с именами, которые не являются действительными идентификаторами Python, например `"??2@YAPAXI@Z"`. В этом случае вы должны использовать getattr \(\) для получения функции:

```python
>>> getattr(cdll.msvcrt, "??2@YAPAXI@Z")  
<_FuncPtr object at 0x...>
>>>
```

В Windows некоторые DLL экспортируют функции не по имени, а по порядковому номеру. Доступ к этим функциям можно получить, указав объект dll порядковым номером:

```python
>>> cdll.kernel32[1]  
<_FuncPtr object at 0x...>
>>> cdll.kernel32[0]  
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "ctypes.py", line 310, in __getitem__
    func = _StdcallFuncPtr(name, self)
AttributeError: function ordinal 0 not found
>>>
```

### Вызов функций

Вы можете вызывать эти функции как любые другие вызываемые Python. В этом примере используется функция `time ()`, которая возвращает системное время в секундах с момента появления эпохи Unix, и функция `GetModuleHandleA ()`, которая возвращает дескриптор модуля win32.

В этом примере обе функции вызываются с указателем `NULL` \(`None` не следует использовать как указатель `NULL`\):

```python
>>> print(libc.time(None))  
1150640792
>>> print(hex(windll.kernel32.GetModuleHandleA(None)))  
0x1d000000
>>>
```

ValueError возникает, когда вы вызываете функцию `stdcall` с соглашением о вызовах `cdecl`, или наоборот:

```python
>>> cdll.kernel32.GetModuleHandleA(None)  
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: Procedure probably called with not enough arguments (4 bytes missing)
>>>

>>> windll.msvcrt.printf(b"spam")  
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: Procedure probably called with too many arguments (4 bytes in excess)
>>>
```

Чтобы узнать правильное соглашение о вызовах, вам нужно заглянуть в файл заголовка C или в документацию для функции, которую вы хотите вызвать.

В Windows **ctypes** использует структурированную обработку исключений win32 для предотвращения сбоев из-за общих сбоев защиты, когда функции вызываются с недопустимыми значениями аргументов:

```python
>>> windll.kernel32.GetModuleHandleA(32)  
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
OSError: exception: access violation reading 0x00000020
>>>
```

Однако существует достаточно способов остановить Python с помощью **ctypes**, так что вам в любом случае следует быть осторожными. Модуль обработки ошибок может быть полезен при отладке сбоев \(например, из-за ошибок сегментации, вызванных ошибочными вызовами библиотеки C\).

`None`, целые числа, байтовые объекты и \(unicode\) строки - единственные собственные объекты Python, которые можно напрямую использовать в качестве параметров в этих вызовах функций. `None` передается как указатель C `NULL`, байтовые объекты и строки передаются как указатель на блок памяти, содержащий их данные \(`char *`  __или `wchar_t *` __\). Целые числа Python передаются как тип C `int` по умолчанию для платформ, их значение замаскировано, чтобы соответствовать типу C.

Прежде чем мы перейдем к вызову функций с другими типами параметров, мы должны узнать больше о типах данных **ctypes**.

### Основные типы данных

**ctypes** определяет ряд примитивных типов данных, совместимых с C:


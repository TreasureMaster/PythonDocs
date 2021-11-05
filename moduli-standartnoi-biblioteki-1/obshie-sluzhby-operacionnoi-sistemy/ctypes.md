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

Иногда библиотеки DLL экспортируют функции с именами, которые не являются действительными идентификаторами Python, например `"??2@YAPAXI@Z"`. В этом случае вы должны использовать getattr () для получения функции:

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

В этом примере обе функции вызываются с указателем `NULL` (`None` не следует использовать как указатель `NULL`):

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

Однако существует достаточно способов остановить Python с помощью **ctypes**, так что вам в любом случае следует быть осторожными. Модуль обработки ошибок может быть полезен при отладке сбоев (например, из-за ошибок сегментации, вызванных ошибочными вызовами библиотеки C).

`None`, целые числа, байтовые объекты и (unicode) строки - единственные собственные объекты Python, которые можно напрямую использовать в качестве параметров в этих вызовах функций. `None` передается как указатель C `NULL`, байтовые объекты и строки передаются как указатель на блок памяти, содержащий их данные (`char *` _ _или `wchar_t *`_ _). Целые числа Python передаются как тип C `int` по умолчанию для платформ, их значение замаскировано, чтобы соответствовать типу C.

Прежде чем мы перейдем к вызову функций с другими типами параметров, мы должны узнать больше о типах данных **ctypes**.

### Основные типы данных

**ctypes** определяет ряд примитивных типов данных, совместимых с C:

| Тип ctypes    | Тип С                                     | Тип Python                   |
| ------------- | ----------------------------------------- | ---------------------------- |
| c\_bool       | \_Bool                                    | bool (1)                     |
| c\_char       | char                                      | 1-символьный байтовый объект |
| c\_wchar      | wchar\_t                                  | 1-символьная строка          |
| c\_byte       | char                                      | int                          |
| c\_ubyte      | unsigned char                             | int                          |
| c\_short      | short                                     | int                          |
| c\_ushort     | unsigned short                            | int                          |
| c\_int        | int                                       | int                          |
| c\_uint       | unsigned int                              | int                          |
| c\_long       | long                                      | int                          |
| c\_ulong      | unsigned long                             | int                          |
| c\_longlong   | \_\_int64 или long long                   | int                          |
| c\_ulonglong  | unsigned \_\_int64 или unsigned long long | int                          |
| c\_size\_t    | size\_t                                   | int                          |
| c\_ssize\_t   | ssize\_t или Py\_ssize\_t                 | int                          |
| c\_float      | float                                     | float                        |
| c\_double     | double                                    | float                        |
| c\_longdouble | long double                               | float                        |
| c\_char\_p    | char \* (NUL ограниченный)                | байтовый объект или None     |
| c\_wchar\_p   | wchar\_t \* (NUL ограниченный)            | string или None              |
| c\_void\_p    | void \*                                   | int или None                 |

1. Конструктор принимает любой объект со значением истинности.

Все эти типы можно создать, вызвав их с необязательным инициализатором правильного типа и значения:

```python
>>> c_int()
c_long(0)
>>> c_wchar_p("Hello, World")
c_wchar_p(140018365411392)
>>> c_ushort(-3)
c_ushort(65533)
>>>
```

Поскольку эти типы изменчивы, их значение также можно изменить впоследствии:

```python
>>> i = c_int(42)
>>> print(i)
c_long(42)
>>> print(i.value)
42
>>> i.value = -99
>>> print(i.value)
-99
>>>
```

Присвоение нового значения экземплярам типов указателей c\_char\_p, c\_wchar\_p и c\_void\_p изменяет _**место в памяти**_, на которое они указывают, а _**не содержимое блока памяти**_ (конечно, нет, потому что объекты байтов Python неизменяемы):

```python
>>> s = "Hello, World"
>>> c_s = c_wchar_p(s)
>>> print(c_s)
c_wchar_p(139966785747344)
>>> print(c_s.value)
Hello World
>>> c_s.value = "Hi, there"
>>> print(c_s)              # место в памяти изменилось
c_wchar_p(139966783348904)
>>> print(c_s.value)
Hi, there
>>> print(s)                # первый объект без изменений
Hello, World
>>>
```

Однако вы должны быть осторожны, чтобы не передавать их функциям, ожидающим указателей на изменяемую память. Если вам нужны изменяемые блоки памяти, **ctypes** имеет функцию create\_string\_buffer (), которая создает их различными способами. К текущему содержимому блока памяти можно получить доступ (или изменить) с помощью свойства `raw`; если вы хотите получить доступ к нему как к строке с завершающим NUL, используйте свойство `value`:

```python
>>> from ctypes import *
>>> p = create_string_buffer(3)            # создать 3-байтовый буфер, инициализированный байтами NUL
>>> print(sizeof(p), repr(p.raw))
3 b'\x00\x00\x00'
>>> p = create_string_buffer(b"Hello")     # создать буфер, содержащий строку с завершающим NUL
>>> print(sizeof(p), repr(p.raw))
6 b'Hello\x00'
>>> print(repr(p.value))
b'Hello'
>>> p = create_string_buffer(b"Hello", 10) # создать 10-байтовый буфер
>>> print(sizeof(p), repr(p.raw))
10 b'Hello\x00\x00\x00\x00\x00'
>>> p.value = b"Hi"
>>> print(sizeof(p), repr(p.raw))
10 b'Hi\x00lo\x00\x00\x00\x00\x00'
>>>
```

Функция create\_string\_buffer () заменяет функцию `c_buffer ()` (которая все еще доступна как псевдоним), а также функцию `c_string ()` из более ранних выпусков **ctypes**. Чтобы создать изменяемый блок памяти, содержащий символы Юникода типа C `wchar_t`, используйте функцию create\_unicode\_buffer ().

### Вызов функций, продолжение

Обратите внимание, что `printf` печатает в реальном стандартном канале вывода, а не в [sys.stdout](../sluzhby-sredy-vypolneniya-python/sys/sys.stdin-sys.stdout-sys.stderr.md), поэтому эти примеры будут работать только в приглашении консоли, а не из **IDLE** или **PythonWin**:

```python
>>> printf = libc.printf
>>> printf(b"Hello, %s\n", b"World!")
Hello, World!
14
>>> printf(b"Hello, %S\n", "World!")
Hello, World!
14
>>> printf(b"%d bottles of beer\n", 42)
42 bottles of beer
19
>>> printf(b"%f bottles of beer\n", 42.5)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ArgumentError: argument 2: exceptions.TypeError: Don't know how to convert parameter 2
>>>
```

Как уже упоминалось ранее, все типы Python, кроме целых чисел, строк и байтов, должны быть заключены в соответствующий им тип **ctypes**, чтобы их можно было преобразовать в требуемый тип данных C.

```python
>>> printf(b"An int %d, a double %f\n", 1234, c_double(3.14))
An int 1234, a double 3.140000
31
>>>
```

### Вызов функций с вашими собственными типами данных

Вы также можете настроить преобразование аргументов **ctypes**, чтобы в качестве аргументов функции можно было использовать экземпляры ваших собственных классов. **ctypes** ищет атрибут `_as_parameter_` и использует его в качестве аргумента функции. Конечно, это должно быть целое число, строка или байты:

```python
>>> class Bottles:
...     def __init__(self, number):
...         self._as_parameter_ = number
...
>>> bottles = Bottles(42)
>>> printf(b"%d bottles of beer\n", bottles)
42 bottles of beer
19
>>>
```

Если вы не хотите хранить данные экземпляра в переменной экземпляра `_as_parameter_`, вы можете определить свойство, которое делает атрибут доступным по запросу.

### Указание необходимых типов аргументов (прототипы функций)

Можно указать требуемые типы аргументов функций, экспортируемых из DLL, установив атрибут _**argtypes**_.

_**argtypes**_ должны быть последовательностью типов данных C (функция `printf`, вероятно, здесь не лучший пример, потому что она принимает номер переменной и различные типы параметров в зависимости от строки формата, с другой стороны, это очень удобно, чтобы поэкспериментировать с этой особенностью):

```python
>>> printf.argtypes = [c_char_p, c_char_p, c_int, c_double]
>>> printf(b"String '%s', Int %d, Double %f\n", b"Hi", 10, 2.2)
String 'Hi', Int 10, Double 2.200000
37
>>>
```

Указание формата защищает от несовместимых типов аргументов (как прототип для функции C) и пытается преобразовать аргументы в допустимые типы:

```python
>>> printf(b"%d %d %d", 1, 2, 3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ArgumentError: argument 2: exceptions.TypeError: wrong type
>>> printf(b"%s %d %f\n", b"X", 2, 3)
X 2 3.000000
13
>>>
```

Если вы определили свои собственные классы, которые вы передаете вызовам функций, вы должны реализовать метод класса `from_param ()`,_ _чтобы они могли использовать их в последовательности _**argtypes**_. Метод класса `from_param ()` получает объект Python, переданный в вызов функции, он должен выполнить проверку типа или что-то еще, что необходимо, чтобы убедиться, что этот объект приемлем, а затем вернуть сам объект, его атрибут `_as_parameter_` или все, что вы хотите передать в качестве аргумента функции C. Опять же, результатом должно быть целое число, строка, байты, экземпляр **ctypes** или объект с атрибутом `_as_parameter_`.

### Возвращаемые типы

По умолчанию предполагается, что функции возвращают тип C **int**. Другие возвращаемые типы могут быть указаны путем установки атрибута _**restype**_ объекта функции.

Вот более сложный пример, он использует функцию `strchr`, которая ожидает указатель на строку и символ и возвращает указатель на строку:

```python
>>> strchr = libc.strchr
>>> strchr(b"abcdef", ord("d"))  
8059983
>>> strchr.restype = c_char_p    # c_char_p - указатель на строку
>>> strchr(b"abcdef", ord("d"))
b'def'
>>> print(strchr(b"abcdef", ord("x")))
None
>>>
```

Если вы хотите избежать вышеупомянутых вызовов `ord ("x")`, вы можете установить атрибут _**argtypes**_, и второй аргумент будет преобразован из односимвольного объекта байтов Python в символ C _**char**_:

```python
>>> strchr.restype = c_char_p
>>> strchr.argtypes = [c_char_p, c_char]
>>> strchr(b"abcdef", b"d")
'def'
>>> strchr(b"abcdef", b"def")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ArgumentError: argument 2: exceptions.TypeError: one character string expected
>>> print(strchr(b"abcdef", b"x"))
None
>>> strchr(b"abcdef", b"d")
'def'
>>>
```

Вы также можете использовать вызываемый объект Python (например, функцию или класс) в качестве атрибута _**restype**_, если внешняя функция возвращает целое число. Вызываемый объект будет вызываться с целым числом, возвращаемым функцией C, и результат этого вызова будет использоваться как результат вызова вашей функции. Это полезно для проверки возвращаемых значений ошибок и автоматического создания исключения:

```python
>>> GetModuleHandle = windll.kernel32.GetModuleHandleA  
>>> def ValidHandle(value):
...     if value == 0:
...         raise WinError()
...     return value
...
>>>
>>> GetModuleHandle.restype = ValidHandle  
>>> GetModuleHandle(None)  
486539264
>>> GetModuleHandle("something silly")  
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 3, in ValidHandle
OSError: [Errno 126] The specified module could not be found.
>>>
```

`WinError` - это функция, которая вызывает API-интерфейс Windows `FormatMessage ()` для получения строкового представления кода ошибки и возвращает исключение. `WinError` принимает необязательный параметр кода ошибки, если никто не используется, он вызывает GetLastError () для его получения.

Обратите внимание, что через атрибут _**errcheck**_ доступен гораздо более мощный механизм проверки ошибок; подробности см. в справочном руководстве.

### Передача указателей (или: передача параметров по ссылке)

Иногда API функции C ожидает указатель _**pointer**_ на тип данных в качестве параметра, возможно, для записи в соответствующее место или если данные слишком велики для передачи по значению. Это также известно как _**передача параметров по ссылке**_.

**ctypes** экспортирует функцию byref (), которая используется для передачи параметров по ссылке. Тот же эффект может быть достигнут с помощью функции pointer (), хотя pointer () выполняет гораздо больше работы, поскольку создает реальный объект-указатель, поэтому быстрее использовать byref (), если вам не нужен сам объект-указатель в Python:

```python
>>> i = c_int()
>>> f = c_float()
>>> s = create_string_buffer(b'\000' * 32)
>>> print(i.value, f.value, repr(s.value))
0 0.0 b''
>>> libc.sscanf(b"1 3.14 Hello", b"%d %f %s",
...             byref(i), byref(f), s)
3
>>> print(i.value, f.value, repr(s.value))
1 3.1400001049 b'Hello'
>>>
```

### Структуры и объединения

Структуры и объединения должны быть производными от базовых классов Structure и Union, которые определены в модуле **ctypes**. Каждый подкласс должен определять атрибут_**\_fields\_**_. _**\_fields\_**_ должен быть списком из двух кортежей, содержащим имя поля _**field**_ и тип поля _**type**_.

Тип поля должен быть типом **ctypes**, например c\_int, или любым другим производным типом **ctypes**: структурой, объединением, массивом, указателем.

Вот простой пример структуры POINT, которая содержит два целых числа с именами _**x**_ и _**y**_, а также показывает, как инициализировать структуру в конструкторе:

```python
>>> from ctypes import *
>>> class POINT(Structure):
...     _fields_ = [("x", c_int),
...                 ("y", c_int)]
...
>>> point = POINT(10, 20)
>>> print(point.x, point.y)
10 20
>>> point = POINT(y=5)
>>> print(point.x, point.y)
0 5
>>> POINT(1, 2, 3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: too many initializers
>>>
```

Однако вы можете строить гораздо более сложные конструкции. Структура может сама содержать другие структуры, используя структуру как тип поля.

Вот структура RECT, которая содержит две POINT с именами _**upperleft**_ и _**lowerright**_:

```python
>>> class RECT(Structure):
...     _fields_ = [("upperleft", POINT),
...                 ("lowerright", POINT)]
...
>>> rc = RECT(point)
>>> print(rc.upperleft.x, rc.upperleft.y)
0 5
>>> print(rc.lowerright.x, rc.lowerright.y)
0 0
>>>
```

Вложенные структуры также можно инициализировать в конструкторе несколькими способами:

```python
>>> r = RECT(POINT(1, 2), POINT(3, 4))
>>> r = RECT((1, 2), (3, 4))
```

Дескрипторы полей могут быть получены из класса, они полезны для отладки, поскольку могут предоставить полезную информацию:

```python
>>> print(POINT.x)
<Field type=c_long, ofs=0, size=4>
>>> print(POINT.y)
<Field type=c_long, ofs=4, size=4>
>>>
```

{% hint style="danger" %}
**ctypes** не поддерживает передачу объединений или структур с битовыми полями в функции по значению. Хотя это может работать на 32-битной x86, библиотека не гарантирует работу в общем случае. Объединения и структуры с битовыми полями всегда должны передаваться в функции по указателю.
{% endhint %}

### Выравнивание структуры/объединения и порядок байтов

По умолчанию поля **Structure** и **Union** выравниваются так же, как это делает компилятор C. Это поведение можно изменить, указав атрибут класса_**\_pack\_**_ в определении подкласса. Это должно быть положительное целое число и указывает максимальное выравнивание для полей. Это то, что `#pragma pack(n)` также делает в MSVC.

**ctypes** использует собственный порядок байтов для структур и объединений. Чтобы построить структуры с неродным порядком байтов, вы можете использовать один из базовых классов BigEndianStructure, LittleEndianStructure, BigEndianUnion и LittleEndianUnion. Эти классы не могут содержать поля указателей.

### Битовые поля в структурах и объединениях

Можно создавать структуры и объединения, содержащие битовые поля. Битовые поля возможны только для целочисленных полей, разрядность указывается в третьем элементе кортежей_**\_fields\_**_:

```python
>>> class Int(Structure):
...     _fields_ = [("first_16", c_int, 16),
...                 ("second_16", c_int, 16)]
...
>>> print(Int.first_16)
<Field type=c_long, ofs=0:0, bits=16>
>>> print(Int.second_16)
<Field type=c_long, ofs=0:16, bits=16>
>>>
```

### Массивы

Массивы - это последовательности, содержащие фиксированное количество экземпляров одного типа.

Рекомендуемый способ создания типов массивов - умножение типа данных на положительное целое число:

```python
TenPointsArrayType = POINT * 10
```

Вот пример несколько искусственного типа данных, структура, содержащая, среди прочего, 4 POINT:

```python
>>> from ctypes import *
>>> class POINT(Structure):
...     _fields_ = ("x", c_int), ("y", c_int)
...
>>> class MyStruct(Structure):
...     _fields_ = [("a", c_int),
...                 ("b", c_float),
...                 ("point_array", POINT * 4)]
>>>
>>> print(len(MyStruct().point_array))
4
>>>
```

Экземпляры создаются обычным способом, вызывая класс:

```python
arr = TenPointsArrayType()
for pt in arr:
    print(pt.x, pt.y)
```

Приведенный выше код выводит серию из `0 0` строк, поскольку содержимое массива инициализировано нулями.

Также могут быть указаны инициализаторы правильного типа:

```python
>>> from ctypes import *
>>> TenIntegers = c_int * 10
>>> ii = TenIntegers(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
>>> print(ii)
<c_long_Array_10 object at 0x...>
>>> for i in ii: print(i, end=" ")
...
1 2 3 4 5 6 7 8 9 10
>>>
```

### Указатели

Экземпляры указателя создаются путем вызова функции pointer () для типа **ctypes**:

```python
>>> from ctypes import *
>>> i = c_int(42)
>>> pi = pointer(i)
>>>
```

Экземпляры указателей имеют атрибут содержимого, который возвращает объект, на который указывает указатель, объект `i` выше:

```python
>>> pi.contents
c_long(42)
>>>
```

Обратите внимание, что **ctypes** не имеет OOR (возврат исходного объекта), он создает новый эквивалентный объект каждый раз, когда вы извлекаете атрибут:

```python
>>> pi.contents is i
False
>>> pi.contents is pi.contents
False
>>>
```

Назначение другого экземпляра c\_int атрибуту содержимого указателя приведет к тому, что указатель будет указывать на то место памяти, где он хранится:

```python
>>> i = c_int(99)
>>> pi.contents = i
>>> pi.contents
c_long(99)
>>>
```

Экземпляры указателя также можно индексировать целыми числами:

```python
>>> pi[0]
99
>>>
```

Присвоение целочисленному индексу изменяет указанное значение:

```python
>>> print(i)
c_long(99)
>>> pi[0] = 22
>>> print(i)
c_long(22)
>>>
```

Также можно использовать индексы, отличные от 0, но вы должны знать, что делаете, как и в C: вы можете получить доступ к произвольным ячейкам памяти или изменить их. Обычно вы используете эту функцию, только если вы получаете указатель от функции C, и вы знаете, что указатель фактически указывает на массив, а не на отдельный элемент.

За кулисами функция pointer () делает больше, чем просто создает экземпляры указателя, она должна сначала создать типы _**types**_ указателей. Это делается с помощью функции POINTER (), которая принимает любой тип **ctypes** и возвращает новый тип:

```python
>>> PI = POINTER(c_int)
>>> PI
<class 'ctypes.LP_c_long'>
>>> PI(42)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: expected c_long instead of int
>>> PI(c_int(42))
<ctypes.LP_c_long object at 0x...>
>>>
```

Вызов типа указателя без аргумента создает указатель `NULL`. Указатели `NULL` имеют логическое значение `False`:

```python
>>> null_ptr = POINTER(c_int)()
>>> print(bool(null_ptr))
False
>>>
```

**ctypes** проверяет `NULL` при разыменовании указателей (но разыменование недопустимых указателей, отличных от `NULL`, приведет к сбою Python):

```python
>>> null_ptr[0]
Traceback (most recent call last):
    ....
ValueError: NULL pointer access
>>>

>>> null_ptr[0] = 1234
Traceback (most recent call last):
    ....
ValueError: NULL pointer access
>>>
```

### Преобразование типов

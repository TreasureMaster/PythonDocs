# socket

### Сетевой интерфейс низкого уровня

Этот модуль обеспечивает доступ к интерфейсу сокета _**socket**_ BSD. Он доступен во всех современных системах Unix, Windows, MacOS и, возможно, на дополнительных платформах.

{% hint style="info" %}
Некоторое поведение может зависеть от платформы, поскольку выполняются вызовы API сокетов операционной системы.
{% endhint %}

Интерфейс Python представляет собой прямую транслитерацию системного вызова Unix и интерфейса библиотеки для сокетов в объектно-ориентированный стиль Python: функция [socket \(\)](funkcii-soketov/socket.socket.md) возвращает объект сокета, методы которого реализуют различные системные вызовы сокетов. Типы параметров несколько более высокоуровневые, чем в интерфейсе C: как и в случае операций чтения \(\) и записи \(\) с файлами Python, распределение буфера при операциях приема происходит автоматически, а длина буфера неявна при операциях отправки.

{% hint style="warning" %}
См. также:

Модуль [socketserver](../../internet-protokoly/socketserver.md) - классы, упрощающие написание сетевых серверов.

Модуль [ssl](../ssl.md) - оболочка TLS/SSL для объектов сокета.
{% endhint %}

### [Семейство сокетов](semeistvo-soketov.md)

В зависимости от системы и параметров сборки этот модуль поддерживает различные семейства сокетов.

Формат адреса, необходимый для конкретного объекта сокета, выбирается автоматически на основе семейства адресов, указанного при создании объекта сокета. Адреса сокетов представлены следующим образом:

* AF\_UNIX
* AF\_INET
* AF\_INET6
* AF\_NETLINK
* AF\_TIPC
* AF\_CAN
* PF\_SYSTEM
* AF\_BLUETOOTH
* AF\_ALG
* AF\_VSOCK
* AF\_PACKET
* AF\_QIPCRTR
* IPPROTO\_UDPLITE

Если вы используете имя хоста в части хоста адреса сокета IPv4/v6, программа может показывать недетерминированное поведение, поскольку Python использует первый адрес, возвращенный из разрешения DNS. Адрес сокета будет по-разному преобразован в фактический адрес IPv4/v6, в зависимости от результатов разрешения DNS и/или конфигурации хоста. Для детерминированного поведения используйте числовой адрес в части хоста.

Все ошибки вызывают исключения. Могут возникать обычные исключения для недопустимых типов аргументов и условий нехватки памяти; начиная с Python 3.3, ошибки, связанные с семантикой сокета или адреса, вызывают OSError или один из его подклассов \(они использовались для повышения [socket.error](isklyucheniya-soketov/socket.error.md)\).

Неблокирующий режим поддерживается через [setblocking \(\)](obekty-soketov/socket.setblocking.md). Обобщение этого на основе тайм-аутов поддерживается через [settimeout \(\)](obekty-soketov/socket.settimeout.md).

### Содержимое модуля

Модуль **socket** экспортирует следующие элементы.

### [Исключения](isklyucheniya-soketov/)

* socket.error exception
* socket.herror exception
* socket.gaierror exception
* socket.timeout exception

### [Константы](konstanty-soketov/)

* socket.AF\_UNIX
* socket.AF\_INET
* socket.AF\_INET6
* socket.SOCK\_STREAM
* не заполнено...
* socket.CAN\_BCM
* не заполнено...

### [Функции](funkcii-soketov/)

#### Создание сокетов

Все следующие функции создают объекты сокетов.

* [socket.socket \(\)](funkcii-soketov/socket.socket.md) - создает новый сокет
* socket.socketpair \(\)
* socket.create\_connection \(\)
* 
#### Другие функции

Модуль **socket** также предлагает различные сетевые услуги:

* [socket.close \(\)](funkcii-soketov/socket.close.md) - закрывает дескриптор файла сокета
* не заполнено...
* socket.gethostbyname \(\)
* socket.gethostbyname\_ex \(\)
* socket.gethostname \(\)
* socket.gethostbyaddr \(\)
* socket.getnameinfo \(\)
* socket.getprotobyname \(\)
* socket.getservbyname \(\)
* socket.getservbyport \(\)
* socket.ntohl \(\)
* socket.ntohs \(\)
* socket.htonl \(\)
* не заполнено...
* socket.getdeafulttimeout \(\)
* socket.setdefaulttimeout \(\)
* socket.sethostname \(\)
* socket.if\_nameindex \(\)
* socket.if\_nametoindex \(\)
* socket.if\_indextoname \(\)

### [Объекты сокетов](obekty-soketov/)

У объектов **socket** есть следующие методы. За исключением makefile \(\), они соответствуют системным вызовам Unix, применимым к сокетам.

_Изменено в версии 3.2_: добавлена поддержка протокола диспетчера контекста. Выход из диспетчера контекста эквивалентен вызову [close \(\)](funkcii-soketov/socket.close.md).

* [socket.accept \(\)](obekty-soketov/socket.accept.md) - принимает соединение
* [socket.bind \(\)](obekty-soketov/socket.bind.md) - привязывает сокет к адресу
* [socket.close \(\)](obekty-soketov/socket.close.md) - помечает сокет закрытым
* [socket.connect \(\)](obekty-soketov/socket.connect.md) - подключается к удаленному сокету по заданному адресу
* socket.connect\_ex \(\)
* socket.detach \(\)
* socket.dup \(\)
* socket.fileno \(\)
* socket.get\_inheritable \(\)
* socket.getpeername \(\)
* socket.getsockname \(\)
* socket.getsockopt \(\)
* socket.getblocking \(\)
* socket.gettimeout \(\)
* socket.ioctl \(\)
* [socket.listen \(\)](obekty-soketov/socket.listen.md) - разрешает серверу принимать заданное количество соединений
* socket.makefile \(\)
* [socket.recv \(\)](obekty-soketov/socket.recv.md) - получает данные из сокета
* socket.recvfrom \(\)
* socket.recvmsg \(\)
* socket.recvmsg\_into \(\)
* socket.recvfrom\_into \(\)
* socket.recv\_into \(\)
* [socket.send \(\)](obekty-soketov/socket.send.md) - отправляет данные в сокет
* [socket.sendall \(\)](obekty-soketov/socket.sendall.md) - отправляет все данные в сокет принудительно
* socket.sendto \(\)
* socket.sendmsg \(\)
* socket.sendmsg\_afalg \(\)
* socket.send\_fds \(\)
* socket.recv\_fds \(\)
* socket.sendfile \(\)
* socket.set\_inheritable \(\)
* socket.setblocking \(\)
* socket.settimeout \(\)
* socket.setsockopt \(\)
* socket.shutdown \(\)
* socket.share \(\)
* socket.family
* socket.type
* socket.proto

### Примечания относительно тайм-аутов сокетов

Объект сокета может находиться в одном из трех режимов: блокирующий, неблокирующий или тайм-аут. По умолчанию сокеты всегда создаются в режиме блокировки, но это можно изменить, вызвав [setdefaulttimeout \(\)](funkcii-soketov/socket.setdefaulttimeout.md).

* В режиме блокировки _**blocking mode**_ операции блокируются до завершения или система не возвращает ошибку \(например, истекло время ожидания соединения\).
* В неблокирующем режиме _**non-blocking mode**_ операции завершаются неудачно \(с ошибкой, которая, к сожалению, зависит от системы\), если они не могут быть выполнены немедленно: функции из модуля [select](../select.md) могут использоваться, чтобы узнать, когда и доступен ли сокет для чтения или записи.
* В режиме тайм-аута _**timeout mode**_ операции завершаются ошибкой, если они не могут быть завершены в течение тайм-аута, указанного для сокета \(они вызывают исключение тайм-аута [timeout exception](isklyucheniya-soketov/socket.timeout.md)\) или если система возвращает ошибку.

{% hint style="info" %}
На уровне операционной системы сокеты в режиме тайм-аута внутренне устанавливаются в неблокирующий режим. Кроме того, режимы блокировки и тайм-аута используются совместно дескрипторами файлов и объектами сокетов, которые относятся к одной и той же конечной точке сети. Эта деталь реализации может иметь видимые последствия, если, например, вы решили использовать [fileno \(\)](obekty-soketov/socket.fileno.md) сокета.
{% endhint %}

### Тайм-ауты и метод connect

Операция [connect \(\)](obekty-soketov/socket.connect.md) также зависит от установки тайм-аута, и в целом рекомендуется вызвать [settimeout \(\)](obekty-soketov/socket.settimeout.md) перед вызовом [connect \(\)](obekty-soketov/socket.connect.md) или передать параметр тайм-аута в [create\_connection \(\)](funkcii-soketov/socket.create_connection.md). Однако системный сетевой стек может также возвращать собственную ошибку тайм-аута соединения независимо от любого параметра тайм-аута сокета Python.

### Тайм-ауты и метод accept

Если [getdefaulttimeout \(\)](funkcii-soketov/socket.getdefaulttimeout.md) не равно `None`, сокеты, возвращаемые методом [accept \(\)](obekty-soketov/socket.accept.md), наследуют этот тайм-аут. В противном случае поведение зависит от настроек прослушивающего сокета:

* если прослушивающий сокет находится в режиме блокировки _**blocking mode**_ или в режиме тайм-аута _**timeout mode**_, сокет, возвращаемый функцией [accept \(\)](obekty-soketov/socket.accept.md), находится в режиме блокировки _**blocking mode**_;
* если прослушивающий сокет находится в неблокирующем режиме _**non-blocking mode**_, то, находится ли сокет, возвращаемый [accept \(\)](obekty-soketov/socket.accept.md), в блокирующем или неблокирующем режиме, зависит от операционной системы. Если вы хотите обеспечить кросс-платформенное поведение, рекомендуется вручную переопределить этот параметр.

### Примеры

Вот четыре минимальных примера программ, использующих протокол TCP/IP: сервер, который отображает все данные, которые он получает обратно \(обслуживая только одного клиента\), и клиент, использующий его. Обратите внимание, что сервер должен выполнять последовательность [socket \(\)](funkcii-soketov/socket.socket.md), [bind \(\)](obekty-soketov/socket.bind.md), [listen \(\)](obekty-soketov/socket.listen.md), [accept \(\)](obekty-soketov/socket.accept.md) \(возможно, повторяя [accept \(\)](obekty-soketov/socket.accept.md) для обслуживания более чем одного клиента\), в то время как клиенту требуется только последовательность [socket \(\)](funkcii-soketov/socket.socket.md), [connect \(\)](obekty-soketov/socket.connect.md). Также обратите внимание, что сервер не выполняет [sendall \(\)](obekty-soketov/socket.sendall.md) / [recv \(\)](obekty-soketov/socket.recv.md) на сокете, который он прослушивает, а на новом сокете, возвращаемом [accept \(\)](obekty-soketov/socket.accept.md).

Первые два примера поддерживают только IPv4.

```python
# Программа эхо-сервера
import socket

HOST = ''                 # Символическое имя, означающее все доступные интерфейсы
PORT = 50007              # Произвольный непривилегированный порт
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.bind((HOST, PORT))
    s.listen(1)
    conn, addr = s.accept()
    with conn:
        print('Connected by', addr)
        while True:
            data = conn.recv(1024)
            if not data: break
            conn.sendall(data)
```

```python
# Программа эхо-клиента
import socket

HOST = 'daring.cwi.nl'    # Удаленный хост
PORT = 50007              # Тот же порт, что и сервер
with socket.socket(socket.AF_INET, socket.SOCK_STREAM) as s:
    s.connect((HOST, PORT))
    s.sendall(b'Hello, world')
    data = s.recv(1024)
print('Received', repr(data))
```

Следующие два примера идентичны двум приведенным выше, но поддерживают как IPv4, так и IPv6. Сторона сервера будет прослушивать первое доступное семейство адресов \(вместо этого она должна слушать оба\). В большинстве систем, поддерживающих IPv6, IPv6 будет иметь приоритет, и сервер может не принимать трафик IPv4. Клиентская сторона попытается подключиться ко всем адресам, полученным в результате разрешения имен, и отправит трафик на первый успешно подключенный.

```python
# Программа эхо-сервера
import socket
import sys

HOST = None               # Символическое имя, означающее все доступные интерфейсы
PORT = 50007              # Произвольный непривилегированный порт
s = None
for res in socket.getaddrinfo(HOST, PORT, socket.AF_UNSPEC,
                              socket.SOCK_STREAM, 0, socket.AI_PASSIVE):
    af, socktype, proto, canonname, sa = res
    try:
        s = socket.socket(af, socktype, proto)
    except OSError as msg:
        s = None
        continue
    try:
        s.bind(sa)
        s.listen(1)
    except OSError as msg:
        s.close()
        s = None
        continue
    break
if s is None:
    print('could not open socket')
    sys.exit(1)
conn, addr = s.accept()
with conn:
    print('Connected by', addr)
    while True:
        data = conn.recv(1024)
        if not data: break
        conn.send(data)
```

```python
# Программа эхо-клиента
import socket
import sys

HOST = 'daring.cwi.nl'    # Удаленный хост
PORT = 50007              # Тот же порт, что и сервер
s = None
for res in socket.getaddrinfo(HOST, PORT, socket.AF_UNSPEC, socket.SOCK_STREAM):
    af, socktype, proto, canonname, sa = res
    try:
        s = socket.socket(af, socktype, proto)
    except OSError as msg:
        s = None
        continue
    try:
        s.connect(sa)
    except OSError as msg:
        s.close()
        s = None
        continue
    break
if s is None:
    print('could not open socket')
    sys.exit(1)
with s:
    s.sendall(b'Hello, world')
    data = s.recv(1024)
print('Received', repr(data))
```

В следующем примере показано, как написать очень простой сетевой сниффер с необработанными сокетами в Windows. В примере требуются права администратора для изменения интерфейса:

```python
import socket

# публичный сетевой интерфейс
HOST = socket.gethostbyname(socket.gethostname())

# создать необработанный сокет и привязать его к общедоступному интерфейсу
s = socket.socket(socket.AF_INET, socket.SOCK_RAW, socket.IPPROTO_IP)
s.bind((HOST, 0))

# Включить заголовки IP
s.setsockopt(socket.IPPROTO_IP, socket.IP_HDRINCL, 1)

# получить все пакеты
s.ioctl(socket.SIO_RCVALL, socket.RCVALL_ON)

# получить пакет
print(s.recvfrom(65565))

# отключен беспорядочный режим
s.ioctl(socket.SIO_RCVALL, socket.RCVALL_OFF)
```

В следующем примере показано, как использовать интерфейс сокета для связи с сетью CAN с использованием протокола сырых сокетов. Чтобы вместо этого использовать CAN с протоколом диспетчера вещания, откройте сокет с помощью:

```python
socket.socket(socket.AF_CAN, socket.SOCK_DGRAM, socket.CAN_BCM)
```

После привязки \(CAN\_RAW\) или подключения \([CAN\_BCM](konstanty-soketov/socket.can_bcm.md)\) сокета вы можете использовать операции [socket.send \(\)](obekty-soketov/socket.send.md) и [socket.recv \(\)](obekty-soketov/socket.recv.md) \(и их аналоги\) для объекта сокета как обычно.

В этом последнем примере могут потребоваться особые привилегии:

```python
import socket
import struct


# Упаковка/распаковка CAN-фреймов (см. 'Struct can_frame' в <linux / can.h>)

can_frame_fmt = "=IB3x8s"
can_frame_size = struct.calcsize(can_frame_fmt)

def build_can_frame(can_id, data):
    can_dlc = len(data)
    data = data.ljust(8, b'\x00')
    return struct.pack(can_frame_fmt, can_id, can_dlc, data)

def dissect_can_frame(frame):
    can_id, can_dlc, data = struct.unpack(can_frame_fmt, frame)
    return (can_id, can_dlc, data[:can_dlc])


# создать необработанный сокет и привязать его к интерфейсу 'vcan0'
s = socket.socket(socket.AF_CAN, socket.SOCK_RAW, socket.CAN_RAW)
s.bind(('vcan0',))

while True:
    cf, addr = s.recvfrom(can_frame_size)

    print('Received: can_id=%x, can_dlc=%x, data=%s' % dissect_can_frame(cf))

    try:
        s.send(cf)
    except OSError:
        print('Error sending CAN frame')

    try:
        s.send(build_can_frame(0x01, b'\x01\x02\x03'))
    except OSError:
        print('Error sending CAN frame')
```

Выполнение примера несколько раз со слишком малой задержкой между выполнениями может привести к этой ошибке:

```python
OSError: [Errno 98] Address already in use
```

Это связано с тем, что предыдущее выполнение оставило сокет в состоянии `TIME_WAIT` и не может быть немедленно использовано повторно.

Чтобы предотвратить это, нужно установить флаг сокета **socket.SO\_REUSEADDR**:

```python
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
s.bind((HOST, PORT))
```

флаг `SO_REUSEADDR` указывает ядру повторно использовать локальный сокет в состоянии `TIME_WAIT`, не дожидаясь истечения его естественного тайм-аута.

{% hint style="info" %}
См.также: Введение в программирование сокетов \(на C\) можно найти в следующих статьях:

* Вводное руководство по межпроцессному взаимодействию 4.3BSD от Стюарта Сечреста
* Расширенный учебник по межпроцессному взаимодействию 4.3BSD, Сэмюэл Дж. Леффлер и др.

оба в Руководстве программиста UNIX, Дополнительные документы 1 \(разделы PS1: 7 и PS1: 8\). Справочные материалы, относящиеся к конкретной платформе, по различным системным вызовам, связанным с сокетами, также являются ценным источником информации о деталях семантики сокетов. Для Unix см. Справочные страницы; для Windows см. спецификацию WinSock \(или Winsock 2\). Для интерфейсов API, поддерживающих IPv6, читатели могут захотеть обратиться к [RFC 3493](https://tools.ietf.org/html/rfc3493.html) под названием «Расширения базового интерфейса сокетов для IPv6».
{% endhint %}


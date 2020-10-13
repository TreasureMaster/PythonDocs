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

### [Константы](konstanty-soketov.md)

### [Функции](funkcii-soketov/)

#### Создание сокетов

Все следующие функции создают объекты сокетов.

* socket.socket \(\)
* 
#### Другие функции

Модуль **socket** также предлагает различные сетевые услуги:

* socket.close \(\)
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
* socket.setdefaulttimeout \(\)
* socket.sethostname \(\)
* socket.if\_nameindex \(\)
* socket.if\_nametoindex \(\)
* socket.if\_indextoname \(\)

### [Объекты сокетов](obekty-soketov/)

У объектов **socket** есть следующие методы. За исключением makefile \(\), они соответствуют системным вызовам Unix, применимым к сокетам.

_Изменено в версии 3.2_: добавлена поддержка протокола диспетчера контекста. Выход из диспетчера контекста эквивалентен вызову [close \(\)](funkcii-soketov/socket.close.md).

* socket.accept \(\)
* socket.bind \(\)
* socket.close \(\)
* socket.connect \(\)
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
* socket.listen \(\)
* socket.makefile \(\)
* socket.recv \(\)
* socket.recvfrom \(\)
* socket.recvmsg \(\)
* socket.recvmsg\_into \(\)
* socket.recvfrom\_into \(\)
* socket.recv\_into \(\)
* socket.send \(\)
* socket.sendall \(\)
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


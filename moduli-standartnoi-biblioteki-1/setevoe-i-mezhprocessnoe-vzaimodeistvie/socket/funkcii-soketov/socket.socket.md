# socket.socket \(\)

### socket.socket \( _family=AF\_INET_, _type=SOCK\_STREAM_, _proto=0_, _fileno=None_ \)

Создает новый сокет, используя указанное семейство адресов _**family**_, тип сокета _**type**_ и номер протокола _**proto**_. Семейство адресов должно быть [AF\_INET](../konstanty-soketov/socket.af_inet.md) \(по умолчанию\), [AF\_INET6](../konstanty-soketov/socket.af_inet6.md), [AF\_UNIX](../konstanty-soketov/socket.af_unix.md), [AF\_CAN](../konstanty-soketov/socket.af_can.md), [AF\_PACKET](../konstanty-soketov/socket.af_packet.md) или [AF\_RDS](../konstanty-soketov/socket.af_rds.md). Тип сокета должен быть [SOCK\_STREAM](../konstanty-soketov/socket.sock_stream.md) \(по умолчанию\), [SOCK\_DGRAM](../konstanty-soketov/socket.sock_dgram.md), [SOCK\_RAW](../konstanty-soketov/socket.sock_raw.md) или, возможно, одной из других констант `SOCK_`. Номер протокола обычно равен нулю и может быть опущен, или в случае, когда семейство адресов [AF\_CAN](../konstanty-soketov/socket.af_can.md), протокол должен быть одним из **CAN\_RAW**, [CAN\_BCM](../konstanty-soketov/socket.can_bcm.md), [CAN\_ISOTP](../konstanty-soketov/socket.can_isotp.md) или [CAN\_J1939](../konstanty-soketov/socket.can_j1939.md).

Если указано _**fileno**_, значения для _**family**_, _**type**_ и _**proto**_ автоматически определяются из указанного файлового дескриптора. Автоопределение можно отменить, вызвав функцию с явными аргументами семейства _**family**_, типа _**type**_ или протокола _**proto**_. Это влияет только на то, как Python представляет, например, возвращаемое значение [socket.getpeername \(\)](../obekty-soketov/socket.getpeername.md), но не фактический ресурс ОС. В отличие от [socket.fromfd \(\)](socket.fromfd.md), _**fileno**_ вернет тот же сокет, а не его дубликат. Это может помочь закрыть отсоединенный сокет с помощью [socket.close \(\)](socket.close.md).

Вновь созданный сокет не наследуется.

Создает событие аудита `socket.__new__` с аргументами _**self**_, _**family**_, _**type**_, _**protocol**_.

_Изменено в версии 3.3_: Добавлено семейство **AF\_CAN**. Добавлено семейство **AF\_RDS**.

_Изменено в версии 3.4_: Добавлен протокол **CAN\_BCM**.

_Изменено в версии 3.4_: возвращаемый сокет теперь не наследуется.

_Изменено в версии 3.7_: Добавлен протокол **CAN\_ISOTP**.

_Изменено в версии 3.7_: Когда битовые флаги [SOCK\_NONBLOCK](../konstanty-soketov/socket.sock_nonblock.md) или [SOCK\_CLOEXEC](../konstanty-soketov/socket.sock_cloexec.md) применяются к типу _**type**_, они очищаются, и [socket.type](../obekty-soketov/socket.type.md) не будет их отражать. Они по-прежнему передаются в базовый системный вызов **socket \(\)**.

Следовательно, будет по-прежнему создаваться неблокирующий сокет в операционных системах, поддерживающих `SOCK_NONBLOCK`, но для `sock.type` будет установлено значение `socket.SOCK_STREAM`.

```python
sock = socket.socket(
    socket.AF_INET,
    socket.SOCK_STREAM | socket.SOCK_NONBLOCK)
```

_Изменено в версии 3.9_: Добавлен протокол **CAN\_J1939**.


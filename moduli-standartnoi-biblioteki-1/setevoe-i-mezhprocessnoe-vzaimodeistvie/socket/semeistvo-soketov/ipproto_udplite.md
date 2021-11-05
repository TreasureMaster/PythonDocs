# IPPROTO\_UDPLITE

### IPPROTO\_UDPLITE

**IPPROTO\_UDPLITE** - это вариант UDP, который позволяет указать, какая часть пакета покрывается контрольной суммой. Он добавляет два параметра сокета, которые вы можете изменить. `self.setsockopt (IPPROTO_UDPLITE, UDPLITE_SEND_CSCOV, length)` изменит, какая часть исходящих пакетов покрывается контрольной суммой, а `self.setsockopt (IPPROTO_UDPLITE, UDPLITE_RECV_CSCOV, length)` отфильтрует пакеты, которые покрывают слишком мало данных. В обоих случаях длина должна быть в диапазоне `range (8, 2 ** 16, 8)`.

Такой сокет должен быть построен с сокетом `socket (AF_INET, SOCK_DGRAM, IPPROTO_UDPLITE)` для IPv4 или сокетом `socket (AF_INET6, SOCK_DGRAM, IPPROTO_UDPLITE)` для IPv6.

**Доступность: **Linux> = 2.6.20, FreeBSD> = 10.1-RELEASE

_Новое в версии 3.9._

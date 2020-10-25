# AF\_TIPC

### AF\_TIPC

Поддержка [**TIPC**](https://en.wikipedia.org/wiki/Transparent_Inter-process_Communication) только для Linux доступна с использованием семейства адресов **AF\_TIPC**. [**TIPC**](http://tipc.io/protocol.html) - это открытый сетевой протокол, не основанный на IP, разработанный для использования в кластерных компьютерных средах. Адреса представлены кортежем, а поля зависят от типа адреса. Общая форма кортежа - `(addr_type, v1, v2, v3 [, scope])`, где:

* _**addr\_type**_ может быть одним из `TIPC_ADDR_NAMESEQ`, `TIPC_ADDR_NAME` или `TIPC_ADDR_ID`.
* _**scope**_ - одна из `TIPC_ZONE_SCOPE`, `TIPC_CLUSTER_SCOPE` и `TIPC_NODE_SCOPE`.
* если _**addr\_type**_ - `TIPC_ADDR_NAME`, то _**v1**_ - это тип сервера, _**v2**_ - идентификатор порта, а _**v3**_ должен быть `0`.
* если _**addr\_type**_ - `TIPC_ADDR_NAMESEQ`, то _**v1**_ - это тип сервера, _**v2**_ - нижний номер порта, а _**v3**_ - верхний номер порта.
* если _**addr\_type**_ равен `TIPC_ADDR_ID`, тогда _**v1**_ - это узел, _**v2**_ - ссылка, а _**v3**_ должно быть установлено в `0`.


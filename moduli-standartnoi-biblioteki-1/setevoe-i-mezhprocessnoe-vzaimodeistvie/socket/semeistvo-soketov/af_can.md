# AF\_CAN

### AF\_CAN

Кортеж `(interface,)` используется для семейства адресов **AF\_CAN**, где _**interface**_ - это строка, представляющая имя сетевого интерфейса, например, `can0`. Имя сетевого интерфейса `''` можно использовать для приема пакетов от всех сетевых интерфейсов этого семейства.

* Протокол [CAN\_ISOTP](../konstanty-soketov/socket.can_isotp.md) требует кортежа `(interface, rx_addr, tx_addr)`, где оба дополнительных параметра представляют собой длинное целое число без знака, представляющее идентификатор CAN \(стандартный или расширенный\).
* Протокол [CAN\_J1939](../konstanty-soketov/socket.can_j1939.md) требует кортежа `(interface, name, pgn, addr)`, где дополнительными параметрами являются 64-битное целое число без знака, представляющее имя ECU, 32-битное целое число без знака, представляющее номер группы параметров \(PGN\), и 8-битное целое число, представляющее адрес.

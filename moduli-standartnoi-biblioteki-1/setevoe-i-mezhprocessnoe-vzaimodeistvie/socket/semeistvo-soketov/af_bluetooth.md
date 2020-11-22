# AF\_BLUETOOTH

### AF\_BLUETOOTH

**AF\_BLUETOOTH** поддерживает следующие протоколы и форматы адресов:

* **BTPROTO\_L2CAP** принимает `(bdaddr, psm)`, где _**bdaddr**_ - это адрес Bluetooth в виде строки, а _**psm**_ - целое число.
* **BTPROTO\_RFCOMM** принимает `(bdaddr, channel)`, где _**bdaddr**_ - это адрес Bluetooth в виде строки, а канал _**channel**_ - целое число.
* **BTPROTO\_HCI** принимает `(device_id,)`, где _**device\_id**_ является целым числом или строкой с Bluetooth-адресом интерфейса. \(Это зависит от вашей ОС; NetBSD и DragonFlyBSD ожидают адрес Bluetooth, а все остальное - целое число.\)
* **BTPROTO\_SCO** принимает _**bdaddr**_, где _**bdaddr**_ - байтовый объект, содержащий адрес Bluetooth в строковом формате. \(например, `b'12:23:34:45:56:67'`\) Этот протокол не поддерживается FreeBSD.

_Изменено в версии 3.2:_ добавлена поддержка NetBSD и DragonFlyBSD для **BTPROTO\_HCI**.


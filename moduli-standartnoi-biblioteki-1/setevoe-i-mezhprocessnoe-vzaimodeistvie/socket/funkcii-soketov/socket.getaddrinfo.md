# socket.getaddrinfo ()

### socket.getaddrinfo ( _host_, _port_, _family=0_, _type=0_, _proto=0_, _flags=0 _)

Преобразует аргументы _**host**_/_**port**_ в последовательность из кортежа с 5 членами, которые содержат все необходимые аргументы для создания сокета, подключенного к этой службе. _**host**_ - это доменное имя, строковое представление адреса IPv4/v6 или `None`. _**port**_ - это строковое имя службы, такое как `'http'`, числовой номер порта или `None`. Передав `None` в качестве значения _**host**_ и _**port**_, вы можете передать `NULL` в базовый API C.

Аргументы семейства _**family**_, типа _**type**_ и прототипа _**proto**_ могут быть дополнительно указаны, чтобы сузить список возвращаемых адресов. Передача нуля в качестве значения для каждого из этих аргументов выбирает полный диапазон результатов. Аргумент _**flags**_ может быть одной или несколькими константами `AI_*` и будет влиять на способ вычисления и возврата результатов. Например, `AI_NUMERICHOST` отключит разрешение доменного имени и вызовет ошибку, если _**host**_ является доменным именем.

Функция возвращает список из кортежа с 5 элементами со следующей структурой:

`(family, type, proto, canonname, sockaddr)`

В этих кортежах _**family**_, _**type**_, _**proto**_ являются целыми числами и предназначены для передачи в функцию [socket ()](socket.socket.md). _**canonname**_ будет строкой, представляющей каноническое имя хоста _**host**_, если `AI_CANONNAME` является частью аргумента _**flags**_; иначе _**canonname**_ будет пустым. _**sockaddr**_ - это кортеж, описывающий адрес сокета, формат которого зависит от возвращаемого семейства _**family **_(кортеж с 2 элементами `(address, port)` для [AF\_INET](../konstanty-soketov/socket.af\_inet.md), кортеж с 4 элементами `(address, port, flowinfo, scope_id)` для [AF\_INET6](../konstanty-soketov/socket.af\_inet6.md)) и предназначен для передачи в метод [socket.connect ()](../obekty-soketov/socket.connect.md).

Вызывает событие аудита `socket.getaddrinfo` с аргументами _**host**_, _**port**_, _**family**_, _**type**_, _**protocol**_.

В следующем примере извлекается адресная информация для гипотетического TCP-соединения с `example.org` через порт 80 (результаты могут отличаться в вашей системе, если IPv6 не включен):

```python
>>> socket.getaddrinfo("example.org", 80, proto=socket.IPPROTO_TCP)
[(<AddressFamily.AF_INET6: 10>, <SocketType.SOCK_STREAM: 1>,
 6, '', ('2606:2800:220:1:248:1893:25c8:1946', 80, 0, 0)),
 (<AddressFamily.AF_INET: 2>, <SocketType.SOCK_STREAM: 1>,
 6, '', ('93.184.216.34', 80))]
```

_Изменено в версии 3.2_: параметры теперь можно передавать с помощью ключевых аргументов.

_Изменено в версии 3.7_: для адресов многоадресной рассылки IPv6 строка, представляющая адрес, не будет содержать `%scope_id` часть.

# socket.gethostbyaddr ()

### socket.gethostbyaddr ( _ip\_address _)

Возвращает кортеж с 3 элементами `(hostname, aliaslist, ipaddrlist)`, где _**hostname**_ - это имя основного хоста, отвечающее на заданный _**ip\_address**_, _**aliaslist**_ - (возможно, пустой) список альтернативных имен хостов для того же адреса, а _**ipaddrlist**_ - это список адресов IPv4/v6 для одного и того же интерфейса на одном и том же хосте (скорее всего, содержащего только один адрес). Чтобы найти полное доменное имя, используйте функцию [getfqdn ()](socket.getfqdn.md). **gethostbyaddr ()** поддерживает как IPv4, так и IPv6.

Вызывает событие аудита `socket.gethostbyaddr` с аргументом _**ip\_address**_.

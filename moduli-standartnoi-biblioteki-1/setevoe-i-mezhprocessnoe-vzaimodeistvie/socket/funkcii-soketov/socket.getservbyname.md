# socket.getservbyname ()

### socket.getservbyname ( _servicename _\[, _protocolname _] )

Преобразует имя интернет-службы и имя протокола в номер порта для этой службы. Необязательное имя протокола, если указано, должно быть `'tcp'` или `'udp'`, в противном случае будет совпадать любой протокол.

Вызывает событие аудита `socket.getservbyname` с аргументами _**servicename**_, _**protocolname**_.

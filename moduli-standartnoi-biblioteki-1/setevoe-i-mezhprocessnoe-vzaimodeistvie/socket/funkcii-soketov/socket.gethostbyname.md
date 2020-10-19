# socket.gethostbyname \(\)

### socket.gethostbyname \( _hostname_ \)

Преобразует имя хоста в формат адреса IPv4. Адрес IPv4 возвращается в виде строки, например `'100.50.200.5'`. Если имя хоста является IPv4-адресом, оно возвращается без изменений. См. [gethostbyname\_ex \(\)](socket.gethostbyname_ex.md) для более полного интерфейса. **gethostbyname \(\)** не поддерживает разрешение имен IPv6, а [getaddrinfo \(\)](socket.getaddrinfo.md) следует использовать вместо этого для поддержки двойного стека IPv4/v6.

Вызывает событие аудита `socket.gethostbyname` с аргументом `hostname`.


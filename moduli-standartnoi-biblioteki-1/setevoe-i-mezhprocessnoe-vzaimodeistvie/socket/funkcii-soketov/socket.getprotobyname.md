# socket.getprotobyname \(\)

### socket.getprotobyname \( _protocolname_ \)

Преобразует имя интернет-протокола \(например, `'icmp'`\) в константу, подходящую для передачи в качестве \(необязательного\) третьего аргумента функции [socket \(\)](socket.socket.md). Обычно это требуется только для сокетов, открытых в «сыром» режиме \([SOCK\_RAW](../konstanty-soketov/socket.sock_raw.md)\); для обычных режимов сокета правильный протокол выбирается автоматически, если протокол пропущен или равен нулю.


# socket.connect \(\)

### socket.connect \( _address_ \)

Подключается к удаленному сокету по адресу _**address**_. \(Формат адреса зависит от семейства адресов - см. выше.\)

Если соединение прерывается сигналом, метод ожидает завершения соединения или вызывает [socket.timeout](../isklyucheniya-soketov/socket.timeout.md) по таймауту, если обработчик сигнала не вызывает исключение и сокет блокируется или имеет тайм-аут. Для неблокирующих сокетов метод вызывает исключение InterruptedError, если соединение прерывается сигналом \(или исключением, созданным обработчиком сигнала\).

Вызывает событие аудита `socket.connect` с аргументами `self`, `address`.

_Изменено в версии 3.5_: теперь метод ожидает завершения соединения вместо того, чтобы вызывать исключение InterruptedError, если соединение прерывается сигналом, обработчик сигнала не вызывает исключение и сокет блокируется или имеет тайм-аут \(см. [PEP 475](https://www.python.org/dev/peps/pep-0475/) для обоснования\).

### Пример

```python
sockobj.connect((serverHost, serverPort))
```

{% hint style="success" %}
Открывает соединение с компьютером и портом, где программа сервера ждет запросы на соединение от клиентов. В этом месте клиент указывает строку с именем службы, с которой ему необходимо связаться. Клиент может передать имя удаленного компьютера в виде доменного имени или числового IP-адреса. Можно также определить имя сервера как `localhost` \(или использовать эквивалентный ему IP-адрес `127.0.0.1`\), указав тем самым, что программа сервера выполняется на том же компьютере, что и клиент. Это удобно для отладки серверов без подключения к сети. Номер порта клиента должен в точности соответствовать номеру порта сервера. Адрес хоста/порта сервера передается методу в виде кортежа.
{% endhint %}




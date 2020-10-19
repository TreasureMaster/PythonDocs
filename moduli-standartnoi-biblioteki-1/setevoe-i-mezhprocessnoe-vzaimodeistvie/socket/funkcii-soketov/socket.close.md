# socket.close \(\)

### socket.close \( _fd_ \)

Закрывает дескриптор файла сокета. Это похоже на [os.close \(\)](../../../obshie-sluzhby-operacionnoi-sistemy/os/operacii-s-failovymi-deskriptorami/os.close.md), но для сокетов. На некоторых платформах \(наиболее заметно в Windows\) [os.close \(\)](../../../obshie-sluzhby-operacionnoi-sistemy/os/operacii-s-failovymi-deskriptorami/os.close.md) не работает для дескрипторов файлов сокетов.

_Новое в версии 3.7._


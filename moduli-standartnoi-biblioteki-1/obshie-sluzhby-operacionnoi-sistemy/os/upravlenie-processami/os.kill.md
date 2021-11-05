# os.kill ()

### os.kill ( _pid_, _sig _)

Отправляет сигнал _**sig**_ на _**pid**_ процесса. Константы для конкретных сигналов, доступных на платформе хоста, определены в модуле сигналов [signal](../../../setevoe-i-mezhprocessnoe-vzaimodeistvie/signal/).

**Windows**: сигналы [signal.CTRL\_C\_EVENT](../../../setevoe-i-mezhprocessnoe-vzaimodeistvie/signal/konstanty-signalov/signal.ctrl\_c\_event.md) и [signal.CTRL\_BREAK\_EVENT](../../../setevoe-i-mezhprocessnoe-vzaimodeistvie/signal/konstanty-signalov/signal.ctrl\_break\_event.md) являются специальными сигналами, которые могут быть отправлены только консольным процессам, которые совместно используют общее окно консоли, например, некоторым подпроцессам. Любое другое значение для _**sig**_ приведет к тому, что процесс будет безоговорочно завершен API-интерфейсом TerminateProcess, а код выхода будет установлен на _**sig**_. Версия **kill ()** для Windows дополнительно требует уничтожения дескрипторов процесса.

См. также [signal.pthread\_kill ()](../../../setevoe-i-mezhprocessnoe-vzaimodeistvie/signal/funkcii-modulya-signal/signal.pthread\_kill.md).

Вызывает событие аудита `os.kill` с аргументами _**pid**_, _**sig**_.

_Новое в версии 3.2:_ поддержка Windows.

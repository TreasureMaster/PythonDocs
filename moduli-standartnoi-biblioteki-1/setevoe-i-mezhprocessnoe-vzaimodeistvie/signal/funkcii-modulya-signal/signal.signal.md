# signal.signal \(\)

### signal.signal \( _signalnum_, _handler_ \)

Задает обработчик для сигнала _**signalnum**_ обработчику функции _**handler**_. _**handler**_ может быть вызываемым объектом Python, принимающим два аргумента \(см. ниже\), или одно из специальных значений [signal.SIG\_IGN](../konstanty-signalov/signal.sig_ign.md) или [signal.SIG\_DFL](../konstanty-signalov/signal.sig_dfl.md). Возвращает предыдущий обработчик сигнала \(см. описание [getsignal \(\)](signal.getsignal.md) выше\). \(Для получения дополнительной информации см. основную страницу [signal\(2\)](https://manpages.debian.org/buster/manpages-dev/signal.2.en.html) в Unix.\)

Когда потоки включены, эту функцию можно вызывать только из основного потока; попытка вызвать его из других потоков вызовет исключение ValueError.

_**handler**_ вызывается с двумя аргументами: номер сигнала и текущий кадр стека \(`None` или объект кадра; описание объектов кадра см. в описании иерархии типов или в описаниях атрибутов модуля [inspect](../../../sluzhby-sredy-vypolneniya-python/inspect.md)\).

В Windows **signal \(\)** можно вызывать только с [SIGABRT](../konstanty-signalov/signal.sigabrt.md), [SIGFPE](../konstanty-signalov/signal.sigfpe.md), [SIGILL](../konstanty-signalov/signal.sigill.md), [SIGINT](../konstanty-signalov/signal.sigint.md), [SIGSEGV](../konstanty-signalov/signal.sigsegv.md), [SIGTERM](../konstanty-signalov/signal.sigterm.md) или [SIGBREAK](../konstanty-signalov/signal.sigbreak.md). В любом другом случае возникнет ошибка ValueError. Обратите внимание, что не все системы определяют одинаковый набор имен сигналов; ошибка AttributeError будет вызвана, если имя сигнала не определено как константа уровня модуля SIG \*.

{% hint style="success" %}
Лутц \(ред.4\): Принимает номер сигнала, объект функции и устанавливает эту функцию в качестве обработчика сигнала с данным номером. Интерпретатор Python автоматически восстанавливает большинство обработчиков сигналов, когда они возникают, поэтому нет необходимости повторно вызывать эту функцию внутри самого обработчика сигнала, чтобы заново его зарегистрировать. То есть обработчики всех сигналов, за исключением сигнала [SIGCHLD](../konstanty-signalov/signal.sigchld.md), остаются установленными, пока не будут сброшены явно \(например, путем установки его в значение [SIG\_DFL](../konstanty-signalov/signal.sig_dfl.md), чтобы восстановить режим по умолчанию, или в значение [SIG\_IGN](../konstanty-signalov/signal.sig_ign.md), чтобы игнорировать сигнал\). Поведение сигнала [SIGCHLD](../konstanty-signalov/signal.sigchld.md) зависит от платформы.
{% endhint %}


# signal.pause \(\)

### signal.pause \(\)

Заставляет процесс засыпать до получения сигнала; тогда будет вызван соответствующий обработчик. Ничего не возвращает.

**Доступность**: Unix. См. справочную страницу [signal\(2\)](https://manpages.debian.org/buster/manpages-dev/signal.2.en.html) для получения дополнительной информации.

Смотрите также [sigwait \(\)](signal.sigwait.md), [sigwaitinfo \(\)](signal.sigwaitinfo.md), [sigtimedwait \(\)](signal.sigtimedwait.md) и [sigpending \(\)](signal.sigpending.md).

{% hint style="success" %}
Лутц \(ред.4\): Приостанавливает процесс, пока не будет перехвачен следующий сигнал. Функция [time.sleep](../../../obshie-sluzhby-operacionnoi-sistemy/time/funkcii-time/time.sleep.md) действует аналогично, но не работает с сигналами в моей системе Linux, - она генерирует ошибку прерванного системного вызова. Цикл `while True: pass` тоже остановит сценарий, но будет напрасно тратить ресурсы процессора.
{% endhint %}


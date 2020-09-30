# signal

### Устанавливает обработчики для асинхронных событий

Этот модуль предоставляет механизмы для использования обработчиков сигналов в Python.

### Общие правила

Функция [signal.signal \(\)](funkcii-modulya-signal/signal.signal.md) позволяет определять пользовательские обработчики, которые будут выполняться при получении сигнала. Установлено небольшое количество обработчиков по умолчанию: [SIGPIPE](konstanty-signalov/signal.sigpipe.md) игнорируется \(поэтому об ошибках записи в каналах и сокетах можно сообщать как об обычных исключениях Python\), а [SIGINT](konstanty-signalov/signal.sigint.md) преобразуется в исключение KeyboardInterrupt, если родительский процесс не изменил его.

После установки обработчик для конкретного сигнала остается установленным до его явного сброса \(Python эмулирует интерфейс стиля BSD независимо от базовой реализации\), за исключением обработчика для [SIGCHLD](konstanty-signalov/signal.sigchld.md), который следует базовой реализации.

### Выполнение обработчиков сигналов Python

Обработчик сигналов Python не выполняется внутри обработчика сигналов низкого уровня \(C\). Вместо этого обработчик сигналов низкого уровня устанавливает флаг, который сообщает виртуальной машине выполнить соответствующий обработчик сигнала Python в более поздний момент \(например, в следующей инструкции байт-кода\). Это имеет последствия:

* Бессмысленно отлавливать синхронные ошибки, такие как [SIGFPE](konstanty-signalov/signal.sigfpe.md) или [SIGSEGV](konstanty-signalov/signal.sigsegv.md), вызванные недопустимой операцией в коде C. Python вернется из обработчика сигнала в код C, который, вероятно, снова вызовет тот же сигнал, что приведет к зависанию Python. Начиная с Python 3.3, вы можете использовать модуль обработки ошибок для сообщения о синхронных ошибках.
* Долговременные вычисления, реализованные исключительно на C \(например, сопоставление регулярных выражений для большого объема текста\), могут выполняться непрерывно в течение произвольного количества времени, независимо от полученных сигналов. Обработчики сигналов Python будут вызваны по окончании вычислений.

### Сигналы и потоки

Обработчики сигналов Python всегда выполняются в основном потоке Python, даже если сигнал был получен в другом потоке. Это означает, что сигналы нельзя использовать как средство межпоточного взаимодействия. Вместо этого вы можете использовать примитивы синхронизации из модуля [threading](../../parallelnoe-vypolnenie/threading/).

Кроме того, только основной поток может устанавливать новый обработчик сигнала.

### Содержание модуля

_Изменено в версии 3.5_: перечисленные ниже константы, связанные с сигналом \(SIG\*\), обработчиком \([SIG\_DFL](konstanty-signalov/signal.sig_dfl.md), [SIG\_IGN](konstanty-signalov/signal.sig_ign.md)\) и sigmask \([SIG\_BLOCK](konstanty-signalov/signal.sig_block.md), [SIG\_UNBLOCK](konstanty-signalov/signal.sig_unblock.md), [SIG\_SETMASK](konstanty-signalov/signal.sig_setmask.md)\), были преобразованы в перечисления [enums](../../specialnye-tipy-dannykh/enum/soderzhanie-modulya/enum.intenum.md). Функции [getsignal \(\)](funkcii-modulya-signal/signal.getsignal.md), [pthread\_sigmask \(\)](funkcii-modulya-signal/signal.pthread_sigmask.md), [sigpending \(\)](funkcii-modulya-signal/signal.sigpending.md) и [sigwait \(\)](funkcii-modulya-signal/signal.sigwait.md) возвращают удобочитаемые перечисления [enums](../../specialnye-tipy-dannykh/enum/soderzhanie-modulya/enum.intenum.md).

В модуле **signal** определены следующие переменные:

* [signal.SIG\_DFL](konstanty-signalov/signal.sig_dfl.md) - выполняет функцию по умолчанию для сигнала
* [signal.SIG\_IGN](konstanty-signalov/signal.sig_ign.md) - обработчик просто игнорирует данный сигнал
* signal.SIGABRT
* [signal.SIGALRM](konstanty-signalov/signal.sigalrm.md) - сигнал таймера от alarm\(2\) в Unix
* signal.SIGBREAK
* signal.SIGBUS
* [signal.SIGCHLD](konstanty-signalov/signal.sigchld.md) - дочерний процесс остановлен или прекращен
* не заполнено...
* [signal.SIGUSR1](konstanty-signalov/signal.sigusr1.md) - определяемый пользователем сигнал 1
* [signal.SIGUSR2](konstanty-signalov/signal.sigusr2.md) - определяемый пользователем сигнал 2
* не заполнено...

Модуль **signal** определяет одно исключение:

* signal.ItimerError exception

Модуль signal определяет следующие функции:

* [signal.alarm \(\)](funkcii-modulya-signal/signal.alarm.md) - отправляет сигнал SIGALRM через указанное количество секунд
* signal.getsignal \(\)
* signal.strsignal \(\)
* signal. valid\_signals \(\)
* [signal.pause \(\)](funkcii-modulya-signal/signal.pause.md) - приостанавливает процесс, пока не будет перехвачен следующий сигнал
* не заполнено...
* signal.signal \(\)
* не заполнено...

### Пример

Вот минимальный пример программы. Он использует функцию [alarm \(\)](funkcii-modulya-signal/signal.alarm.md), чтобы ограничить время ожидания открытия файла; это полезно, если файл предназначен для последовательного устройства, которое не может быть включено, что обычно приводит к зависанию [os.open \(\)](../../obshie-sluzhby-operacionnoi-sistemy/os/operacii-s-failovymi-deskriptorami/os.open.md) на неопределенное время. Решение - установить 5-секундный сигнал тревоги перед открытием файла; если операция длится слишком долго, будет отправлен аварийный сигнал, и обработчик вызовет исключение.

```python
import signal, os

def handler(signum, frame):
    print('Signal handler called with signal', signum)
    raise OSError("Couldn't open device!")

# Установите обработчик сигнала и 5-секундный будильник
signal.signal(signal.SIGALRM, handler)
signal.alarm(5)

# Этот open () может зависать бесконечно
fd = os.open('/dev/ttyS0', os.O_RDWR)

signal.alarm(0)          # Отключить будильник
```

### Примечание для SIGPIPE

Передача вывода вашей программы по конвейеру таким инструментам, как [head\(1\)](https://manpages.debian.org/buster/coreutils/head.1.en.html), вызовет отправку сигнала [SIGPIPE](konstanty-signalov/signal.sigpipe.md) вашему процессу, когда приемник его стандартного вывода закроется раньше. Это приводит к возникновению исключения, например `BrokenPipeError: [Errno 32] Broken pipe`. Чтобы обработать этот случай, оберните вашу точку входа, чтобы перехватить это исключение, следующим образом:

```python
import os
import sys

def main():
    try:
        # имитировать большой вывод (ваш код заменяет этот цикл)
        for x in range(10000):
            print("y")
        # очистить вывод здесь, чтобы принудительно запустить SIGPIPE
        # находясь внутри этого блока try.
        sys.stdout.flush()
    except BrokenPipeError:
        # Python сбрасывает стандартные потоки при выходе;
        # перенаправить оставшийся вывод на devnull,
        # чтобы избежать еще одной BrokenPipeError при завершении работы
        devnull = os.open(os.devnull, os.O_WRONLY)
        os.dup2(devnull, sys.stdout.fileno())
        sys.exit(1)  # Python выходит с кодом ошибки 1 на EPIPE

if __name__ == '__main__':
    main()
```

Не устанавливайте для [SIGPIPE](konstanty-signalov/signal.sigpipe.md) значение [SIG\_DFL](konstanty-signalov/signal.sig_dfl.md), чтобы избежать ошибки BrokenPipeError. Это может привести к неожиданному завершению вашей программы также всякий раз, когда какое-либо соединение сокета прерывается, пока ваша программа все еще пишет в него.


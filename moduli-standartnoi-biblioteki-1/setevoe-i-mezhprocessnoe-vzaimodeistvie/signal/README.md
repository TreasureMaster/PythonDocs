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


# os.environ

#### os.environ

Объект сопоставления, представляющий строковое окружение. Например, `environment['HOME']` - это путь к вашему домашнему каталогу \(на некоторых платформах\) и эквивалентен `getenv("HOME")` в C.

Это сопоставление фиксируется при первом импорте модуля [os](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os), обычно во время запуска Python в рамках обработки `site.py`. Изменения среды, внесенные после этого времени, не отражаются в `os.environ`, за исключением изменений, внесенных путем непосредственного изменения `os.environ`.

Если платформа поддерживает функцию [putenv \(\)](os.putenv.md), это сопоставление можно использовать для изменения среды, а также для запроса среды. [putenv \(\)](os.putenv.md) будет вызываться автоматически при изменении сопоставления.

В Unix ключи и значения используют [sys.getfilesystemencoding \(\)](../../../sluzhby-sredy-vypolneniya-python/sys/sys.getfilesystemencoding.md) и обработчик ошибок `'surrogateescape'`. Используйте environb, если хотите использовать другую кодировку.

{% hint style="info" %}
Прямой вызов [putenv \(\)](os.putenv.md) не меняет _**os.environ**_, поэтому лучше изменить _**os.environ**_.
{% endhint %}

{% hint style="info" %}
На некоторых платформах, включая FreeBSD и Mac OS X, настройка среды может вызвать утечку памяти. Обратитесь к системной документации для putenv \(\).
{% endhint %}

Если [putenv \(\)](os.putenv.md) не предоставляется, измененная копия этого сопоставления может быть передана в соответствующие функции создания процесса, чтобы дочерние процессы использовали измененную среду.

Если платформа поддерживает функцию [unsetenv \(\)](os.unsetenv.md), вы можете удалить элементы в этом сопоставлении, чтобы сбросить переменные среды. [unsetenv \(\)](os.unsetenv.md) будет вызываться автоматически при удалении элемента из **os.environ** и при вызове одного из методов `pop ()` или `clear ()`.

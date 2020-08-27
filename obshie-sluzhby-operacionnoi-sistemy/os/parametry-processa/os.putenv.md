# os.putenv \(\)

#### os.putenv \( _key_, _value_ \)

Задает для переменной среды с именем _**key**_ строковое значение. Такие изменения в среде влияют на подпроцессы, запущенные с помощью [os.system \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.system), [os.popen \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/os.popen) или os.fork \(\) и os.execv \(\).

**Доступность**: большинство разновидностей Unix, Windows.

{% hint style="info" %}
На некоторых платформах, включая FreeBSD и Mac OS X, настройка `environ` может вызвать утечку памяти. Обратитесь к системной документации для **putenv**.
{% endhint %}

Когда поддерживается **putenv \(\)**, назначения элементам в [os.environ](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/os/environ) автоматически переводятся в соответствующие вызовы **putenv \(\)**; однако вызовы **putenv \(\)** не обновляют `os.environ`, поэтому на самом деле предпочтительнее назначать элементы `os.environ`.

Вызывает событие проверки **os.putenv** с аргументами _**key**_, _**value**_.


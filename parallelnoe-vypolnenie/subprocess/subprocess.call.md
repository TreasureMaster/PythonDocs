# subprocess.call \(\)

#### subprocess.call \( _args_, _\*_, _stdin=None_, _stdout=None_, _stderr=None_, _shell=False_, _cwd=None_, _timeout=None_, _\*\*other\_popen\_kwargs_ \)

Запускает команду, описанную _**args**_. Ожидает завершения команды, затем возвращает атрибут кода возврата [returncode](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.returncode).

Код, которому необходимо захватить [**stdout**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stdout) или [**stderr**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stderr), должен вместо этого использовать run \(\):

```python
run(...).returncode
```

Чтобы подавить [**stdout**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stdout) или [**stderr**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stderr), укажите значение DEVNULL.

Приведенные выше аргументы - лишь некоторые общие. Полная сигнатура функции такая же, как у конструктора [**Popen**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/subprocess.popen) - эта функция передает все предоставленные аргументы, кроме _**timeout**_, непосредственно через этот интерфейс.

{% hint style="info" %}
Не используйте `stdout = PIPE` или `stderr = PIPE` с этой функцией. Дочерний процесс будет заблокирован, если он сгенерирует достаточно вывода для канала, чтобы заполнить буфер канала ОС, поскольку каналы не читаются.
{% endhint %}

_Изменено в версии 3.3:_ добавлен _**timeout**_.


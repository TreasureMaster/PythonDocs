# Popen.wait \(\)

#### Popen.wait \( _timeout=None_ \)

Ожидает, пока дочерний процесс завершится. Устанавливает и возвращает атрибут [Popen.returncode](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.returncode).

Если процесс не завершается после истечения _**timeout**_ секунд, вызывает исключение TimeoutExpired. Это исключение можно безопасно перехватить и повторить ожидание.

{% hint style="info" %}
Это приведет к взаимной блокировке при использовании `stdout = PIPE` или `stderr = PIPE`, и дочерний процесс генерирует достаточно вывода для канала, так что он блокирует ожидание, пока буфер канала ОС не примет больше данных. Используйте [Popen.communicate \(\)](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.communicate) при использовании каналов, чтобы этого избежать.
{% endhint %}

{% hint style="info" %}
Функция реализована с использованием цикла занятости \(неблокирующий вызов и короткие засыпания\). Используйте модуль asyncio для асинхронного ожидания: см. asyncio.create\_subprocess\_exec.
{% endhint %}

_Изменено в версии 3.3:_ добавлен _**timeout**_.


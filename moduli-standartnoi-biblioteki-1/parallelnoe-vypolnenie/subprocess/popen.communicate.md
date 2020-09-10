# Popen.communicate \(\)

#### Popen.communicate \( _input=None_, _timeout=None_ \)

Взаимодействие с процессом: отправка данных на стандартный ввод [**stdin**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stdin). Читает данные из [**stdout**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stdout) и [**stderr**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stderr), пока не будет достигнут конец файла. Подождите, пока процесс завершится, и установится атрибут [returncode](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.returncode). Необязательный аргумент _**input**_ должен быть данными для отправки дочернему процессу или `None`, если данные не должны отправляться дочернему процессу. Если потоки были открыты в текстовом режиме, _**input**_ должен быть строкой. В противном случае это должны быть байты.

**communicate \(\)** возвращает кортеж `(stdout_data, stderr_data)`. Данные будут строками, если потоки открывались в текстовом режиме; в противном случае байты.

Обратите внимание: если вы хотите отправлять данные на стандартный ввод процесса [**stdin**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.stdin), вам необходимо создать объект [**Popen**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/subprocess.popen) с помощью `stdin = PIPE`. Точно так же, чтобы получить в результирующем кортеже что-либо, кроме `None`, вам также необходимо указать `stdout = PIPE` и / или `stderr = PIPE`.

Если процесс не завершится по истечении _**timeout**_ секунд ожидания, будет возбуждено исключение TimeoutExpired. Перехват этого исключения и повторная попытка связи не приведет к потере вывода.

Дочерний процесс не уничтожается, если истекает _**timeout**_, поэтому для правильной очистки приложение с хорошим поведением должно убить дочерний процесс и завершить обмен данными:

```python
proc = subprocess.Popen(...)
try:
    outs, errs = proc.communicate(timeout=15)
except TimeoutExpired:
    proc.kill()
    outs, errs = proc.communicate()
```

{% hint style="info" %}
Считанные данные буферизуются в памяти, поэтому не используйте этот метод, если размер данных большой или неограниченный.
{% endhint %}

_Изменено в версии 3.3:_ добавлен _**timeout**_.


# Popen.stderr

#### Popen.stderr

Если аргумент _**stderr**_ был равен [**PIPE**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/subprocess.pipe), этот атрибут является читаемым объектом потока, возвращенным open \(\). Чтение из потока обеспечивает вывод ошибок дочернего процесса. Если были указаны аргументы _**encoding**_ или _**errors**_ или аргумент _**universal\_newlines**_ был равен `True`, поток является текстовым потоком, в противном случае это поток байтов. Если аргумент _**stderr**_ не был равен **PIPE**, этот атрибут имеет значение `None`.

{% hint style="danger" %}
Используйте функцию [`communicate ()`](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/popen.communicate) вместо `.stdin.write`, `.stdout.read` или `.stderr.read`, чтобы избежать взаимоблокировок из-за того, что какой-либо из других буферов канала ОС заполняется и блокирует дочерний процесс.
{% endhint %}

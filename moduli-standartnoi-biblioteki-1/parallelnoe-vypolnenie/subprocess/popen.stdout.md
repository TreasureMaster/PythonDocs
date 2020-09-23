# Popen.stdout

#### Popen.stdout

Если аргумент _**stdout**_ равен [**PIPE**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/subprocess.pipe), этот атрибут является читаемым объектом потока, возвращенным функцией open \(\). Чтение из потока обеспечивает вывод дочернего процесса. Если были указаны аргументы _**encoding**_ или _**errors**_ или аргумент _**universal\_newlines**_ был `True`, поток является текстовым потоком, в противном случае это поток байтов. Если аргумент _**stdout**_ не был равен **PIPE**, этот атрибут имеет значение `None`.

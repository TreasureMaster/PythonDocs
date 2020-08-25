# Popen.stdin

#### Popen.stdin

Если аргумент _**stdin**_ был [**PIPE**](https://treasuremaster.gitbook.io/python-docs/parallelnoe-vypolnenie/subprocess/subprocess.pipe), этот атрибут является записываемым объектом потока, возвращенным open \(\). Если были указаны аргументы _**encoding**_ или _**errors**_ или аргумент _**universal\_newlines**_ был `True`, поток является текстовым потоком, в противном случае это поток байтов. Если аргумент _**stdin**_ не был **PIPE**, этот атрибут имеет значение `None`.


# io.StringIO

#### class io.StringIO \( _initial\_value=''_, _newline='\n'_  \)

Поток в памяти для текстового ввода-вывода. Текстовый буфер удаляется при вызове метода close \(\).

Начальное значение буфера можно установить, указав _**initial\_value**_. Если перевод новой строки включен, новые строки будут закодированы, как если бы с помощью write \(\). Поток располагается в начале буфера.

Аргумент _**newline**_ работает аналогично TextIOWrapper. По умолчанию в качестве концов строк рассматриваются только символы  `'\n'` и не выполняется перевод новой строки. Если для _**newline**_ установлено значение `None`, новые строки записываются как  `'\n'` на всех платформах, но универсальное декодирование новой строки по-прежнему выполняется при чтении.

**StringIO** предоставляет этот метод в дополнение к методам [TextIOBase](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.textiobase) и его родителей:

* [getvalue \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.stringio/io.stringio.getvalue) - метод возвращает строку, содержащую все содержимое буфера

Пример использования:

```python
import io

output = io.StringIO()
output.write('First line.\n')
print('Second line.', file=output)

# Получить содержимое файла -- это будет
# 'First line.\nSecond line.\n'
contents = output.getvalue()

# Закрыть объект и сбросить буфер памяти --
# .getvalue() теперь вызовет исключение.
output.close()
```


# io.BytesIO

#### class io.BytesIO \( \[_initial\_bytes_\] \)

Реализация потока с использованием байтового буфера в памяти. Он наследует BufferedIOBase. Буфер удаляется при вызове метода close \(\).

Необязательный аргумент _**initial\_bytes**_ - это байтовый объект \(_bytes-like object_ \), содержащий начальные данные.

**BytesIO** предоставляет или переопределяет эти методы в дополнение к методам из [BufferedIOBase](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bufferediobase) и IOBase:

* getbuffer \(\)
* [getvalue \(\)](https://treasuremaster.gitbook.io/python-docs/obshie-sluzhby-operacionnoi-sistemy/io/io.bytesio/io.bytesio.getvalue) - возвращает все байты, содержащиеся в буфере
* read1 \(\)
* readinto1 \(\)


# io.BufferedReader

### io.BufferedReader \( _raw_, _buffer\_size=DEFAULT\_BUFFER\_SIZE_ \)

Буфер, обеспечивающий доступ более высокого уровня к читаемому последовательному объекту [RawIOBase](../io.rawiobase/). Он наследует [BufferedIOBase](../io.bufferediobase/). При чтении данных из этого объекта может быть запрошен больший объем данных из базового необработанного потока и сохранен во внутреннем буфере. Буферизованные данные могут быть возвращены непосредственно при последующих чтениях.

Конструктор создает **BufferedReader** для данного читаемого необработанного потока _**raw**_ и _**buffer\_size**_. Если _**buffer\_size**_ не указан, используется [**DEFAULT\_BUFFER\_SIZE**](../vysokourovnevyi-interfeis-modulya/io.default_buffer_size.md).

**BufferedReader** предоставляет или переопределяет эти методы в дополнение к методам из [BufferedIOBase](../io.bufferediobase/) и [IOBase](../io.iobase/):

* peek \(\)
* [read \(\)](io.bufferedreader.read.md) - читает и возвращает количество байтов заданного размера
* read1 \(\)


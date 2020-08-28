# io.BufferedWriter

### io.BufferedWriter \( _raw_, _buffer\_size=DEFAULT\_BUFFER\_SIZE_ \)

Буфер, обеспечивающий доступ более высокого уровня к записываемому последовательному объекту [RawIOBase](../io.rawiobase/). Он наследует [BufferedIOBase](../io.bufferediobase/). При записи в этот объект данные обычно помещаются во внутренний буфер. Буфер будет записан в базовый объект [RawIOBase](../io.rawiobase/) при различных условиях, включая:

* когда буфер становится слишком маленьким для всех ожидающих данных
* когда вызывается [flush \(\)](io.bufferedwriter.flush.md)
* когда запрашивается `seek ()` \(для объектов [BufferedRandom](../io.bufferedrandom.md)\)
* когда объект **BufferedWriter** закрывается или уничтожается

Конструктор создает **BufferedWriter** для данного записываемого необработанного потока. Если _**buffer\_size**_ не указан, по умолчанию используется [**DEFAULT\_BUFFER\_SIZE**](../vysokourovnevyi-interfeis-modulya/io.default_buffer_size.md).

**BufferedWriter** предоставляет или переопределяет эти методы в дополнение к методам из [BufferedIOBase](../io.bufferediobase/) и [IOBase](../io.iobase/):

* [flush \(\)](io.bufferedwriter.flush.md) - переводит байты, хранящиеся в буфере в необработанный поток
* [write \(\)](io.bufferedwriter.write.md) - записывает байтовый поток и возвращает количество записанных байтов


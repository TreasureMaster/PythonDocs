# time

### Доступ к времени и его преобразования

Этот модуль предоставляет различные функции, связанные со временем. Для связанных функций см. также модули [datetime](../specialnye-tipy-dannykh/datetime.md) и [calendar](../specialnye-tipy-dannykh/calendar.md).

Хотя этот модуль доступен всегда, не все функции доступны на всех платформах. Большинство функций, определенных в этом модуле, вызывают функции библиотеки C с тем же именем. Иногда может быть полезно обратиться к документации платформы, поскольку семантика этих функций различается для разных платформ.

Необходимо пояснение некоторых терминов и условностей.

* _**epoch**_ - это точка, в которой время начинается, и зависит от платформы. Для Unix эпоха - 1 января 1970 г., 00:00:00 \(UTC\). Чтобы узнать, какая эпоха на данной платформе, посмотрите на `time.gmtime (0)`
* Термин «[секунды с начала эпохи](https://en.wikipedia.org/wiki/Leap_second)» относится к общему количеству секунд, прошедших с начала эпохи, обычно без учета дополнительных секунд. Дополнительные секунды исключаются из этого общего количества на всех POSIX-совместимых платформах
* Функции в этом модуле могут не обрабатывать даты и время до эпохи или далеко в будущем. Точка отсечения в будущем определяется библиотекой C; для 32-битных систем это обычно 2038 год
* 

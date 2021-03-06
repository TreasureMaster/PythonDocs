# time.time \(\)

### time.time \(\) -&gt; _float_

Возвращает время в секундах с начала эпохи в виде числа с плавающей запятой. Конкретная дата эпохи и обработка [дополнительных секунд](https://en.wikipedia.org/wiki/Leap_second) зависят от платформы. В Windows и большинстве систем Unix эпохой является 1 января 1970 г., 00:00:00 \(UTC\), и дополнительные секунды не засчитываются во время в секундах, прошедшее с начала эпохи. Это обычно называют [временем Unix](https://en.wikipedia.org/wiki/Unix_time). Чтобы узнать, какая эпоха на данной платформе, посмотрите на `gmtime (0)`.

Обратите внимание, что даже несмотря на то, что время всегда возвращается как число с плавающей запятой, не все системы обеспечивают время с большей точностью, чем 1 секунда. Хотя эта функция обычно возвращает неубывающие значения, она может возвращать более низкое значение, чем предыдущий вызов, если системные часы были установлены обратно между двумя вызовами.

Число, возвращаемое функцией **time \(\)**, может быть преобразовано в более общий формат времени \(например, год, месяц, день, час и т. д.\) В формате UTC, передав его в функцию [gmtime \(\)](time.gmtime.md), или в местное время, передав его в [localtime \( \)](time.localtime.md) функция. В обоих случаях возвращается объект [struct\_time](time.struct_time.md), из которого можно получить доступ к компонентам календарной даты как к атрибутам.


# pickle

Модуль pickle реализует двоичные протоколы для сериализации и десериализации структуры объекта Python. «Pickling» - это процесс, посредством которого иерархия объектов Python преобразуется в поток байтов, а «unpickling» - обратная операция, посредством которой поток байтов \(из двоичного файла или объекта, похожего на байты\) преобразуется обратно в иерархию объектов. Pickling \(и unpickling\) также известно как «сериализация», «сортировка» или «выравнивание»; однако во избежание путаницы здесь используются термины «сериализация» и «десериализация».

{% hint style="danger" %}
**Предупреждение**

Модуль **pickle** не безопасен. Распаковывайте данные, только которым вы доверяете. Не загружайте с помощью модуля pickle файлы из ненадёжных источников. Это может привести к необратимым последствиям. Попробуйте подписать данные с помощью hmac, если вам нужно убедиться, что они не были подделаны. Более безопасные форматы сериализации, такие как json, могут быть более подходящими, если вы обрабатываете ненадежные данные. Смотрите Сравнение с JSON.
{% endhint %}

#### Отношение к другим модулям Python

#### Формат потока данных

#### Интерфейс модуля pickle

Чтобы сериализовать иерархию объектов, вы просто вызываете функцию dumps \(\). Аналогично, для десериализации потока данных вы вызываете функцию load \(\). Однако, если вы хотите больше контролировать сериализацию и десериализацию, вы можете создать объект Pickler или Unpickler соответственно.

Модуль pickle предоставляет следующие константы:

* \*\*\*\*[**pickle.HIGHEST\_PROTOCOL**](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/highest_protocol) - самая высокая доступная версия протокола.
* \*\*\*\*[**pickle.DEFAULT\_PROTOCOL**](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/default_protocol) - версия протокола по умолчанию.

Модуль pickle включает следующие функции, чтобы сделать процесс сериализации удобным:

* [dump \(\)](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/dump) - записывает сериализованный объект в файл.
* [dumps \(\)](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/dumps) - возвращает сериализованный объект.
* [load \(\)](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/load) - загружает объект из файла.
* [loads \(\)](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/loads) - загружает объект из потока байт.

Модуль pickle определяет следующие исключения:

* [pickle.PickleError](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/pickleerror) - общий класс исключений сериализации.
* [pickle.PicklingError](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/picklingerror) - возникает, когда Pickler принимает несериализуемый объект.
* [pickle.UnpicklingError](https://treasuremaster.gitbook.io/python-docs/khranenie-dannykh/pickle/unpicklingerror) - возникает при невозможности десериализации объекта.

Модуль pickle экспортирует 3 класса:

* pickle.Pickler - используется для записи сериализованных данных в двоичный файл.
* pickle.Unpickler - используется для чтения сериализованных данных из двоичного файла.
* pickle.PickleBuffer - оболочка для буфера, представляющего извлекаемые данные.


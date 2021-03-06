# mmap

### Поддержка файлов с отображением памяти

Отображенные в память файловые объекты ведут себя как байтовые массивы, так и файловые объекты. Вы можете использовать объекты **mmap** в большинстве мест, где ожидается bytearray; например, вы можете использовать модуль [re](../obrabotka-teksta/re/) для поиска в файле с отображением в память. Вы также можете изменить один байт, выполнив `obj [index] = 97`, или изменить подпоследовательность, присвоив срезу: `obj [i1: i2] = b '...'`. Вы также можете читать и записывать данные, начиная с текущей позиции файла, и `seek()` через файл в разные позиции.

Файл с отображением памяти создается конструктором **mmap**, который отличается в Unix и Windows. В любом случае вы должны предоставить файловый дескриптор для файла, открытого для обновления. Если вы хотите отобразить существующий файловый объект Python, используйте его метод `fileno ()`, чтобы получить правильное значение для параметра _**fileno**_. В противном случае вы можете открыть файл с помощью функции [os.open \(\)](../obshie-sluzhby-operacionnoi-sistemy/os/operacii-s-failovymi-deskriptorami/os.open.md), которая напрямую возвращает дескриптор файла \(после завершения файл все равно необходимо закрыть\).

{% hint style="info" %}
Если вы хотите создать отображение памяти для буферизованного файла с возможностью записи, вы должны сначала использовать [flush \(\)](../obshie-sluzhby-operacionnoi-sistemy/io/io.iobase/io.iobase.flush.md) файл. Это необходимо, чтобы гарантировать, что локальные модификации буферов действительно доступны для отображения.
{% endhint %}

Для версий конструктора как для Unix, так и для Windows доступ может быть указан как необязательный параметр ключевого слова. _**access**_ принимает одно из четырех значений: ACCESS\_READ, ACCESS\_WRITE или ACCESS\_COPY, чтобы указать память только для чтения, сквозную запись или копирование при записи соответственно, или ACCESS\_DEFAULT, чтобы отложить до _**prot**_. _**access**_ можно использовать как в Unix, так и в Windows. Если _**access**_ не указан, Windows **mmap** возвращает отображение со сквозной записью. Начальные значения памяти для всех трех типов доступа берутся из указанного файла. Назначение карте памяти ACCESS\_READ вызывает исключение TypeError. Назначение карте памяти ACCESS\_WRITE влияет как на память, так и на базовый файл. Назначение карте памяти ACCESS\_COPY влияет на память, но не обновляет базовый файл.

_Изменено в версии 3.7_: Добавлена константа ACCESS\_DEFAULT.

Чтобы отобразить анонимную память, в качестве fileno необходимо передать `-1` вместе с длиной.

### Классы mmap

* mmap.mmap class Windows
* mmap.mmap class Unix

Отображенные в память файловые объекты поддерживают следующие методы:

* mmap.close \(\)
* mmap.closed
* mmap.find \(\)
* mmap.flush \(\)
* mmap.madvise \(\)
* mmap.move \(\)
* mmap.read \(\)
* mmap.read\_byte \(\)
* mmap.readline \(\)
* mmap.resize \(\)
* mmap.rfind \(\)
* mmap.seek \(\)
* mmap.size \(\)
* mmap.tell \(\)
* mmap.write \(\)
* mmap.write\_byte \(\)

### Константы MADV\_\*


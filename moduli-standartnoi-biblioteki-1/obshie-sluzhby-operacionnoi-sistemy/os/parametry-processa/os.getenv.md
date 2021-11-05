# os.getenv ()

#### os.getenv ( _key_, _default=None _)

Возвращает значение _**key**_ переменной среды, если он существует, или значение _**default**_, если его нет. _**key**_, _**default**_ и результат - str.

В Unix ключи и значения декодируются с помощью [sys.getfilesystemencoding ()](../../../sluzhby-sredy-vypolneniya-python/sys/sys.getfilesystemencoding.md) и обработчика ошибок `'surrogateescape'`. Используйте [os.getenvb ()](os.getenvb.md), если хотите использовать другую кодировку.

**Доступность**: большинство разновидностей Unix, Windows.

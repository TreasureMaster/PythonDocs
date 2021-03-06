# os.chdir \(\)

### os.chdir \( _path_ \)

Изменяет текущий рабочий каталог на _**path**_.

Эта функция может поддерживать указание дескриптора файла. Дескриптор должен ссылаться на открытый каталог, а не на открытый файл.

Эта функция может вызывать OSError и такие подклассы, как FileNotFoundError, PermissionError и NotADirectoryError.

Вызывает событие аудита `os.chdir` с аргументом _**path**_.

_Новое в версии 3.3:_ добавлена поддержка указания пути в качестве дескриптора файла на некоторых платформах.

_Изменено в версии 3.6:_ Принимает объект, подобный пути \(_path-like object_\).


# io.IOBase.close \(\)

### io.IOBase.close \(\)

Выталкивает и закрывает поток. Этот метод не действует, если файл уже закрыт. После закрытия файла любая операция с файлом \(например, чтение или запись\) вызовет ошибку ValueError.

Для удобства этот метод можно вызывать более одного раза; однако только первый вызов будет иметь эффект.

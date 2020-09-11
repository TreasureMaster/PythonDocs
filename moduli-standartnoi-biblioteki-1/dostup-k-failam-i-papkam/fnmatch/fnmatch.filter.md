# fnmatch.filter \(\)

### fnmatch.filter \( _names_, _pattern_ \)

Возвращает подмножество списка имен _**names**_, соответствующих шаблону _**pattern**_. Это то же самое, что `[n for n in names if fnmatch (n, pattern)]`, но реализовано более эффективно.


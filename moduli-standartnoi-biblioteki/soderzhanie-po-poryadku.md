# Содержание по порядку



#### Модули стандартной библиотеки

* [Обработка текста](../moduli-standartnoi-biblioteki-1/obrabotka-teksta/) - обработка строк и текста
  * string
  * re
  * difflib
  * textwrap
  * unicodedata
  * stringprep
  * readline
  * rlcompleter
* [Двоичные данные](../moduli-standartnoi-biblioteki-1/dvoichnye-dannye/) - базовые сервисные операции с двоичными данными
  * struct
  * codecs
* [Специальные типы данных](../moduli-standartnoi-biblioteki-1/specialnye-tipy-dannykh/) - различные типы данных \(дата, время, массивы, очереди и т.п.\)
  * datetime
  * calendar
  * collections
  * collections.abc
  * heapq
  * bisect
  * array
  * weakref
  * types
  * copy
  * pprint
  * reprlib
  * enum
* [Математические модули](../moduli-standartnoi-biblioteki-1/matematicheskie-moduli/) - числовые и математические функции и типы данных
  * numbers
  * math
  * cmath
  * decimal
  * fractions
  * random
  * statistics
* [Функциональные программные модули](../moduli-standartnoi-biblioteki-1/funkcionalnye-programmnye-moduli.md) - объекты для функционального программирования
  * itertools
  * functools
  * operator
* [Доступ к файлам и папкам](../moduli-standartnoi-biblioteki-1/dostup-k-failam-i-papkam/) - работа с файлами и каталогами
  * pathlib
  * os.path
  * fileinput
  * stat
  * filecmp
  * tempfile
  * glob
  * fnmatch
  * linecache
  * shutil
* [Хранение данных](../moduli-standartnoi-biblioteki-1/khranenie-dannykh/) - сериализация и хранение данных на диске
  * pickle
  * copyreg
  * shelve
  * marshal
  * dbm
  * sqlite3
* [Сжатие и архивирование данных](../moduli-standartnoi-biblioteki-1/szhatie-i-arkhivirovanie-dannykh.md) - сжатие данных и создание архивов
  * zlib
  * gzip
  * bz2
  * lzma
  * zipfile
  * tarfile
* [Форматы файлов](../moduli-standartnoi-biblioteki-1/formaty-failov/) - анализ различных форматов файлов
  * csv
  * configparser
  * netrc
  * xdrlib
  * plistlib
* [Криптографические службы](../moduli-standartnoi-biblioteki-1/kriptograficheskie-sluzhby.md) - алгоритмы криптографического характера
  * hashlib
  * hmac
  * secrets
* [Общие службы операционной системы](../moduli-standartnoi-biblioteki-1/obshie-sluzhby-operacionnoi-sistemy/) - интерфейсы к функциям операционной системы
  * os
  * io
  * time
  * argparse
  * getopt
  * logging
  * logging.config
  * logging.handlers
  * getpass
  * curses
  * curses.textpad
  * curses.ascii
  * curses.panel
  * platform
  * errno
  * ctypes
* [Параллельное выполнение](../moduli-standartnoi-biblioteki-1/parallelnoe-vypolnenie/) - одновременное выполнение кода в процессах или потоках
  * threading
  * multiprocessing
  * multiprocessing.shared\_memory
  * concurrent
  * concurrent.futures
  * subprocess
  * sched
  * queue
  * \_thread
  * \_dummy_\__thread
  * dummy\_threading
  * contextvars
* [Сетевое и межпроцессное взаимодействие](../moduli-standartnoi-biblioteki-1/setevoe-i-mezhprocessnoe-vzaimodeistvie/) - механизмы взаимодействия в сети/процессах
  * asyncio
  * socket
  * ssl
  * select
  * selectors
  * asyncore
  * asynchat
  * signal
  * mmap
* [Обработка интернет данных](../moduli-standartnoi-biblioteki-1/obrabotka-internet-dannykh.md) - обработка форматов данных, используемых в интернете
  * email
  * json
  * mailcap
  * mailbox
  * mimetypes
  * base64
  * binhex
  * binascii
  * quopri
  * uu
* [Обработка упорядоченной разметки](../moduli-standartnoi-biblioteki-1/obrabotka-uporyadochennoi-razmetki.md) - формы разметки структурированных данных
  * html
  * html.parser
  * html.entities
  * xml.etree.ElementTree
  * xml.dom
  * xml.dom.minidom
  * xml.dom.pulldom
  * xml.sax
  * xml.sax.handler
  * xml.sax.saxutils
  * xml.sax.xmlreader
  * xml.parsers.expat
* [Интернет протоколы](../moduli-standartnoi-biblioteki-1/internet-protokoly.md) - интернет-протоколы и соответствующие технологии
  * webbrowser
  * cgi
  * cgitb
  * wsgiref
  * urllib
  * urllib.request
  * urllib.response
  * urllib.parse
  * urllib.error
  * urllib.robotparser
  * http
  * http.client
  * ftplib
  * poplib
  * imaplib
  * nntplib
  * smtplib
  * smtpd
  * telnetlib
  * uuid
  * socketserver
  * http.server
  * http.cookies
  * http.cookiejar
  * xmlrpc
  * xmlrpc.client
  * xmlrpc.server
  * ipaddress
* [Мультимедиа службы](../moduli-standartnoi-biblioteki-1/multimedia-sluzhby.md) - алгоритмы и интерфейсы мультимедийных приложений
  * audioop
  * aifc
  * sunau
  * wave
  * chunk
  * colorsys
  * imghdr
  * sndhdr
  * ossaudiodev
* [Интернационализация](../moduli-standartnoi-biblioteki-1/internacionalizaciya.md) - адаптация к местным локали и языку
  * gettext
  * locale
* [Программные фреймворки](../moduli-standartnoi-biblioteki-1/programmnye-freimvorki.md) - задание структуры программы и интерфейсов командной строки
  * turtle
  * cmd
  * shlex
* [Графические интерфейсы пользователя с Tk](../moduli-standartnoi-biblioteki-1/graficheskie-interfeisy-polzovatelya-s-tk.md) - описание графического интерфейса tkinter
  * tkinter
  * tkinter.ttk
  * tkinter.tix
  * tkinter.scrolledtext
  * IDLE
  * Другие пакеты графических интерфейсов
* [Инструменты разработки](../moduli-standartnoi-biblioteki-1/instrumenty-razrabotki.md) - документирование, тестирование, декодирование кода
  * typing
  * pydoc
  * doctest
  * unittest
  * unittest.mock
  * 2to3
  * test
  * test.support
  * test.support.script\_helper
* [Отладка и профилирование](../moduli-standartnoi-biblioteki-1/otladka-i-profilirovanie.md) - отладчики, профилировщики и события аудита
  * Таблица событий аудита
  * bdb
  * faulthandler
  * pdb
  * Профилировщики Python
  * timeit
  * trace
  * tracemalloc
* [Упаковка и распространение программ](../moduli-standartnoi-biblioteki-1/upakovka-i-rasprostranenie-programm.md) - публикация и установка ПО на Python
  * distutils
  * ensurepip
  * venv
  * zipapp
* [Службы среды выполнения Python](../moduli-standartnoi-biblioteki-1/sluzhby-sredy-vypolneniya-python/) - взаимодействие интерпретатора Python со своей средой
  * sys
  * sysconfig
  * builtins
  * \_\_main\_\_
  * warnings
  * dataclasses
  * contextlib
  * abc
  * atexit
  * traceback
  * \_\_future\_\_
  * gc
  * inspect
  * site
* [Пользовательские интерпретаторы Python](../moduli-standartnoi-biblioteki-1/polzovatelskie-interpretatory-python.md) - интерфейсы интерактивного интерпретатора
  * code
  * codeop
* [Импортирование модулей](../moduli-standartnoi-biblioteki-1/importirovanie-modulei.md) - обработчики настройки процесса импорта модулей
  * zipimport
  * pkgutil
  * modulefinder
  * runpy
  * importlib
  * importlib.metadata
* [Службы языка Python](../moduli-standartnoi-biblioteki-1/sluzhby-yazyka-python.md) - разметка, синтаксический анализ и дизассемблирование байт-кода
  * parser
  * ast
  * symtable
  * symbol
  * token
  * keyword
  * tokenize
  * tabnanny
  * pyclbr
  * py\_compile
  * compileall
  * dis
  * pickletools
* [Разные службы](../moduli-standartnoi-biblioteki-1/raznye-sluzhby.md) - различные службы Python
  * formatter
* [Специальные службы MS Windows](../moduli-standartnoi-biblioteki-1/specialnye-sluzhby-ms-windows/) - модули платформы MS Windows
  * msilib
  * msvcrt
  * winreg
  * winsound
* [Специальные службы Unix](../moduli-standartnoi-biblioteki-1/specialnye-sluzhby-unix.md) - модули, доступные только на UNIX платформе
  * posix
  * pwd
  * spwd
  * grp
  * crypt
  * termios
  * tty
  * pty
  * fcntl
  * pipes
  * resource
  * nis
  * syslog
* [Замененные модули](../moduli-standartnoi-biblioteki-1/zamenennye-moduli.md) - устаревшие модули
  * optparse
  * imp
* [Недокументированные модули](../moduli-standartnoi-biblioteki-1/nedokumentirovannye-moduli.md) - эти модули в настоящее время недокументированы
  * Специфичные модули платформы


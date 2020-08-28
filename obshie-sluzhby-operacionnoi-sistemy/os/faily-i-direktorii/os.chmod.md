# os.chmod \(\)

### os.chmod \( _path_, _mode_, _\*_, _dir\_fd=None_, _follow\_symlinks=True_ \)

Изменяет режим пути _**path**_ на числовой _**mode**_. _**mode**_ может принимать одно из следующих значений \(как определено в модуле [stat](../../../dostup-k-failam-i-papkam/stat.md)\) или их комбинации с побитовым ИЛИ:

* stat.S\_ISUID
* stat.S\_ISGID
* stat.S\_ENFMT
* stat.S\_ISVTX
* stat.S\_IREAD
* stat.S\_IWRITE
* stat.S\_IEXEC
* stat.S\_IRWXU
* stat.S\_IRUSR
* stat.S\_IWUSR
* stat.S\_IXUSR
* stat.S\_IRWXG
* stat.S\_IRGRP
* stat.S\_IWGRP
* stat.S\_IXGRP
* stat.S\_IRWXO
* stat.S\_IROTH
* stat.S\_IWOTH
* stat.S\_IXOTH

Эта функция может поддерживать указание дескриптора файла, путей относительно дескрипторов каталогов, а не следование символическим ссылкам.

{% hint style="info" %}
Хотя Windows поддерживает **chmod \(\)**, с его помощью вы можете установить только флаг файла для чтения \(через константы stat.S\_IWRITE и stat.S\_IREAD или соответствующее целочисленное значение\). Все остальные биты игнорируются.
{% endhint %}

Вызывает событие аудита **os.chmod** с аргументами `path`, `mode`, `dir_fd`.

_Новое в версии 3.3:_ добавлена поддержка указания пути как дескриптора открытого файла, а также аргументов _**dir\_fd**_ и _**follow\_symlinks**_.

_Изменено в версии 3.6:_ Принимает объект, подобный пути \(_path-like object_ \).


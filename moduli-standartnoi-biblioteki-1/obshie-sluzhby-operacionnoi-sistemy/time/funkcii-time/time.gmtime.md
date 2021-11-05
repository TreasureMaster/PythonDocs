# time.gmtime ()

### time.gmtime( \[ _secs _] )

Конвертирует время, выраженное в секундах с начала эпохи, в [struct\_time](time.struct\_time.md) в формате UTC, в котором флаг _**dst**_ всегда равен нулю. Если _**secs**_ не указано или `None`, используется текущее время, возвращаемое функцией [time ()](time.time.md). Доли секунды игнорируются. См. выше описание объекта [struct\_time](time.struct\_time.md). См. [Calendar.timegm ()](../../../specialnye-tipy-dannykh/calendar/calendar.calendar/calendar.timegm.md) для обратной функции этой функции.

---
id: 14_date_functions_and_timedelta
title: Date Functions and Timedelta
sidebar_label: Date Functions and Timedelta
slug: /14_date_functions_and_timedelta
---

---

### Data Functions
Pandas contains extensive capabilities and features for working with time series data for all domains.

- `pd.date_range(start=None, end=None, periods=None, freq=None, tz=None, normalize=False, name=None, closed=None)`: returns a fixed frequency DatetimeIndex (Immutable ndarray-like of datetime64 data).
  - `start`: str or datetime-like (optional). Left bound for generating dates.
  - `end`: str or datetime-like (optional). Right bound for generating dates.
  - `periods`: int (optional). Number of periods to generate.
  - `freq`: str or DateOffset, default 'D'. Frequency strings can have multiples, e.g. '5H'.
    - `B`: business day frequency
    - `D`: calendar day frequency
    - `A`: annual(Year) end frequency
    - `W`: weekly frequency
    - `M`: month end frequency
    - `H`: hourly frequency
    - `T`, `min`: minutely frequency
    - `S`: secondly frequency
    - `L`, `ms`: milliseconds
    - `U`, `us`: microseconds
    - `N`: nanoseconds
  - `tz`: str or tzinfo (optional). Time zone name for returning localized DatetimeIndex, for example 'Asia/Hong_Kong'. By default, the resulting DatetimeIndex is timezone-naive.
  - `normalize`: bool. Normalize start/end dates to midnight before generating date range.
  - `name`: str. Name of the resulting DatetimeIndex.
  - `closed`: {None, 'left', 'right'} (optional). Make the interval closed with respect to the given frequency to the 'left', 'right', or both sides.


- `pd.to_datetime(arg, errors='raise', dayfirst=False, yearfirst=False, utc=None, format=None, exact=True, unit=None, infer_datetime_format=False, origin='unix', cache=True)`: converts argument to datetime.
  - `arg`: int, float, str, datetime, list, tuple, 1-d array, Series, DataFrame/dict-like. The object to convert to a datetime.
  - `errors`: {'ignore', 'raise', 'coerce'}.
    - If 'raise', then invalid parsing will raise an exception.
    - If 'coerce', then invalid parsing will be set as NaT.
    - If 'ignore', then invalid parsing will return the input.
  - `dayfirst`: bool. it specifies a date parse order if `arg` is str or its list-likes. If True, parses dates with the day first, eg 10/11/12 is parsed as 2012-11-10.
  - `yearfirst`: bool. it specifies a date parse order if `arg` is str or its list-likes.
    - If True parses dates with the year first, eg 10/11/12 is parsed as 2010-11-12.
    - If both dayfirst and yearfirst are True, yearfirst is preceded.
  - `utc`: bool. Return UTC DatetimeIndex if True.
  - `format`: str. The strftime to parse time, eg "%d/%m/%Y", note that "%f" will parse all the way up to nanoseconds.
  - `exact`: bool. Behaves as:
    - If True, require an exact format match.
    - If False, allow the format to match anywhere in the target string.
  - `unit`: str, default 'ns'. The unit of the arg (D,s,ms,us,ns) denote the unit, which is an integer or float number.
  - `infer_datetime_format`: bool. If True and no `format` is given, attempt to infer the format of the datetime strings based on the first non-NaN element, and if it can be inferred, switch to a faster method of parsing them.
  - `origin`: scalar. Define the reference date. The numeric values would be parsed as number of units (defined by `unit`) since this reference date.
    - If 'unix' (or POSIX) time; origin is set to 1970-01-01.
    - If 'julian', unit must be 'D', and origin is set to beginning of Julian Calendar. Julian day number 0 is assigned to the day starting at noon on January 1, 4713 BC.
    - If Timestamp convertible, origin is set to Timestamp identified by origin.
  - `cache`: bool. If True, use a cache of unique, converted dates to apply the datetime conversion.


```
import pandas as pd
import datetime

start = datetime.datetime(2020, 1, 1)
end = datetime.datetime(2021, 12, 5)

print("Simple Date Range:\n")
print(pd.date_range(start,end))

print("\nDate Range with montly frequncy:\n")
print(pd.date_range(start,end, freq='M'))

print("\nSimple Date Range with period=10:\n")
print(pd.date_range(start,end, periods=10 ))

print('\nto_string function:\n')
print(pd.to_datetime(start))



(output):
Simple Date Range:

DatetimeIndex(['2020-01-01', '2020-01-02', '2020-01-03', '2020-01-04',
               '2020-01-05', '2020-01-06', '2020-01-07', '2020-01-08',
               '2020-01-09', '2020-01-10',
               ...
               '2021-11-26', '2021-11-27', '2021-11-28', '2021-11-29',
               '2021-11-30', '2021-12-01', '2021-12-02', '2021-12-03',
               '2021-12-04', '2021-12-05'],
              dtype='datetime64[ns]', length=705, freq='D')

Date Range with montly frequncy:

DatetimeIndex(['2020-01-31', '2020-02-29', '2020-03-31', '2020-04-30',
               '2020-05-31', '2020-06-30', '2020-07-31', '2020-08-31',
               '2020-09-30', '2020-10-31', '2020-11-30', '2020-12-31',
               '2021-01-31', '2021-02-28', '2021-03-31', '2021-04-30',
               '2021-05-31', '2021-06-30', '2021-07-31', '2021-08-31',
               '2021-09-30', '2021-10-31', '2021-11-30'],
              dtype='datetime64[ns]', freq='M')

Simple Date Range with period=10:

DatetimeIndex(['2020-01-01 00:00:00', '2020-03-19 05:20:00',
               '2020-06-05 10:40:00', '2020-08-22 16:00:00',
               '2020-11-08 21:20:00', '2021-01-26 02:40:00',
               '2021-04-14 08:00:00', '2021-07-01 13:20:00',
               '2021-09-17 18:40:00', '2021-12-05 00:00:00'],
              dtype='datetime64[ns]', freq=None)

to_string:

2020-01-01 00:00:00
```



### Timedelta
Timedeltas are the differences in time and it can expressed in various format and units, for example, days, hours, minutes, seconds. Timedeltas cab be positive or negative.

-  `pd.timedelta_range(start=None, end=None, periods=None, freq=None, name=None, closed=None)`: returns a fixed frequency TimedeltaIndex (Immutable ndarray of timedelta64 data), with day as the default
frequency.
  - `start`: str or timedelta-like. Left bound for generating timedeltas.
  - `end`: str or timedelta-like. Right bound for generating timedeltas.
  - `periods`: int. Number of periods to generate.
  - `freq`: str or DateOffset, default 'D'. Frequency strings can have multiples, e.g. '5H'.
  - `name`: str. Name of the resulting TimedeltaIndex.
  - `closed`: str. Make the interval closed with respect to the given frequency to the 'left', 'right', or both sides (None).


- `pd.to_timedelta(arg, unit=None, errors='raise')`: converts argument to timedelta.
  - `arg` : str, timedelta, list-like or Series
    The data to be converted to timedelta.
  - `unit`: str (optional). it denotes the unit of the arg for numeric `arg`. Defaults to `"ns"`. Possible values:
    * 'W'
    * 'D' / 'days' / 'day'
    * 'hours' / 'hour' / 'hr' / 'h'
    * 'm' / 'minute' / 'min' / 'minutes' / 'T'
    * 'S' / 'seconds' / 'sec' / 'second'
    * 'ms' / 'milliseconds' / 'millisecond' / 'milli' / 'millis' / 'L'
    * 'us' / 'microseconds' / 'microsecond' / 'micro' / 'micros' / 'U'
    * 'ns' / 'nanoseconds' / 'nano' / 'nanos' / 'nanosecond' / 'N'
  - `errors`: {'ignore', 'raise', 'coerce'}.
    - If 'raise', then invalid parsing will raise an exception.
    - If 'coerce', then invalid parsing will be set as NaT.
    - If 'ignore', then invalid parsing will return the input.


```
import pandas as pd

print('Simple Timedelta Range:\n')
print(pd.timedelta_range(start='2 days', end='10 days'))

print('\nTimedelta Range by considering periods:\n')
print(pd.timedelta_range(start='2 days', end='10 days', periods=4))

print('\nTimedelta Range by considering freq:\n')
print(pd.timedelta_range(start='2 days', end='10 days',freq='10H'))

print('\nTimedelta Range by considering Year,Month and day:\n')
print(pd.timedelta_range(start='2 Y 10 M 11 days', end='3 Y 10 days'))



(output):
Simple Timedelta Range:

TimedeltaIndex([ '2 days',  '3 days',  '4 days',  '5 days',  '6 days',
                 '7 days',  '8 days',  '9 days', '10 days'],
               dtype='timedelta64[ns]', freq='D')

Timedelta Range by considering periods:

TimedeltaIndex(['2 days 00:00:00', '4 days 16:00:00', '7 days 08:00:00',
                '10 days 00:00:00'],
               dtype='timedelta64[ns]', freq=None)

Timedelta Range by considering freq:

TimedeltaIndex(['2 days 00:00:00', '2 days 10:00:00', '2 days 20:00:00',
                '3 days 06:00:00', '3 days 16:00:00', '4 days 02:00:00',
                '4 days 12:00:00', '4 days 22:00:00', '5 days 08:00:00',
                '5 days 18:00:00', '6 days 04:00:00', '6 days 14:00:00',
                '7 days 00:00:00', '7 days 10:00:00', '7 days 20:00:00',
                '8 days 06:00:00', '8 days 16:00:00', '9 days 02:00:00',
                '9 days 12:00:00', '9 days 22:00:00'],
               dtype='timedelta64[ns]', freq='10H')

Timedelta Range by considering Year,Month and day:

TimedeltaIndex([ '741 days 11:48:24',  '742 days 11:48:24',
                 '743 days 11:48:24',  '744 days 11:48:24',
                 '745 days 11:48:24',  '746 days 11:48:24',
                 '747 days 11:48:24',  '748 days 11:48:24',
                 '749 days 11:48:24',  '750 days 11:48:24',
                ...
                '1096 days 11:48:24', '1097 days 11:48:24',
                '1098 days 11:48:24', '1099 days 11:48:24',
                '1100 days 11:48:24', '1101 days 11:48:24',
                '1102 days 11:48:24', '1103 days 11:48:24',
                '1104 days 11:48:24', '1105 days 11:48:24'],
               dtype='timedelta64[ns]', length=365, freq='D')
```

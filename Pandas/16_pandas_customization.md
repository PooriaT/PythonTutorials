---
id: 16_pandas_customization
title: Pandas Customization
sidebar_label: Pandas Customization
slug: /16_pandas_customization
---

---


Pandas provides some instances to customize or change the display view and other aspects.

- `pd.get_option(pat)`: retrieves the value of the specified option.
  - `pat`: str. Regexp which should match a single option.
    - compute.[use_bottleneck, use_numba, use_numexpr]
    - display.[chop_threshold, colheader_justify, column_space, date_dayfirst, date_yearfirst, encoding, expand_frame_repr, float_format]
    - display.html.[border, table_schema, use_mathjax]
    - display.[large_repr]
    - display.latex.[escape, longtable, multicolumn, multicolumn_format, multirow,
    repr]
    - display.[max_categories, max_columns, max_colwidth, max_info_columns, max_info_rows, max_rows, max_seq_items, memory_usage, min_rows, multi_sparse, notebook_repr_html, pprint_nest_depth, precision, show_dimensions]
    - display.unicode.[ambiguous_as_wide, east_asian_width]
    - display.[width]
    - io.excel.ods.[reader, writer]
    - io.excel.xls.[reader, writer]
    - io.excel.xlsb.[reader]
    - io.excel.xlsm.[reader, writer]
    - io.excel.xlsx.[reader, writer]
    - io.hdf.[default_format, dropna_table]
    - io.parquet.[engine]
    - mode.[chained_assignment, sim_interactive, use_inf_as_na, use_inf_as_null]
    - plotting.[backend]
    - plotting.matplotlib.[register_converters]

```
import pandas as pd

# Some options
print("display.date_yearfirst: ",pd.get_option('display.date_yearfirst'))
print("display.width: ",pd.get_option('display.width'))
print("display.max_columns: ",pd.get_option('display.max_columns'))
print("compute.use_bottleneck: ",pd.get_option('compute.use_bottleneck'))



(output):
display.date_yearfirst:  False
display.width:  80
display.max_columns:  20
compute.use_bottleneck:  True
```


- `pd.set_option(pat,value)`: sets the value of the specified option.
  - `pat`: str. Regexp which should match a single option.
    - compute.[use_bottleneck, use_numba, use_numexpr]
    - display.[chop_threshold, colheader_justify, column_space, date_dayfirst, date_yearfirst, encoding, expand_frame_repr, float_format]
    - display.html.[border, table_schema, use_mathjax]
    - display.[large_repr]
    - display.latex.[escape, longtable, multicolumn, multicolumn_format, multirow,
    repr]
    - display.[max_categories, max_columns, max_colwidth, max_info_columns, max_info_rows, max_rows, max_seq_items, memory_usage, min_rows, multi_sparse, notebook_repr_html, pprint_nest_depth, precision, show_dimensions]
    - display.unicode.[ambiguous_as_wide, east_asian_width]
    - display.[width]
    - io.excel.ods.[reader, writer]
    - io.excel.xls.[reader, writer]
    - io.excel.xlsb.[reader]
    - io.excel.xlsm.[reader, writer]
    - io.excel.xlsx.[reader, writer]
    - io.hdf.[default_format, dropna_table]
    - io.parquet.[engine]
    - mode.[chained_assignment, sim_interactive, use_inf_as_na, use_inf_as_null]
    - plotting.[backend]
    - plotting.matplotlib.[register_converters]
  - `value`: object. New value of option.


- `pd.reset_option(pat)`: resets one or more options to their default value. Pass `"all"` as argument to reset all options.
  - `pat`: str/regex. If specified only options matching `prefix*` will be reset.


```
import pandas as pd

print('Current display width', pd.get_option('display.width'))

# Setting new value for display.width
pd.set_option('display.width', 40)
print('New display width', pd.get_option('display.width'))

# reset to default value
pd.reset_option('display.width')
print('Reset display width', pd.get_option('display.width'))



(output):
Current display width 80
New display width 40
Reset display width 80
```

- ` pd.describe_option(pat,  _print_desc=False)`: prints the description for one or more registered options.  
  - `pat`: str. Regexp pattern. All matching keys will have their description displayed.
  - `_print_desc`: bool. If True (default) the description(s) will be printed to stdout. Otherwise, the description(s) will be returned as a unicode string (for testing).


```
import pandas as pd

print(pd.describe_option('compute.use_bottleneck'))



(output):
compute.use_bottleneck : bool
    Use the bottleneck library to accelerate if it is installed,
    the default is True
    Valid values: False,True
    [default: True] [currently: True
```


- `pd.option_context(pat, val)`: context manager to ***temporarily*** set options in the `with` statement context.
  - `pat`: str. Regexp which should match a single option.  
  - `val`: object. New value of option.


```
import pandas as pd

print("Current display.width: ", pd.get_option('display.width'))

with pd.option_context("display.width",40):
    print("display.width inside the with:",pd.get_option("display.width"))

print("The last value of display.width:",pd.get_option("display.width"))



(output):
Current display.width:  80
display.width inside the with: 40
The last value of display.width: 80
```

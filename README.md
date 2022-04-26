# Bike Stats- ["The Notebook"](./bike-stats.ipynb)

---
jupyter:
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.7.12
  nbformat: 4
  nbformat_minor: 5
  papermill:
    default_parameters: {}
    duration: 13.514187
    end_time: "2022-04-26T05:00:13.325084"
    environment_variables: {}
    input_path: \_\_notebook\_\_.ipynb
    output_path: \_\_notebook\_\_.ipynb
    parameters: {}
    start_time: "2022-04-26T04:59:59.810897"
    version: 2.3.4
---

::: {.cell .markdown}
`<a href="https://www.kaggle.com/code/abedalqaderalkhatib/bike-stats?scriptVersionId=94020252" target="_blank">`{=html}`<img align="left" alt="Kaggle" title="Open in Kaggle" src="https://kaggle.com/static/images/open-in-kaggle.svg">`{=html}`</a>`{=html}
:::

::: {.cell .markdown _cell_guid="b1076dfc-b9ad-4769-8c92-a6c4dae69d19" _uuid="8f2839f25d086af736a60e9eeb907d3b93b6e0e5" papermill="{\"status\":\"completed\",\"duration\":1.4461e-2,\"end_time\":\"2022-04-26T05:00:10.628805\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:10.614344\"}" tags="[]"}
# Data Analysis with pandas

## Data set name: Cycle Share Data set
:::

::: {.cell .code execution_count="1" execution="{\"iopub.status.busy\":\"2022-04-26T05:00:10.656076Z\",\"iopub.status.idle\":\"2022-04-26T05:00:12.070255Z\",\"iopub.execute_input\":\"2022-04-26T05:00:10.65641Z\",\"shell.execute_reply\":\"2022-04-26T05:00:12.069068Z\"}" papermill="{\"status\":\"completed\",\"duration\":1.433022,\"end_time\":\"2022-04-26T05:00:12.07498\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:10.641958\"}" tags="[]"}
``` {.python}
import pandas as pd
import numpy as np
from datetime import datetime as dt


trip_df = pd.read_csv('../input/cycle-share-dataset/trip.csv', error_bad_lines=False)

weather_df = pd.read_csv('../input/cycle-share-dataset/weather.csv')

station_df = pd.read_csv('../input/cycle-share-dataset/station.csv')
```

::: {.output .stream .stderr}
    /opt/conda/lib/python3.7/site-packages/IPython/core/interactiveshell.py:3524: FutureWarning: The error_bad_lines argument has been deprecated and will be removed in a future version.


      exec(code_obj, self.user_global_ns, self.user_ns)
    b'Skipping line 50794: expected 12 fields, saw 20\n'
:::
:::

::: {.cell .markdown papermill="{\"status\":\"completed\",\"duration\":1.3549e-2,\"end_time\":\"2022-04-26T05:00:12.102888\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.089339\"}" tags="[]"}
### Q1: What is the average trip duration for a borrowed bicycle?
:::

::: {.cell .code execution_count="2" execution="{\"iopub.status.busy\":\"2022-04-26T05:00:12.131257Z\",\"iopub.status.idle\":\"2022-04-26T05:00:12.143613Z\",\"iopub.execute_input\":\"2022-04-26T05:00:12.131983Z\",\"shell.execute_reply\":\"2022-04-26T05:00:12.142162Z\"}" papermill="{\"status\":\"completed\",\"duration\":3.0053e-2,\"end_time\":\"2022-04-26T05:00:12.146535\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.116482\"}" tags="[]"}
``` {.python}
duration_in_minutes = trip_df['tripduration'].mean() // 60
print(duration_in_minutes)
```

::: {.output .stream .stdout}
    19.0
:::
:::

::: {.cell .markdown papermill="{\"status\":\"completed\",\"duration\":1.4989e-2,\"end_time\":\"2022-04-26T05:00:12.176377\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.161388\"}" tags="[]"}
### Q2: What's the most common age of a bicycle-sharer?
:::

::: {.cell .code execution_count="3" execution="{\"iopub.status.busy\":\"2022-04-26T05:00:12.205856Z\",\"iopub.status.idle\":\"2022-04-26T05:00:12.221871Z\",\"iopub.execute_input\":\"2022-04-26T05:00:12.206187Z\",\"shell.execute_reply\":\"2022-04-26T05:00:12.220651Z\"}" papermill="{\"status\":\"completed\",\"duration\":3.3484e-2,\"end_time\":\"2022-04-26T05:00:12.224123\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.190639\"}" tags="[]"}
``` {.python}
age = 2020 - int(trip_df['birthyear'].value_counts().idxmax())
print(age)
```

::: {.output .stream .stdout}
    33
:::
:::

::: {.cell .markdown papermill="{\"status\":\"completed\",\"duration\":1.3833e-2,\"end_time\":\"2022-04-26T05:00:12.252456\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.238623\"}" tags="[]"}
### Q3: Given all the weather data here, find the average precipitation per month, and the median precipitation. {#q3-given-all-the-weather-data-here-find-the-average-precipitation-per-month-and-the-median-precipitation}
:::

::: {.cell .code execution_count="4" execution="{\"iopub.status.busy\":\"2022-04-26T05:00:12.2824Z\",\"iopub.status.idle\":\"2022-04-26T05:00:12.3636Z\",\"iopub.execute_input\":\"2022-04-26T05:00:12.283055Z\",\"shell.execute_reply\":\"2022-04-26T05:00:12.362656Z\"}" papermill="{\"status\":\"completed\",\"duration\":9.9493e-2,\"end_time\":\"2022-04-26T05:00:12.366341\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.266848\"}" tags="[]"}
``` {.python}
weather_df['Date'] = pd.to_datetime(weather_df['Date'])
weather_df['Month'] = weather_df['Date'].dt.month
avg = (weather_df[['Month','Precipitation_In']]).groupby(weather_df.Month).mean()
print(avg)

medi = (weather_df[['Month','Precipitation_In']]).groupby(weather_df.Month).median()
print(medi)
```

::: {.output .stream .stdout}
           Month  Precipitation_In
    Month                         
    1        1.0          0.143548
    2        2.0          0.168421
    3        3.0          0.156935
    4        4.0          0.051333
    5        5.0          0.012419
    6        6.0          0.030500
    7        7.0          0.012097
    8        8.0          0.018226
    9        9.0          0.041000
    10      10.0          0.189000
    11      11.0          0.187833
    12      12.0          0.236290
           Month  Precipitation_In
    Month                         
    1        1.0             0.020
    2        2.0             0.040
    3        3.0             0.025
    4        4.0             0.000
    5        5.0             0.000
    6        6.0             0.000
    7        7.0             0.000
    8        8.0             0.000
    9        9.0             0.000
    10      10.0             0.040
    11      11.0             0.035
    12      12.0             0.100
:::
:::

::: {.cell .markdown papermill="{\"status\":\"completed\",\"duration\":1.4563e-2,\"end_time\":\"2022-04-26T05:00:12.396232\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.381669\"}" tags="[]"}
### Q4: What's the average number of bikes at a given bike station?
:::

::: {.cell .code execution_count="5" execution="{\"iopub.status.busy\":\"2022-04-26T05:00:12.428327Z\",\"iopub.status.idle\":\"2022-04-26T05:00:12.433832Z\",\"iopub.execute_input\":\"2022-04-26T05:00:12.42868Z\",\"shell.execute_reply\":\"2022-04-26T05:00:12.433139Z\"}" papermill="{\"status\":\"completed\",\"duration\":2.434e-2,\"end_time\":\"2022-04-26T05:00:12.436013\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.411673\"}" tags="[]"}
``` {.python}
median_precipitation = station_df.current_dockcount.mean()
print(median_precipitation)
```

::: {.output .stream .stdout}
    16.517241379310345
:::
:::

::: {.cell .markdown papermill="{\"status\":\"completed\",\"duration\":1.5156e-2,\"end_time\":\"2022-04-26T05:00:12.466838\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.451682\"}" tags="[]"}
### Q5: When a bike station is modified, is it more likely that it'll lose bikes or gain bikes? How do you know?
:::

::: {.cell .code execution_count="6" execution="{\"iopub.status.busy\":\"2022-04-26T05:00:12.498598Z\",\"iopub.status.idle\":\"2022-04-26T05:00:12.510311Z\",\"iopub.execute_input\":\"2022-04-26T05:00:12.49943Z\",\"shell.execute_reply\":\"2022-04-26T05:00:12.509659Z\"}" papermill="{\"status\":\"completed\",\"duration\":3.0826e-2,\"end_time\":\"2022-04-26T05:00:12.512702\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.481876\"}" tags="[]"}
``` {.python}
station = station_df[['modification_date','install_dockcount','current_dockcount']].dropna()
bike_modified = station['current_dockcount'].sum()-station['install_dockcount'].sum()

print(station)
print(bike_modified)
```

::: {.output .stream .stdout}
       modification_date  install_dockcount  current_dockcount
    7          11/9/2015                 20                 18
    10          8/9/2016                 16                  0
    12         2/24/2015                 18                 20
    17         2/24/2015                 28                 26
    22         3/24/2015                 30                 24
    23         3/27/2015                 12                 16
    26         3/18/2016                 16                  0
    31         2/24/2015                 18                 20
    35         3/13/2015                 12                 20
    37         2/23/2015                 18                 16
    38         11/2/2015                 20                  0
    39          3/4/2015                 12                 16
    46        10/29/2015                 16                  0
    47         2/20/2015                 12                 14
    48         2/20/2015                 18                 16
    49         2/20/2015                 12                 14
    50         2/20/2015                 20                 14
    -64
:::
:::

::: {.cell .markdown papermill="{\"status\":\"completed\",\"duration\":1.5018e-2,\"end_time\":\"2022-04-26T05:00:12.543351\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.528333\"}" tags="[]"}
# The Test
:::

::: {.cell .code execution_count="7" execution="{\"iopub.status.busy\":\"2022-04-26T05:00:12.576194Z\",\"iopub.status.idle\":\"2022-04-26T05:00:12.582446Z\",\"iopub.execute_input\":\"2022-04-26T05:00:12.576734Z\",\"shell.execute_reply\":\"2022-04-26T05:00:12.581794Z\"}" papermill="{\"status\":\"completed\",\"duration\":2.5445e-2,\"end_time\":\"2022-04-26T05:00:12.585119\",\"exception\":false,\"start_time\":\"2022-04-26T05:00:12.559674\"}" tags="[]"}
``` {.python}
def test():
    
    def assert_equal(actual,expected):
        assert actual == expected, f"Expected {expected} but got {actual}"

    assert_equal(duration_in_minutes , 19.0 )
    assert_equal(age, 33)
    assert_equal(median_precipitation, 16.517241379310345)
    assert_equal(bike_modified, -64)


    print("Done..!")

test()
```

::: {.output .stream .stdout}
    Done..!
:::
:::

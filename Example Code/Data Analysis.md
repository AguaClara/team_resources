# Example Code for Data Analysis

We've provided some examples of code here for analyzing and presenting  data. You're welcome to use these as templates for your own code, but you may discover that your specific data is best represented in ways not covered here. In that case, first look up and read about functions in the Python libraries such as [Matplotlib](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html), [NumPy](https://docs.scipy.org/doc/numpy/reference/), and [Pandas](http://pandas.pydata.org/pandas-docs/version/0.15/tutorials.html). Then, if you still believe a certain example should be added to this collection, you  can [write an issue](https://github.com/AguaClara/team_resources/issues/new) to the team_resources repository with your recommendation.

### Table of Contents

I. [Reading ProCoDA Data with the AguaClara Package](#reading-procoda-data-with-the-aguaclara-package)

II. [Reading Other Spreadsheet Data with the Pandas Package](#reading-other-spreadsheet-data-with-the-pandas-package)

III. [Plotting with Matplotlib: One Y-Axis](#plotting-with-matplotlib-one-y-axis)

IV. [Plotting with Matplotlib: Two Y-Axes](#plotting-with-matplotlib-two-y-axes)

V. [Regression Analysis and Curve Fitting](#regression-analysis-and-curve-fitting)

### Reading ProCoDA Data with the AguaClara Package
The `aguaclara.research.procoda_parser` module in the [`aguaclara` Python package](https://github.com/AguaClara/aguaclara) contains functions for analyzing data collected by ProCoDA.

##### Example 1: Reading one column of data for a specified TIME
The function
```python
get_data_by_time(path, columns, start_date, start_time="00:00",
                 end_date=None, end_time="23:59"))
```
in the `procoda_parser` module extracts data from a ProCoDA datalog based on the `path` (folder in your computer) the file is located in, the `columns` you wish to extract, the `start_date`, and the optional `start_time`, `end_date` (if the experiment ran overnight), and `end_time`. The `columns` input can be a single integer, if you want to extract one column, or a list of integers, if you want to extract multiple. *Note that the 0<sup>th</sup> column of a ProCoDA datalog is the time column.*

The output is either
1. a list of numbers (for a single column of data)
2. a list of lists of numbers (for multiple columns of data, in the order specified in the `columns` input)

<!-- Therefore, if we want to graph it, we can pass it directly to the ``plot()`` function from ``matplotlib.pyplot`` (see sections [III](#plotting-with-matplotlib-one-y-axis) and [IV](#plotting-with-matplotlib-two-y-axes)). -->

Here is an example that uses `get_data_by_time` to extract data from one column, for one day, and for specified start and end time.
```python
from aguaclara.research import procoda_parser as pp

data_path = "/Users/HannahSi/Documents/Atom/team_resources/Data"
column = pp.get_data_by_time(path=data_path, columns=4, start_date="6-14-2018",
                             start_time="15:40", end_time="23:30")
print(column) #Run this to see the list of data
```

##### Example 2: Reading multiple columns of data for a specified TIME
Here is another example that uses `get_data_by_time()` again to extract three columns (which happen to represent time, influent turbidity, and effluent turbidity) of data over the entirety of two days (since no start or end times are specified).

```python
from aguaclara.research import procoda_parser as pp

data_path = "/Users/HannahSi/Documents/Atom/team_resources/Data"
columns = pp.get_data_by_time(path=data_path, columns=[0, 3, 4],
                        start_date="6-14-2018", end_date='6-15-2018')
time = columns[0]
influent_turbidity = columns[1]
effluent_turbidity = columns[2]
```

##### Example 3. Reading one column of data for a specified STATE
The function
```python
get_data_by_state(path, dates, state, column)
```
in the `procoda_parser` module extracts data from a ProCoDA datalog based on the `path` (folder in your computer) the file is located in, the `dates` of the experiment (input as a list of one or more dates), the `state` of ProCoDA during which you collected your data of interest (this is an integer), and the `column` of the data that you want to extract. *Note that the 0<sup>th</sup> column of a ProCoDA datalog is the time column.*

The output of the function is a 3-dimension list (list of lists of lists), where the "smallest" lists are lists of time and data (from your desired column) from the ProCoDA datalog, the next level of lists contains contains a time and data column pair for a single iteration of your state, and the top level of lists contains these lists for each iteration.

Here is an example that graphs the output of this function:

```python
from aguaclara.research import procoda_parser as pp
import matplotlib.pyplot as plt

data_path = "/Users/HannahSi/Documents/Atom/team_resources/Data"
data = pp.get_data_by_state(data_path, dates=["6-19-2013"], state=1, column=1)

for i in range(len(data)):
  plt.plot(data[i][:,0]-data[i][0,0], data[i][:,1])
```

### Reading Other Spreadsheet Data with the Pandas Package
The [Pandas](http://pandas.pydata.org/pandas-docs/version/0.15/tutorials.html) library is useful for reading and manipulating spreadsheets of data in Python. Below are some examples for using Pandas to read columns and rows from an Excel spreadsheet.

```python
import pandas as pd

data = pd.read_excel("Data/Solubility of Oxygen.xlsx")
print(data)         # Run this to see the table of data
print(data.columns) # Run this to see the column labels

# Reading columns by name
temperature = data["Temperature (ºC)"]
solubility = data["Solubility of O2 (mg/L)"]

# Reading columns by index
temperature = data.iloc[:,0]
solubility = data.iloc[:,1]

# Reading rows by index
temp_first = data.loc[0]
temp_last = data.loc[data.shape[0]-1]
```
Click [here](http://pandas.pydata.org/pandas-docs/stable/reference/index.html#api) for the full Pandas API Reference (a list of all its available functions and data types).

### Plotting with Matplotlib: One Y-Axis

```python
import aguaclara.research.procoda_parser as pp
import matplotlib.pyplot as plt
import numpy as np

time, effluent_turbidity = pp.get_data_by_time(
      path="Data", columns=[0, 4], start_date="6-14-2018",
      start_time="15:40", end_time="23:30")
elapsed_time = (np.array(time)-time[0])*24

plt.xlabel("Time (hours)")
plt.ylabel("Effluent Turbidity (NTU)")
plt.plot(elapsed_time, effluent_turbidity, color="blue")
```

### Plotting with Matplotlib: Two Y-Axes

```python
import aguaclara.research.procoda_parser as pp
import matplotlib.pyplot as plt
import numpy as np

time, influent_turbidity, effluent_turbidity = pp.get_data_by_time(
      path="Data", columns=[0, 3, 4], start_date="6-14-2018",
      start_time="15:40", end_time="23:30")
elapsed_time = (np.array(time)-time[0])*24

fig, ax1 = plt.subplots()
ax1.set_xlabel("Time (hours)")
ax1.set_ylabel("Effluent Turbidity (NTU)")
line1, = ax1.plot(elapsed_time, effluent_turbidity, color="blue")

ax2 = ax1.twinx()
ax2.set_ylabel("Influent Turbidity (NTU)")
ax2.set_ylim(60,120)
line2, = ax2.plot(elapsed_time, influent_turbidity, color="green")

plt.legend((line1, line2), ("Effluent", "Influent"))
```

### Regression Analysis and Curve Fitting

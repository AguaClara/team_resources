# Example Code for Data Analysis

We've provided some examples of code here for analyzing and presenting research data. You're welcome to use these as templates for your own code, but you may discover that your specific data is best analyzed in ways not covered here. In that case, first look up and read about functions in Python libraries like [Matplotlib](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html), [NumPy](https://docs.scipy.org/doc/numpy/reference/), and [Pandas](http://pandas.pydata.org/pandas-docs/version/0.15/tutorials.html). If you working with data from ProCoDA, check out the [ProCoDA parsing](https://aguaclara.github.io/aguaclara/research/procoda_parser.html) functions in the [AguaClara package](https://aguaclara.github.io/aguaclara/). Then, if you still would like a certain example of code to be added to this collection, you can [write an issue to the team_resources repository](https://github.com/AguaClara/team_resources/issues/new) with your request.

### Table of Contents

I. [Reading ProCoDA Data with the AguaClara Package](#reading-procoda-data-with-the-aguaclara-package)

II. [Reading Other Spreadsheets with the Pandas Package](#reading-other-spreadsheets-with-the-pandas-package)

III. [Plotting with Matplotlib: One Y-Axis](#plotting-with-matplotlib-one-y-axis)

IV. [Plotting with Matplotlib: Two Y-Axes](#plotting-with-matplotlib-two-y-axes)

V. [Regression Analysis and Curve Fitting](#regression-analysis-and-curve-fitting)

### Reading ProCoDA Data with the AguaClara Package
The `aguaclara.research.procoda_parser` module in the [AguaClara Python package](https://github.com/AguaClara/aguaclara) contains functions for analyzing data collected by ProCoDA. Click [here](https://aguaclara.github.io/aguaclara/research/procoda_parser.html) for documentation to all the functions available in the module.

##### Example 1: Reading one column of data for a specified TIME
The function
```python
get_data_by_time(path, columns, dates,
                 start_time="00:00", end_time="23:59")
```
in the `procoda_parser` module extracts data from a ProCoDA datalog based on the `path` (folder in your computer) the file is located in, the `columns` you wish to extract, the `dates` of the experiment (a single date or a list of consecutive dates), and the optional `start_time` and `end_date`. The `columns` input can be a single integer if you want to extract one column, or it can be a list of integers if you want to extract multiple columns. Note: the 0<sup>th</sup> column of a ProCoDA datalog is the time column.

The output is either
1. a list of numbers (for a single column of data), or
2. a list of lists of numbers (for multiple columns of data, in the order specified in the `columns` input)

<!-- Therefore, if we want to graph it, we can pass it directly to the ``plot()`` function from ``matplotlib.pyplot`` (see sections [III](#plotting-with-matplotlib-one-y-axis) and [IV](#plotting-with-matplotlib-two-y-axes)). -->

Here is an example that uses `get_data_by_time` to extract data from one column, for one day, and for specified start and end times.
```python
import aguaclara.research.procoda_parser as pp

# This is a relative path to the Data folder in this repository. If you
# have downloaded this repository onto your computer, you can also use
# an absolute path, which might look like C:\Users\...\team_resource\Data
# (Windows) or /Users/.../team_resources/Data (Mac/Linux)
data_path = "Data"

column = pp.get_data_by_time(path=data_path, columns=4,
                             dates="6-14-2018", start_time="15:40",
                             end_time="23:30")
print(column)
```

##### Example 2: Reading multiple columns of data for a specified TIME
Here is another example that uses `get_data_by_time()` again to extract three columns (which happen to represent time, influent turbidity, and effluent turbidity) of data over the entirety of two days (since no start or end times are specified).

```python
import aguaclara.research.procoda_parser as pp

# This is a relative path to the Data folder in this repository. If you
# have downloaded this repository onto your computer, you can also use
# an absolute path, which might look like C:\Users\...\team_resource\Data
# (Windows) or /Users/.../team_resources/Data (Mac/Linux)
data_path = "Data"

columns = pp.get_data_by_time(path=data_path, columns=[0, 3, 4],
                              dates=["6-14-2018", "6-15-2018"])
# columns is now a list of 3 elements, each of which is also a list:

# 1. a list of times (from the 0th column)
time = columns[0]
# 2. a list of influent turbidity values (from the 3rd column)
influent_turbidity = columns[1]
# 3. a list of effluent turbidity values (from the 4th column)
effluent_turbidity = columns[2]
```

##### Example 3. Reading one column of data for a specified STATE
The function
```python
get_data_by_state(path, dates, state, column)
```
in the `procoda_parser` module extracts data from a ProCoDA datalog based on the `path` (folder in your computer) the file is located in, the `dates` of the experiment (input as a list of one or more dates), the `state` of ProCoDA during which you collected your data of interest (this is an integer), and the `column` of the data that you want to extract. *Note that the 0<sup>th</sup> column of a ProCoDA datalog is the time column.*

The output of the function is a 3-dimension list (list of lists of lists), where the "smallest" lists are lists of time and data (from your desired column) from the ProCoDA datalog, the next level of lists contains contains time and data column pairs (one for each  iteration of your state), and the top level of lists contains these lists for each iteration.

Here is an example that uses `get_data_by_time` to extract and make simple calculations on data from a particular ProCoDA state.

```python
import aguaclara.research.procoda_parser as pp

# This is a relative path to the Data folder in this repository. If you
# have downloaded this repository onto your computer, you can also use
# an absolute path, which might look like C:\Users\...\team_resource\Data
# (Windows) or /Users/.../team_resources/Data (Mac/Linux)
data_path = "Data"

data = pp.get_data_by_state(data_path, dates="6-19-2013", state=1, column=1)

# This empty list will be used later to hold the average pH reading from
# each iteration of the 1st state
pH_averages = []

for iteration in data:
  # Here's how to extract time from the output:
  time = iteration[:,0]
  elapsed_time = time - iteration[0,0]

  # Here's a way to extract and work with data from the output:
  pH_readings = iteration[:,1]
  pH_averages.append(sum(pH_readings)/len(pH_readings))

print(pH_averages)
```

### Reading Other Spreadsheets with the Pandas Package
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
first_row = data.loc[0]
last_row = data.loc[data.shape[0]-1]
```
Click [here](http://pandas.pydata.org/pandas-docs/stable/reference/index.html#api) for the full Pandas API Reference (a list of all its available functions and data types).

### Plotting with Matplotlib: One Y-Axis

[Matplotlib](https://matplotlib.org/api/_as_gen/matplotlib.pyplot.html) is a great package for creating graphs, just as you may already do in Excel or Matlab. As a Python package, however, it can easily handle the data that you have already read and manipulated in Python.

Below is an example of reading s of time and data from a ProCoDA data file (see [Reading ProCoDA Data with the AguaClara Package](#reading-procoda-data-with-the-aguaclara-package)) and graphing it on one y-axis, with labels for the x-axis and the y-axis.

```python
import aguaclara.research.procoda_parser as pp
import matplotlib.pyplot as plt
import numpy as np

# Read the 0th column (time) and the 4th column (effluent turbidity)
time, effluent_turbidity = pp.get_data_by_time(
      path="Data", columns=[0, 4], start_date="6-14-2018",
      start_time="15:40", end_time="23:30")
elapsed_time = (np.array(time)-time[0])*24

plt.xlabel("Time (hours)")
plt.ylabel("Effluent Turbidity (NTU)")
plt.plot(time, effluent_turbidity, color="blue")
```

Output:

<img src="../Images/One Axis.png">


### Plotting with Matplotlib: Two Y-Axes

Below is an example of reading multiple columns of data from a ProCoDA data file (see [Reading ProCoDA Data with the AguaClara Package](#reading-procoda-data-with-the-aguaclara-package)) and graphing it on two y-axes using [`matplotlib.pyplot.subplots()`](https://matplotlib.org/gallery/subplots_axes_and_figures/subplots_demo.html).

```python
import aguaclara.research.procoda_parser as pp
import matplotlib.pyplot as plt
import numpy as np

time, influent_turbidity, effluent_turbidity = pp.get_data_by_time(
      path="Data", columns=[0, 3, 4], start_date="6-14-2018",
      start_time="15:40", end_time="23:30")
elapsed_time = (np.array(time)-time[0])*24

# ax1 is the axis handle for the first y-axis
fig, ax1 = plt.subplots()
ax1.set_xlabel("Time (hours)")
ax1.set_ylabel("Effluent Turbidity (NTU)")
# line1 is the line handle for the effluent_turbidity graph
line1, = ax1.plot(elapsed_time, effluent_turbidity, color="blue")

# ax2 is an axis handle for the second y-axis, with the same x-axis as ax1
ax2 = ax1.twinx()
ax2.set_ylabel("Influent Turbidity (NTU)")
ax2.set_ylim(60,120)
# line1 is the line handle for the effluent_turbidity graph
line2, = ax2.plot(elapsed_time, influent_turbidity, color="green")

plt.legend((line1, line2), ("Effluent", "Influent"))
```

Output:

<img src="../Images/Two Axes.png">


### Regression Analysis and Curve Fitting

The SciPy package, particularly the [`SciPy.stats` modules](https://docs.scipy.org/doc/scipy/reference/stats.html) and [`SciPy.optimize` module](https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.curve_fit.html) is useful for regression analyses and curve fitting in Python.

Here is example of a linear regression on the Temperature and Oxygen Solubility Data in the Data folder of this repository:

```python
import pandas as pd
import scipy.stats as stats

data = pd.read_excel("Data/Solubility of Oxygen.xlsx")
temperature = data["Temperature (ºC)"]
solubility = data["Solubility of O2 (mg/L)"]

linreg = stats.linregress(temperature, solubility)
slope, intercept, r_value = linreg[0:3]

print("Slope:", slope)
print("Intercept:", intercept)
print("R-squared:", r_value ** 2)

# Here's a way to graph the regression line with the data:
import numpy as np
import matplotlib.pyplot as plt
x_range = np.arange(temperature.iloc[0], temperature.iloc[-1]+1)

plt.xlabel('Temperature (ºC)')
plt.ylabel('Solubility of O2 (mg/L)Y label')
plt.plot(temperature, solubility, 'o')
plt.plot(x_range, x_range * slope + intercept)
```

Output:

Slope: -0.17145454545454547

Intercept: 13.277272727272727

R-squared: 0.944743216539532

<img src="../Images/Lin Reg.png">

From the graph, we might judge that an exponential fit would be best for the data. We can also `SciPy.optimize.curve_fit()` for non-linear curve fitting. Here's an example found in SciPy's documentation:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import scipy.optimize as opt

data = pd.read_excel("Data/Solubility of Oxygen.xlsx")
temperature = data["Temperature (ºC)"]
solubility = data["Solubility of O2 (mg/L)"]

def exp_func(x, a, b, c):
  return a * np.exp(-b * x) + c

cf_output = opt.curve_fit(exp_func, temperature, solubility)
optimal_parameters = cf_output[0]
print("a:", optimal_parameters[0])
print("b:", optimal_parameters[1])
print("c:", optimal_parameters[2])

x_range = np.arange(temperature.iloc[0], temperature.iloc[-1]+1, step=0.1)

plt.xlabel('Temperature (ºC)')
plt.ylabel('Solubility of O2 (mg/L)Y label')
plt.plot(temperature, solubility, 'o')
plt.plot(x_range, exp_func(x_range, *optimal_parameters))
```

Output:

a: 10.694801786694969

b: 0.03546205767749912

c: 3.858064720006462

<img src="../Images/Nonlin Reg.png">

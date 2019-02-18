## Example Code for Data Analysis

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
extracts data from a ProCoDA datalog based on the `path` (folder in your computer) the file is located in, the `columns` you wish to extract, the `start_date`, and the optional `start_time`, `end_date` (if the experiment ran overnight), and `end_time`. The `columns` input can be a single integer, if you want to extract one column, or a list of integers, if you want to extract multiple. *Note that the 0<sup>th</sup> column of a ProCoDA datalog is the time column.*

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
print(column) #Run this to see your list of data
```

##### Example 2: Reading multiple columns of data for a specified TIME
Here is another example that uses `get_data_by_time()` again to extract three columns (which happen to represent time, influent turbidity, and effluent turbidity) of data over the entirety of two days (since no start or end times are specified).

```python
from aguaclara.research import procoda_parser as pp

data_path = "/Users/HannahSi/Documents/Atom/team_resources/Data"
data = pp.get_data_by_time(path=data_path, columns=[0, 3, 4],
                        start_date="6-14-2018", end_date='6-15-2018')
time = data[0]
influent_turbidity = data[1]
effluent_turbidity = data[2]
```

##### Example 3. Reading one column of data for a specified STATE


### Reading Other Spreadsheet Data with the Pandas Package


### Plotting with Matplotlib: One Y-Axis


### Plotting with Matplotlib: Two Y-Axes


### Regression Analysis and Curve Fitting

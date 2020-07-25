# pandas Foundations

Source: [pandas Foundations](https://learn.datacamp.com/courses/pandas-foundations#)

pandas is a library for data analysis. 

# Syntax

## DataFrame

- Tabular data structure with labeled rows and columns. 
	- Rows are labeled by data structure index. Indexes in pandas are list of labels that permit fast look-up and relational openrations.

	Example: DataFrame of Apple Stock data. Here, index labels are dates in reverse chronological order.

	<img width="624" alt="Screen Shot 2020-07-25 at 11 36 27 AM" src="https://user-images.githubusercontent.com/8196343/88463964-a4cde180-ce6b-11ea-93d3-d39c686a366a.png">

```python
import pandas as pd
type(APPL) # pandas.core.frame.DataFrame

APPL.shape # (8514, 6) it has 8514 rows & 6 columns

```

## Index
```python
APPL.columns # Index(['Open', 'High', 'Low', 'Close', 'Volume', 'Adj Close'], dtype='object')
type(APPLe.columns) # pandas.indexes.base.Index

APPL.index # DatetimeIndex(['2014-09-16', '2014--0-15'], dtype='datatime64[ns]', name='Date', length=8514, freq=None)
type(APPL.index) # pandas.tseries.index.DatetimeIndex
```

## Slice and Info

Data frames can be sliced using colons to specify the start, end, and stride of a slice.
```python
'''
slice from the start of the DataFrame to the 5th row (non inclusive) using .iloc accessor to express the slice positionally
'''
APPL.iloc[:5,:] 

'''
slice from the 5th last row to the end of the DataFrame using a negative index
'''
APPL.iloc[-5:,:]

'''
slice using labels with the .iloc accessor
'''


'''
return the first 5 rows of the DataFrame
'''
APPL.head(5)

'''
specifying tail() without an argument return the last 5 rows
'''
APPL.tail()

'''
specifying tail() with 3 return the last 3 rows
'''
APPL.tail(3)


APPL.info()
'''
<class 'pandas.core.frame.DataFrame'>
Datetime Index: 8514 entries, 2014-09-16 to 1980-12-12
Data columns (total 6 columns):
Open         8514 non-null float64
High         8514 non-null float64
Low          8514 non-null float64
Close        8514 non-null float64
Volume       8514 non-null int64
Adj Close    8514 non-null float64
dtypes: float64(5), int64(1)
memory usage: 465.6
'''
```

## Broadcast

Braodcast value to each row
```python
'''
assigning scalar value to column slice broadcasts value to each row
here, slice consits of every 3rd row starting from 0 in the last column
view the changes with APPL.head(6). 
call APPL.info() and we can seee the last column has fewer non-null entries than the others due to our assigning nan to every 3rd element.
'''
APPL.iloc[::3, -1] = np.nan
```
<img width="632" alt="Screen Shot 2020-07-25 at 12 11 19 PM" src="https://user-images.githubusercontent.com/8196343/88464484-fd06e280-ce6f-11ea-833e-ac08ced648fe.png">

```python
'''
<class 'pandas.core.frame.DataFrame'>
Datetime Index: 8514 entries, 2014-09-16 to 1980-12-12
Data columns (total 6 columns):
Open         8514 non-null float64
High         8514 non-null float64
Low          8514 non-null float64
Close        8514 non-null float64
Volume       8514 non-null int64
Adj Close    5676 non-null float64
dtypes: float64(5), int64(1)
memory usage: 465.6
'''
```

## Series

Extracting a single column data returns a series.
```python
low = APPL['Low']
type(low) # pandas.core.series.Series


'''
Series extracted has its own head method and inherits its name attribute from the DataFrame column.
'''
low.head()
'''
Date
2014-09-16		98.89
2014-09-15		101.44
2014-09-12		101.88
2014-09-10		97.76
Name: Low, dtype: float64
'''

'''
Extract the numerical entries from the series, use the values attribute
'''
lows = low.values
type(lows) # numpy.ndarray

```

| pandas series  |  pandas DataFrame |
|---|---|
| 1D labelled NumPy array  |  2D labelled array whose columns are Series |

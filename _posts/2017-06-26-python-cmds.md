---
layout: post
title: Python Cheat Sheet
tags: [python]
categories: notes
---
This list is supposed to be a refresher to help me quickly recall a few Python's key points.

## Syntax 
* variable = blah7
* zero-indexed
* raise to power by **
* print(stuff)
* True/False
* and/or/not
* assert returns nothing when there are no errors
* type()
* if/elif/else COLON, INDENT
* while COLON, INDENT
* for index, variable in **enumerate**(list, start=startIndex) COLON
* **global** keyword to change a global variable from inside a function
* to_csv/to_excel
* list [elements can be of many types]
    * list[-1]
    * [a,b] = [0,0]  ; a += 1, print([a,b]) # returns [1,0]
    * slice[incluse:exclusive]
    * del(fam[0])
    * list + [new_element]
    * shallow copy listX=listY
        * use listX = list(listY) for deep copy
* use ; to place commands on the same line
* help(sth) or ?sth
* **map**(function, seq) applies function to every element of seq, and returns a map object, use list() to get a list
* **filter**(function, seq) returns an object that contains elements of seq that answer True to function
* **reduce**(function, seq) is kinda like foldr,foldl
```
stark = ['robb', 'sansa', 'arya', 'eddard', 'jon']
result = reduce(lambda item1, item2: item1+item2, stark)
```
* **try-except** clause + **raise** errors
```
def sqrt(x):
    if x < 0:
        raise ValueError('x must be non-neg')
    try:
        return x ** 0.5
    except TypeError:
        print("blah")
sqrt("hello") # returns blah now
```
* Everything in Python, including strings, floats and lists is an object, so each has its own set of methods.
* strings methods
    * contains(str)
    * upper()
    * count(char)
* to import a specific function from a package
``` Python
from package import function
# rather than
import package
```
* dictionary
    * keys() must be immutable objects, i.e. it cannot be a list
    * del(dict[key])
    * for k,v in dict.items()
* tuple
    * immutable
    * (a,b,c)

* functions
```Python
def function(param):
        """DOCSTRINGS"""
```
    * nested functions
``` Python
def raise_val(n):
    def inner(x):
        return x**n
    return inner
square_val = raise_val(2)
cube_val = raise_val(3)
print (square_val(5), cube_val(4))  # return (25, 64)
```
    * **nonlocal**
```
def outer():
    n = 1
    def inner():
        nonlocal n
        n = 2
    inner()
    print(n)    # return 2
```
    * flexible arguments: 
        * default argument
        * *param_list for unrestricted number of params stored in a list 
        * *\*param_dict for params stored in a dict as param-value pairs
    * **lambda**
```Python
raise_to_power = lambda x,y: x**y
```
* iterable/iterator for when we don't actually want to create a list to iter through, eg. range($$10^{100}$$)
```
# Strings, lists and many other are an iterable
#    object which means they have an iter() method
#    that creates an iterator when called upon. 
it = iter('An')
next(it) #returns 'A'
print(*it) # returns A n
```

* zip(iterable1, iterable2) returns an object of tuples; use list() to convert zip object to list
* **Comprehensions**
    - list
```
matrix = [[col for col in range(5)] for row in range(5)]
new_fellowship = [member if len(member) >= 7 else \'\' for member in fellowship] 
dict = {}
```
- Generators use (); used to stream data
    - **yield** in generator functions
```
a = (member for member in fellowship if len(member) >=7 )
```
* **Context manager**
```
with open('world_dev_ind.csv') as file:
    file.readline() # to read in a line
```
## Visualizing tips
* make eCDF
## Import Data
* file = open(filename, mode='r'forReadOnly) or just use context manager
    * file.read()
    * file.close()
* flat file = .csv file or text file vs. relational file SQL stuff

----------------------------------------------------------
## Freq-used Packages
* sqlalchemy to do SQL query in a Pythonic way
    - create engine()
    - table_names() 
    - connect
    - select
        - where
        - and_, or_, all_, in_
        - order_by
        - func.count,sum
        - label
        - case
        - cast
    - group_by
    - fetchall, first, scalar
    - join to define relationships between tables
    - to join table to itself on different columns, create a copy of the table using alias()
* re
    * RegEx, ex: $17.895 = ^\\$\d*\\.\d{2}$ ; Australia = [A-Z]\w*
    * re.compile(pattern)
    * match
    * re.findall(pattern,string)
* builtins
* urllib.request to save file locally
    * urlretrieve
    * Request to package a reqeuest
    * urlopen to send a GET request and catch a response
    * read() to extract the HTML
* requests does the same thing as the above package in less code
    * requests.get()
    * text
    * json to decode json data into dict
* bs4 to parse HTML
    * BeautifulSoup
    * prettify()
    * title attribute
    * text attribute
    * find_all(tag)
* json to process data packaged from APIs
    * json.load() to load the file into a dict format
* tweepy to stream tweets
    * OAuthHandler(consumer_key, consumer_secret)
* math
* glob to do globbing
* numpy (arrays) == standard for storing numerical data
    * linspace(start,stop,n_default=50) to create a 1D vector of evenly spaced numbers 
    * reshape(-1,1) shapes whatever form to automatically inferred row size and column of 1
    * np.loadtxt(filename, delimiter=, skiprows=,usecols=,dtype=)
    * for cols with mixed datatypes use 
    np.genfromtxt(dtype=None, names=True means there is a header)
    * np.array(list); list with different Element types is converted to array of 1 type
    * shape
    * corrcoef(a,b)/mean/median/std
    * logical_and(/logical_or()/logical_not()
    * for val in np.nditer(2dlist) to print ea element from nested list
    * **random**
        * np.random.seed(num) for reproducibility
        * np.random.rand() gives a num between 0 and 1
        * np.random.randint(smaller, bigger)
    * transpose()
* scipy 
    * linalg
* seaborn - a statistical data visualization lib, default style nicer looking > plt
    * barplot(labels, data)
    * bee swarm plot (x,y,data)
* matplotlib.pyplot as plt
    * use _ as a dummy var to draw
    * plt.plot(x,y, style='colorMarkerLine') for line
    * plt.scatter(x,y,size=otherFeature,c=color,alpha=) for scatter plot
        * plt.xscale('log')
    * plt.hist(data,bins=numBins/binEdges, range=,normed=) -> binning problem -> use bee swarm plot
    * plt.xlabel('name')
    * plt.ylabel('name)
    * plt.title()
    * plt.x/yticks(list1, explanatoryList)
    * plt.text(x,y,'Name')
    * plt.grid(True)
    * plt.plot(subplots = True to draw each column separately, cumulative=True, normed=True for CDF)
    * rotation to rotate axis labels
    * plt.clf() clear figure 
    * plt.show()
    * plt.savefig()
* pandas (for data frames where each col is a Series (1D array with row labels) which yields np array on command series.values)
    * df.info()
    * pd.notnull(df).all().all() first all will return boolean for each col, second all will return one final boolean
    * pct_change() lastVal-thisVal
    * count()
    * quantile(num)
    * turn sth into categorical values by pd.Categorical(values=,categories,ordered=)
    * sum(axis='columns') to add horizontally
    * idxmax/min returns idx or row label of max value
    * unique() returns list of unique values
        * nunique() returns num of unique values
    * sort_values(ascending=False)
    * to merge df's
        * merge(left=, right=, on=, left_on=, right_on)
        * 1-to-1
        * many-to-many ???
    * to concatenate df's by stitching data from
        * top and bottom: use pd.concat([df1,df2], keys= ,ignore_index=True) to reset index
        * the sides: add axis = 1
        * join = 'inner' only matches columns of the same row labels
    * groupby(col)[cols].agg({col1:func1, col2:func2})
    * index
        * reset_index()
        * unstack(level=) multi-index to get shorter and wider df
        * flip indices by swaplevel()
        * sort_index()
    * pd.read_csv(fileName, header= chunksize=, names=colNames, na_values=, parse_dates for Time Series, comments=, index_col=) to read in data in chunks in for loop
    * df = pd.DataFrame(dict)
    * df.head()/tail()
    * indices are immutable, but can be reassigned by df.index= can be tuples
        * df.index.name
        * df.columns.name
    * df.dtypes
        * df[col].astype(str)
        * to_numeric(df[col], errors='coerce')
    * df.columns/shape attributes
    * slicing [::3, -1] every third row starting from index 0, last col
    * df.drop_duplicates() to drop row duplicates
        * df.dropna(how='any'/'all') to drop rows with missing values
        * df.fillna(anything)
    * df.plot(kind=, x=, y=,)
    * df.floordiv(num) floor the result of dividing by num
    * df.boxplot(column=,by=)
    * df.Colname.value_counts(dropna = False) to get the counts for each value in col
    * df.describe to get statistical summary of data
    * df.index = []
    * df.isnull/notnull chained with all()/any() 
    * **df[colName] returns Series**
        * df[[colName]] returns DF
    * pd.melt(id_vars = colsToKeepFIXED, value_vars=colsToMeltIntoRows, var_name=, value_name=) to turn columns into rows
        * versus pd.pivot(values=,index=colsNOTtoPivot,columns=) OR pd.pivot_table(aggfunc=) which allows one function parameter to deal with duplicate values
        <p align="center">
  <img src="../../img/post-img/python/1.png" height="50%" width="50%">
        </p>
    * pd.read_csv(file, index_col = colNumUsedAsRowLabel)
    * loc - index into DF by label
        * iloc - index into DF by index
```
# returns Series
cars.loc['RU']
cars.iloc[4]
# [[]] returns DF
cars.loc[['RU']]
cars.iloc[[4]]
cars.loc[['RU', 'AUS']]
cars.iloc[[4, 1]]
```
    * **Time Series**
        * set_index()
        * slicing with year, year-month, y-m-d
        * to_datetime to convert strings to datetime with specified format string
        * reindex(method='ffill/backfill')
        * resample('D' for daily, '2W' every 2 weeks) similar to group by
            * downsampling vs. upsampling (data sampled more freq)
            * rolling means .rolling().mean()
            * dt.hour to get hour
            * dt.tz_localize() / dt.tz.convert() to change time zone
            * interpolate('linear) to fill missing data linearly
* for label,row in df.iterrows():
* **apply**(function) applies a function on columns of DF
```Python
cars["newColumn"] = cars["someColumn"].apply(function)
```
--------------------------------------------------------------------------
## Scikit Learn
* display(df.head(n=3))
* train_test_split(random_state=seed,stratify=ToKeepTargetDistribution,test_size=0.3)
* Choose a scikit-learn classifier (e.g., adaboost, random forests) that has a feature_importance_ attribute, which is a function that ranks the importance of features according to the chosen classifier.
* from sklearn.decomposition import **PCA**
    * fit
    * explained_variance_ratio_  to get % of variances, how much variance within the data is explained by that dimension alone
    * components_ to get dimensions of PCs
    * transform
    * inverse_transform


* np.**percentile**(feature,percentile)

* data.**drop**(data.index[outliers]).reset_index(drop = True) to drop rows with those indices in outliers 

----------------------------------------

## Keras 
- load_model to load saved model by save('file.h5')
- model.summary()
- Sequential
    - to_categorical is same as one-hot-encoding
    - model.compile(heheh)
    - model.fit()
    - callbacks
        - earlyStoppingm(patience=num) used to stop training num epochs following the moment CV stops improving
- Conv2D
    * **filters** = numFilters
    * **kernel_size** = tuple of height and width of filter
    * **strides** = default to 1
    * **padding** = default to "valid":no, another options is "same"
    * **activation** = default to "relu"
    * **input_shape** = tuple of height, width, depth of first hidden layer
    * Flatten
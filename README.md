# Time Series DataAnalysis 
>keep similing while writting codes
>Description: In this project, we will study the use of statistical models and methods for
analyzing time-series data and their applications such as stock market prediction, monthly
unemployment figures, quarterly crime rates, and annual birth rates, etc. The main focus of this
project is on the understanding of the fundamental concepts of time series modeling. The
following models will be the main center of our research: stationary and nonstationary,
nonseasonal and seasonal, intervention and outlier, transfer function, regression time series,
and vector time series models. We will also implement these models in forecasting and
inference of the real world’s problems. We are also planning to prepare a series of students’
presentations to promote applied mathematical concepts such as a differential equation and
Fourier Analysis in data science across the campus.
------------------------------
# Table of contents
1. [Framework](#infrastructure)
2. [Data importation](#Data-importation)
    1. [Web scraping](#Web-scraping)
3. [Linear Regression](#Linear-Regression)

------------------------------------------------------------------
## Framework <a name="infrastructure"></a>

### How to write README.md 
* Using Markdow [Cheat](https://www.markdownguide.org/cheat-sheet/)
-------------------------------------------------------------------

### The Collaboration Setup for the project
* Setup Brew: [Brew](https://brew.sh/)
* Setup oh my zsh: [Zsh](https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/)
* Setup git and github:[git](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
    * git [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)

----------------------------------------------------------------------------------
### [Install Virtual Environment](https://virtualenv.pypa.io/en/latest/installation.html)
* Install:  brew and update it
* `pip3  install virtualenv`
* Check all the package in your global machine: `pip3 list` 
* Check: `virtualenv --version` 
* `virtualenv -p python3.9 <name_of_virtualenv>`
* Activate: `source ./<name_of_virtualenv>/bin/activate`
* Check which python is active: `which python `
* Deactivate when switch to another the application: `deactivate`
* To install new packages: `pip install <name of the package>`
* Copy local packages to requirements.txt: `pip freeze --local > requirements.txt`
* Check: `cat requirements.txt`
* git push requirement.txt to github
* To get all the package in your virtualenv: `pip install -r requirements.txt`
### Adding virtual enviroment into gitignore 
* `touch .gitignore`
* open .gitignore file and write the name of the files you want to ignore
* `git status`
* `git add .`
* `git commit -m "adding git ignore in working directory"`
* `git push`
#### Python Libraries:
```  
    import pandas as pd
    import pandas_datareader.data as web
    from datetime import datetime, timedelta
    import matplotlib.pyplot as plt
    import numpy as np
```

---------------------------------------------------------------------
## Data importation<a name="Data-importation"></a>

### Task 1: Data Management
#### 1. How to download data from the internet: 
1. Using Quandl
    1. `import quandl,math, datetime`
    2. `quandl.ApiConfig.api_key = "Token`
    3. `df=quandl.get("WIKI/GOOGL")`

2. *Using DataReader*
    1. 
    ``` 
    start_date = datetime(2015,1,1)
    end_date = datetime(2021,1,1)
    ticker = "AAPL"
    df = web.DataReader(ticker, 'yahoo', start=start_date, end=end_date)
    print(df)
    ```

#### 2. How to print/show the data in jupyternotebok?
1. `df.head()`
2. `print(d)`
#### 3. [How to how to save the data on your local machine in csv file?](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_csv.html)
1. `df.to_csv('Name_file.csv')`
#### 4. [How to how to read the data from your local machine of csv file?](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html)
1. `pd.read_csv('Name_file.csv', index_col=0)`
#### 5. How to clean the data ?
1. [Remvoning NAN values](https://datatofish.com/check-nan-pandas-dataframe/): `df.isnull().values.any()`
2. [Removing strings values](https://stackoverflow.com/questions/33413249/how-to-remove-string-value-from-column-in-pandas-dataframe)
#### 5. [How to plot the data](https://pandas.pydata.org/pandas-docs/stable/user_guide/visualization.html)
* Basic plotting

    1.  
    ```
        df["<column name>"].plot()
        plt.legend(loc=4)
        plt.xlabel("Date")
        plt.ylabel("Price")
        plt.show()
    ```
    2. 
    ```
        ts = pd.Series(np.asarray(df["<column name>"]),index=pd.date_range("1/1/2015", periods=len(np.asarray(df["<column name>"]))))
        ts.plot()
    ```




#### 6. Find a best way to visualize this data set ?


## [Linear Regression with python](https://www.kdnuggets.com/2019/03/beginners-guide-linear-regression-python-scikit-learn.html)<a name="Linear-Regression"></a>

* Choose X and Y 
    * The choice of X:
    ```
    import datetime as dt
    df = df.reset_index()
    df['Date'] = pd.to_datetime(df['Date'])
    df['Date']=df['Date'].map(dt.datetime.toordinal)
    X=df["Date"].values.reshape(-1, 1)
    ```
    * The chocie of Y:
    ```
    Y=df["Close"].values
    ```


* Fitting th Data into the model:
```
X_train, X_test, Y_train, Y_test = train_test_split(X,Y,train_size=.7,random_state=42)
model = LinearRegression() #create linear regression object
model.fit(X_train, Y_train) #train model on train data
accuracy=model.score(X_test,Y_test)
```
* One day Forcasting:
    * What day?
    ```
    l=len(X)-1
    day=1
    X_future=np.array(X[l])+day
    X_future
    ```
    * 
    ```
     forecast_set=model.predict(X_future)
     print(forecast_set)
     ```

-------





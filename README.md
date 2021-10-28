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
4. [Time Series Analysis](#time-series) 

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
    import datetime
    import pandas_datareader.data as web
    from datetime import datetime, timedelta
    import matplotlib.pyplot as plt
    import numpy as np
    import datetime as dt
    from sklearn.linear_model import LinearRegression
    from sklearn.model_selection import train_test_split
    import mpld3
    mpld3.enable_notebook()
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
    df_reset['Date'] = pd.to_datetime(df_reset['Date'])
    df_reset['Date']=df_reset['Date'].map(dt.datetime.toordinal)
    X=df_reset["Date"].values.reshape(-1, 1)
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
    day = 1
    X_future=np.array(X[-1:])+day
    X_future
    ```
    * 
    ```
     forecast_set=model.predict(X_future)
     print(forecast_set)
     ```
* How to do this for 30 days??
    * Setting up last date and future date 
    ```
    df["prediction"]=np.nan
    df_reset = df.reset_index()
    last_date=df.iloc[-1].name
    future_date= last_date+pd.DateOffset(days=30)
    ```
    * Creat data set from last date to final date
    ```
    s=pd.date_range(last_date, future_date, freq='D').to_series()
    d=s.dt.weekday
    df_future = pd.DataFrame(data=d,columns=['days'])
    df_future.index.name = 'Date'
    df_future.drop(df_future.index[df_future['days'] == 0], inplace = True)
    df_future.drop(df_future.index[df_future['days'] == 6], inplace = True)

    ```
    * Getting prediction data from our model
    ```
    df_future_reset = df_future.reset_index()
    df_future_reset['DateNummeric'] = pd.to_datetime(df_future_reset['Date'])
    df_future_reset['DateNummeric']=df_future_reset['Date'].map(dt.datetime.toordinal)
    X_future=df_future_reset["DateNummeric"].values.reshape(-1, 1)
    forecast_set=model.predict(X_future)
    df_future["prediction"]=forecast_set
    ```
    * 
    ```
    df_future["Close"] = np.nan 
    df_past= df[["Close","prediction"]]
    result = pd.concat([df_past,df_future])
    ````
    * ploting the resutl
    ```
    result.plot()
    ```
------------------------------------------------------------------------------------------------
## Time Sereis Analysis <a name="time-series"></a>

#### [What is time Series Analysis](https://www.youtube.com/watch?v=chp71nEc320&t=13s) 
#### [ Autocorrelation and Partial Autocorrelation](https://machinelearningmastery.com/gentle-introduction-autocorrelation-partial-autocorrelation/)
1. Create a new file with name ACF_and_PACF.pynb 
2. Import the following libraries of pythons 
```
import pandas as pd
import numpy as np
from statsmodels.tsa.stattools import acf, pacf
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
```
3. Lets first create a small pandas dataframe as 
```
df =pd.DataFrame({"a":[13,5,11,12,9,12,14,7,15]})
```
4. ### [ACF](https://www.statsmodels.org/stable/generated/statsmodels.tsa.stattools.acf.html)
    1. These codes will give us a array of correlation coefficient bewtweeen lags: ```array = acf(df["a"])```
    2. [Plot_ACF](https://www.statsmodels.org/dev/generated/statsmodels.graphics.tsaplots.plot_acf.html): These codes will give us a plot of the above array: `plot_acf(df["a"]])`
5. ### [PACF](https://www.statsmodels.org/stable/generated/statsmodels.tsa.stattools.pacf.html)
    1. These codes will give us a array of correlation coefficient bewtweeen lags: ```array = pacf(df["a"],lags=3)```
    2. These codes will give us a plot of the above array: `plot_pacf(df["a"], lags=3)`
6. Now repeat the above codes with actual stock market data. 

#### [What is Stationary time series](https://otexts.com/fpp2/stationarity.html)
    
- The stationary time series has the following three properties
    - The mean values is constant 
    - The variance of the series is constant 
    - There is no seasonality 
        - Note: White noise is a stationary time series with mean zero
1. #### Give the examples of non-stationary time series
    
2. #### Methods of finding the Stationarity of a time series
    - Visually 
    - Golbal vs Local test 
    - Augument Dickey -Fuller Test

3. #### How to make a time series Stationary 
    - If the mean is not constant: Take the derivative of the series

4. #### [What are the unite roots]()
A unit root (also called a unit root process or a difference stationary process) is a stochastic trend in a time series, sometimes called a random walk with drift”; If a time series has a unit root, it shows a systematic pattern that is unpredictable.

5. #### What is a Unit Root Test?
    - The Dickey Fuller Test (sometimes called a Dickey Pantula test), which is based on linear regression. Serial correlation can be anissue,  in which case the Augmented Dickey-Fuller (ADF) test can be used. The ADF handles bigger, more complex models. It does have the downside of a fairly high Type I error rate.
        - The Elliott–Rothenberg–Stock Test, which has two subtypes:
            - The P-test takes the error term’s serial correlation into account,
            - The DF-GLS test can be applied to detrended data without intercept.
        - The Schmidt–Phillips Test includes the coefficients of the deterministic variables in the null and alternate hypotheses. Subtypes   are  the rho-test and the tau-test.
        - The Phillips–Perron (PP) Test is a modification of the Dickey Fuller test, and corrects for autocorrelation and heteroscedasticity in the errors.
        - The Zivot-Andrews test allows a break at an unknown point in the intercept or linear trend.

5.  #### [Augument Dickey -Fuller Test](https://www.statology.org/dickey-fuller-test-python/)
    - Coding of dickey-fuller test
        * Library
        ```
        import matplotlib.pyplot as plt
        import numpy as np
        from statsmodels.tsa.stattools import adfuller

        ```
        * ADf 
        ```
        data = [3, 4, 4, 5, 6, 7, 6, 6, 7, 8, 9, 12, 10]
        Result_adf = adfuller(data)
        print('ADF Statistic: %f' % Result_adf[0])
        print('p-value: %f' % Result_adf[1])
        ```







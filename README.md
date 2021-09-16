# Time Series DataAnalysis 
>keep similing while writting codes
--------------------------
## How to write README.md: Using Markdow Cheat: [Cheatme](https://www.markdownguide.org/cheat-sheet/)
--------------------------

## The Collaboration Setup for the project
--------------------------
* Setup Brew: [Brew](https://brew.sh/)
* Setup oh my zsh: [Zsh](https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/)
* Setup git and github:[git](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
    * git [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)

----------------------------------------------------------------------------------
### [Install Virtual Environment](https://virtualenv.pypa.io/en/latest/installation.html)
* Install:  brew and update it
* pipx install pyenv-virtualenv 
* Check: virtualenv ---version 
* virtualenv -p python3.9 <name_of_virtualenv>
* Activate: "source ./<name_of_virtualenv>/bin/activate"
* Check: python3 --version
* Deactivate: $deactivate



---------------------------------------------------------------------
## Task 1: Cleaning data 
#### 1. How to download data from the internet: 
    1. Using Quandl
        1. "import quandl,math, datetime"
        2. quandl.ApiConfig.api_key = "Token" 
        3. "df=quandl.get("WIKI/GOOGL")"

    2. * Using DataReader *
        1. 'df = web.DataReader('<ticker>', 'yahoo', start=start_date, end=end_date)'

### 2. How to clean the data ?
    1. Remvoning NAN values?
    2. Removing strings values?
### 3. How to scale the data ?

### 4. How to plot the data ?

### 5. Find a best way to visualize this data set ?


## [Linear Regression with python](https://www.kdnuggets.com/2019/03/beginners-guide-linear-regression-python-scikit-learn.html)

-------


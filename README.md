# Time Series DataAnalysis 
>keep similing while writting codes
--------------------------
## Markdow Cheat: [Cheatme](https://www.markdownguide.org/cheat-sheet/)
--------------------------

## The Setup for the project

### [Install Virtual Environment](https://virtualenv.pypa.io/en/latest/installation.html)
--------------------------
* Setup Brew: [Brew](https://brew.sh/)
* Setup oh my zsh: [Zsh](https://www.freecodecamp.org/news/how-to-configure-your-macos-terminal-with-zsh-like-a-pro-c0ab3f3c1156/)
* Setup git and github:[git](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup)
    * git [cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf)
* Setup virtual Environment:[Virtual Environment]()
    * Install:  brew and update it
    * pipx install pyenv-virtualenv 
    * Check: virtualenv ---version 
    * virtualenv -p python3.9 <name_of_virtualenv>
    * Activate: $source ./<name_of_virtualenv>/bin/activate
    * Check: python3 --version
    * Deactivate: $deactivate
    


---------------------------------------------------------------------
## Phase 1: Cleaning data 
#### How to download data from the internet: 
    1. Using Quandl
        1. "import quandl,math, datetime"
        2. quandl.ApiConfig.api_key = "Token" 
        3. "df=quandl.get("WIKI/GOOGL")"

    2. * Using DataReader *
        1. 'df = web.DataReader('<ticker>', 'yahoo', start=start_date, end=end_date)'

    3.

## [Linear Regression with python](https://www.kdnuggets.com/2019/03/beginners-guide-linear-regression-python-scikit-learn.html)

-------


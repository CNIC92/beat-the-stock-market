# STOCKS PERFORMANCE PREDICTOR

This project begins from a question I asked myself during the 2019 winter holidays: **it is possible to understand which stock will perform well in the year *t* using only financial data available for the year *t-1*?** 

One approach could be the development of a model that, after being trained with historical price data, will be tasked with the prediction of the future price of a given stock or group of stocks. This has shown some potential, especially via the application of LSTM cells and 1D-CNNs.
However, the stock price allows to get a glimpse of the bigger picture. For example, a stock price may be inflated by speculators, or a general market trend (such as the current bull market), etc: I am not confident in the ability of a model/neural network to understand these macro-economic trends. This is why other aspects such as sentiment analysis have also been developed and became quite popular.

Therefore, instead of loading years and years of historical data into a model, I decided that maybe it is more useful and interesting to look at financial and fundamental data. These are the kind of data that it is possible to find in the 10-K filings released yearly by companies (US)(10-Q for the quarterly data). In my opinion, many indicators present in the filings are *harder* to inflate/deflate compared to the trading price. So, they should be able to give a better representation of the true value of a company, possibly leading to a characterization that can be exploited to make sensible predictions about its future state.

I decided to interpret this as a classification problem, in which a model is tasked with the classification of a list of stocks between stocks that will increase their value and stocks that will not increase their value (binary classication). However, it is quite simple to translate this into a regression problem, where the output of the model becomes the predicted value at a future time-step.

With that being said, this notebook is structured in the following parts:

### 1. DATA
I decided to **not** use any already available dataset (as they can be found on Kaggle, Reddit, etc) and to build my own, in order to have full control on its structure, and to improve my data scraping and analysis abilities. I decided to use the Financial Modeling Prep API (https://financialmodelingprep.com/developer/docs). This is a very simple to use API, and it makes possible to scrape a lot of financial data for a lot of stocks for free. I highly recommend it!

### 2. MODELS
As of now, I decided to implement some of the most popular Machine Learning algorithms to solve the classification problem. The algorithms are:
  * Support Vector Machine (from https://scikit-learn.org/stable/modules/generated/sklearn.svm.SVC.html);
  * Random Forest (from https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html);
  * Extreme Gradient Boosting (from https://xgboost.readthedocs.io/en/latest/python/python_intro.html);
  * Feed-forward Neural Network (from https://scikit-learn.org/stable/modules/generated/sklearn.neural_network.MLPClassifier.html).
 
The main hyper-parameters of each algorithm are optimized through the `GridSearchCV` method (with `cv=5`).

#### 2.1 EVALUATION
The evaluation of the performance of each algorithm consists in a 2-step process:

  a. Evaluate testing accuracy of the model when analyzing the testing dataset.
  
  b. Evaluate the gain/loss in $USD if you were to follow the predictions of the models. In other words, which model allows me to make the most money? How do the models compare to the benchmarks (S&P 500, Dow Jones)?


### FUTURE DEVELOPMENTS

  * I would like to run the notebook with data from past years (2017, 2016, 2015, 2014, ...) in order to evaluate the robustness and actual performance of the models/workflow.

  * Many models can be added to the ones already present (others neural network architectures, decision trees, naive bayes classifiers, linear and logist classifiers, ...).

  * Performing dimensionality reduction (PCA, SVD) on the dataset might be beneficial in order to remove redundant information.
  
### ABOUT ME
I am a Mechanical Engineer with a M.Sc. in Advanced Mechanical Design. Machine learning is both part of my job and part of my hobbies. Find me at:
nicolascarbone92@outlook.com
https://www.linkedin.com/in/nicolas-carbone/

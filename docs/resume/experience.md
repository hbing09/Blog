# 简历准备

# Self-Introduction
****
This is Hazel, currently I’m working at Morgan Stanley as a data analyst, under Firm Risk Department, Risk Infrastructure team. In the past one year and a half at Morgan Stanley, I gained some experience in building dashboards, and being more familiar with risk-related business. As for the reason why I want to move, is that I want to seek for more challenges, doing something not only focusing on risk.
So I’m pretty interested in your team about what you do.

# Morgan Stanley 
----------
1. Big picture: 
    To give you a big picture of what I’m doing, our team is at the end of the data flow. 
    - **Basically, we received the data processed by various teams in the firm, and then create dashboards/reports for different stakeholders.** 
    - **The data sources can be very diverse, for example, the the daily PnL, trading exposure, results of some risk models, like VaR or scenario analysis.** 
    - **The stakeholders include risk managers, traders and regulators.** 
    - **Also, we prepare the documents for senior manager’s committee meeting every month.**
    
1. The dashboards I built are about the market risk portfolio level dashboards and stress testing dashboards. The challenging part can be the diverse data source, ongoing structure change, interaction among different dashboards, and back and forth discussion with clients about the design ideas. For example, like what kind of story would be helpful, how to convey the message efficiently? 
    1. Data source: the data source can be some internal system, different risk systems, PnL, historical database; or some external source, like Bloomberg, Horizon, or Risk-1. We need to do adjustment / calculation based on the data we have. Sometimes we need to integrate the dashboards from other team as well.
    2. Structure change: We must be very familiar with the Firm’s ISG structure (Institutional Securities Group), and usually due to some business reason, the front office will propose some structure changes every month. We would receive the change notice around the middle of the month about the change that will go live next month. So before that, we need to estimate the impact and change our current logic and do some testing.
    3. Interaction among different dashboards: I could say, all dashboards are related, like portfolio level and each desk level; Firm level and FID level. Although they come from different data source, and there are different adjustments. The numbers on each dashboard should tie with the
    4. Design: we have a design guideline, like the color, and formatting. Considering the purpose and the audience of the dashboards/reports, we should consider different factors. 
        1. For risk managers, mostly it’s daily refreshed, and it’s for better risk monitoring, whenever there is some weird numbers, which can be an alert, I need to help risk managers dig into it to see know what happened in business.
        2. For senior management, for example, for Firm Risk Committee, our dashboard will be used in the monthly meeting held by chief risk officer. My portfolio dashboard and trading risk exposure dashboard are part of this one.
        
2. Possible conceptual questions
    1. VaR:
    2. Explain the Greeks for options
    3. ATM option delta value?
    4. Explain the assumptions behind Black-Scholes
# OmniMarkets

Quantitative Analyst Intern Mar. 2018 - May 2018

- Applied SVR and GBDT in option pricing prediction using 10-year historical data from Bloomberg
- Tuned model parameters by grid search and improved pricing accuracy over 40% compared to BS Model
- Organized weekly panel discussion for peer review, performed presentations to risk and management teams
----------
1. Big Picture
    This is a company who provide risk management consulting services for financial institutions to model, price and process financial products in various asset classes. 
    Our client includes U.S. Investment Banks, Foreign Bank Organizations, Asset Managers and Fund Managers.


    The project I did here is to work on writing a challenger model for traditional option pricing method, Black Sholes model. 
    Challenger model is to validate the results and evaluate the performance of the model over time.
    
    The traditional option pricing method is using Black-Scholes formula, while the assumptions of the method are often violated in reality. So we want to train an algorithm to learn from the history data in the market and make prediction without making any assumptions about the relationships between input variables.
    
1. Related work
    In recent years, nonparametric methods are used for prediction. Because they are suitable to adjust changing behavior of the derivative securities as they can be trained from time to time.
    
    Since 1994, neural network are used in option pricing and it performed fairly well. 
    
    Support Vector Machine is a powerful tool and it has been widely used for classification, pattern recognition and nonlinear function estimation. And it's found that when it's used for regression, it can provide much better results than neural network. 
    
    Gradient Boosting Decision Tree is also a method proved to be powerful in option pricing.
    
2. BSM
    Background: Challenger model is to validate the results and evaluate the performance of the model over time.
    
    The Black-Scholes approach to option pricing is one of the most important ideas in finance.
    
    Assumptions:
    1. The price of a stock follows a geometric Brownian motion with constant volatility.
    2. efficient markets. stocks move like random walk. At any given moment, the price of the underlying stock can go up or go down with the same probability.
    3. No dividends.
    4. constant and known interest rates.
    5. No transaction costs and commissions.
    
    Inputs:
    - Current stock price
    - Option strike price
    - time to expiration (denoted as a percent of year)
    - risk-free interest rates
    
    Output:
    - Option price
    
    Shortcoming:
    In practice, assume the BS formula is correct and to solve the volatility by inverting the formula. However, BS implies that the volatilities obtained from options on the same stock are constant across different strikes K and maturities T. And prices in the markets do not exactly come from BSM.
    
    So it is possible to train an algorithm to learn from the history data in the market and make prediction without making any assumptions about the relationships between input variables.
    
    And these machine learning models are nonparametric
    
3. Methodology
    SVM: use a kernal to transform the data to one dimension, and make regression
    - pro
        - fewer hyperparameters with robust result
        - no assumptions of the non-linear functional transformation
    - con
        - time consuming
        
1. GBDT
    1. Regression Decision Tree
        - builds regression in the form of a tree structure. 
        - breaks down a dataset into smaller and smaller subsets.
        - the result is a tree with decision nodes and leaf nodes.
        - tree regression models calculate the relative importance of predictors, and the relative importance of predictors can be computed by sum of squared error.
        - it's like a complicated linear regression at each leaf node, and there is a prediction score in each leaf.
        
    2. Gradient boosting
        - Assume the tree is not a perfect model, so every time, each successive tree uses the residuals of the previous tree. In this way, it has strong predictive power.
        - Shrinkage, give a weight to each tree
        - It is an ensemble of many trees.
        - Through control the learning rate, number of estimations, max_depth and max_features, etc.
    3. pros
        - fast * doesn't require careful normalization of features to perform well.
    4. cons
        - difficult to interpret * require the contraint of learning rate 
        
    - Data preparation
        - AAPL, from 2002 to 2010.
        - Inputs: underlying price , strike price, time to expiration, volatility, risk-free interest rate, Black-Scholes option price.
        - remove data that have trading volume less than 100.
        - remove data that have zero trading volume
        - all options with less than 6 days or more than 260 days to expiration are eliminated to avoid extreme option prices that are observed due to potential liquidity problem.
        - after the data cleaning, there are 215393
        - split the data into training data set 70% and testing data set 30%.
        Performance measurement: Explained Variance, MSE
        
    1. Conclusion
        SVR can further be improved by changing the input variables in different conditions. for example, deep-in-the-money option, at-the-money option, out-of-the-money option.
# Forwardlane

Data Science Intern June 2017 - Aug. 2017

- Evaluated portfolio’s performance using efficient frontier generated by Monte Carlo simulation; computed ex-ante analytics using Smart Risk APIs to understand portfolio structure
- Worked with ETF database using SQL Server and categorized ETFs by K-means
- Optimized portfolios and developed real-time automatic recommender based on clients’ risk preference
- Implemented NLP techniques to create Q&A database from Morningstar, Bloomberg news
----------
1. Big picture
    ForwardLane is a fin-tech startup based in New York, it is building a robo-advisor platform which can provide real-time investment solutions to the investors. I helped develop a recommendation model for optimizing the portfolios by applying clustering algorithm and Monte Carlo simulation. The goal of this model is to give online clients customized recommendations to improve their current portfolio. And the language I use are mainly Python and SQL.
    

Using current portfolio's components and the investor's risk appetite as input, the model will automatically add or delete some elements in the portfolio and then allocate the proportion of the assets to satisfy clients' need. 

**For example**, if you are a user of this platform, after you log in and enter into the conversation interface, it will ask your current asset allocation and your risk appetite. Then, it will analyze your portfolio structure and optimize it. 

**How to optimize? First**, it will determine which financial products should be in your portfolio, based on correlation analysis, some elements will be deleted, or it will select some other well-performing products from our database. And after choosing the right products, **the next step** is to adjust the allocation based on **efficient frontier** and your risk appetite. 

In this process, how to select products for adding them to your portfolio? I implemented clustering algorithm.

**Why choose cluster?** For example, for the ETF database, there are thousands of products and it is impossible to try one by one because it is quite time-consuming. So I will firstly cluster all the ETFs to different clusters based on their similarity of risk and return profile using k-means cluster algorithm. In this way I can smaller the ETF universe.

**How to draw efficient frontier?** I ran thousands of times Monte Carlo simulation in Python to simulate as much as possible combinations of this portfolio, and every possible combination of assets plotted on graph. Plots return and risk(std. deviation). Optimal portfolio lies on the efficient frontier curve. 

Monte Carlo simulation: use repeated random sampling to obtain numerical results

**How do you do the classification?**

For each ETF, we calculate the efficient frontier to go back for one year historical data, we calculate the volatility, which we consider risk for this period, we calculate the expected return for the last year period, and then you have the risk and return profile, the next what we do is o draw a coordinate axis, the x axis is the risk and y is your return, for each combination, you have a point in the coordinate, the similar risk and return profile as one cluster.

Evaluated the portfolio's performance using simulating the efficient frontier and Raise Partner's API   https://raisepartner.com/?lang=en

Compute ex-ante portfolio analytics and multi-classification contributions to understand the sources of risk and performance in your portfolio. 

Define optimal and robust portfolios while meeting regulatory and business constraints

# Movie Rating Prediction and Recommendation

• Developed a recommendation system based on MovieLens Dataset with 26 million ratings on 45,000 movies, and conducted online analytical processing via Spark
• Designed a collaborative filtering algorithm based on similarity scores to provide personalized movie recommendations and developed user-based approaches to handle system cold-start problem
• Conducted model hyper-parameters tuning based on cross evaluation components and monitored data processing performance on AWS


this is a course project

**how do you know about AWS?**
S3: is for data storage
EC2: is for calculation
EMR: is a bunch of EC2s







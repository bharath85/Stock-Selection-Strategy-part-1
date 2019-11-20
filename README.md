Portfolio Allocation Strategies for the Defensive Investor
The objective of this project is to compare returns for different investment strategies for multiple stocks.
Before diving deep we need to understand the basis of this project. My basic approach to building a Portfolio Optimization is based on the Modern Portfolio Theory (MPT) by Harry Markowitz which states that “if an investor is willing to take higher risk then it needs to be compensated with high return. If a portfolio gives same return for a given risk then the investor will choose the one with low risk.”
Higher risk is associated with greater probability of higher return and lower risk with a greater probability of smaller return. MPT assumes that investors are risk-averse, meaning that given two portfolios that offer the same expected return, investors will prefer the less risky one. Thus, an investor will take on increased risk only if compensated by higher expected returns.
Another factor comes in to play in MPT is “diversification”. Modern portfolio theory says that it is not enough to look at the expected risk and return of one particular stock. By investing in more than one stock, an investor can reap the benefits of diversification — chief among them, a reduction in the riskiness of the portfolio.
Also, in order to get a better understand of portfolio risk which is not just the simple average / weighted average of volatility of individuals stocks but you also need to how stocks movement correlates with one another. 	
Investment strategies mainly include Active and Passive. These are also known as Aggressive investing and Defensive investing. 
Active investment is basically managing (buy & sell) stocks on a regular basis; it could be daily or monthly. Whereas Passive investing is creating a portfolio of stocks, compute their returns for a specific period and invest. This doesn’t consider short term stock falls or sudden political changes that affect the selected stocks. 
For this project I’ll be starting with a Passive / Defensive investment strategy so that it will form a base for Active / Aggressive investing. In this Defensive Investment Strategy there are mainly two risk strategies that an investor can choose based on his / her risk acceptance level.
1.	High risk high return 
2.	Low risk low return 
 
In my code I’ll show how to select stocks based on their P/E ratio and compare returns for multiple investment strategies. While there are many technical indicators to select a stock P/E ratio is a good place to start. You can create a portfolio with any random stocks but in most cases the portfolio performance will not be acceptable. 
1.	Stock selection strategy using P/E Ratio. For the portfolio I’ve selected 4 stocks from each category – Bluechip, Midcap and Smallcap along with varied P/E value to see how it affects the final portfolio performance.  
2.	Data Download – The NSE python library gives you access to current and historical market prices and it’s very easy to call the data. 
 

 
3.	Data Exploration – Let’s plot the price of stocks to see their trend for the past 5 years. 
 
Clearly HeroMotoCo and Venkeys have a relatively high which makes it difficult to understand the trend of other stocks.

To understand better we will plot the volatility of the stocks using the daily returns / percentage change.     

From the above three graphs we can clearly see that Bluechip stocks have low standard deviation whereas the standard deviation increases for Midcap and higher for Smallcap stocks. So, at this point we can assume that if we make a high risk - high return portfolio the weights allocation could be higher for small cap stocks.
Although there are two major negative spikes in Bluechip stocks it was due to 
•	Indian Oil Corporation has major negative change in Oct 2019 due to govt. decision to cut Rs.1 
•	As for NTPC it was due to Ex-bonus issue, so no major risk there. 

4.	Optimization using Monte Carlo Simulation
Our objective here is to create a portfolio of 12 stocks with optimum allocation of the budget for both the high risk and low risk strategies. 
We initiate the simulation with 12 stocks and 25000 random portfolios. The factors we consider for the portfolio are
1.	Mean returns annually is calculated as below
∑(Mean Returns * Weights) * 252
2.	Standard deviation is calculated using the below formula
  
To compute annually,  we multiply it with √252.

3.	For portfolio performance I’ll be using Sharpe ratio 
 
		Here, we can take the risk free rate as the govt. bond yield of 6.9% which is nothing but what an investor would get with zero risk. 
 
Once we run the simulation we can plot the results by visualizing using the efficient frontier. 
  
Green star indicates the portfolio with lowest risk possible with current selection of stocks and red star indicates Max Sharpe ratio / high risk high return portfolio. 
From the plot of the randomly simulated portfolios, we can see it forms a shape of an arch line on the top of clustered blue dots. This line is called efficient frontier. Why is it efficient? Because points along the line will give you the lowest risk for a given target return. All the other dots right to the line will give you higher risk with same returns. If the expected returns are the same, why would you take an extra risk when there’s an option with lower risk?
5.	Optimization using python library ‘Pypfopt’
The library uses Sharpe ratio as objective function so we don’t have to custom define our function. And, as for the constraints we need give the bounds of weights between 0 and 1. 
Visualizing the weights:
 
 

For High risk high return strategy in Monte Carlo simulation it has given very low weights to Bluechip stocks and high weights to Smallcap stocks where Pypfopt optimization library has completely rounded the weights to 0 for Bluechip stocks. 
While in the cases of low risk strategy in both approaches nearly 50% weightage is given to Bluechip stocks.  As we have seen from the volatility graphs above it seems clear that for a low risk strategy the optimization weights are high for low volatile stocks and for a high risk strategy higher weights are given to more volatile stocks. 

What’s Next? 
Using one or more technical indicators such as RSI or Bollinger bands to identify buy and sell positions and simulate trades for our selected stocks and compare returns. 

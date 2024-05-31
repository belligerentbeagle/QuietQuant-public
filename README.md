# Options trading automated
With usage of IBKR's APIs, we can automate the trading of options based on the intrinsic value of the underlying stock. The manual strategy generates an estimated 20% per month on a 6 figure portfolio. 

Working with 2 semi-retired traders, we are developing a tool to automate a various parts of the trading process of a variety of options strategies, proven profitable over the last decade.

# Topics touched on in this project:
## Software Development 
### Tech Stack
1. Python
1. Streamlit
1. Selenium
1. IBKR API
1. FinanceToolkit
1. Yahoo Finance API
1. AlphaVantage API
1. RapidAPI

### Concepts
1. OOP
1. Web scraping
1. IBKR API usage (trade execution)
1. Financial data analysis
1. Options trading
1. Automated trading
1. Stock valuation, screening
1. Stock market analysis

## Math/Finance
1. Intrinsic value calculation
1. Discount rate calculation
1. Options trading strategies
1. Portfolio Optimization e.g. Efficient Frontier, Kelly Criterion
1. Black-Scholes model


# Architecture
## Phase 1: Gathering data, calculate intrinsic value of assets
![Architecture](./public/images/architecturePhase1.png)

`streamlit main file -- sends growthrates and list of stocks to calculate ---> IntrinsicValueCalculator -- sends stock symbols ---> fetchTickerData 
-- gets fundamental data from online sources --> to IntrinsicValueCalculator to create Stock objects --- sends objects to streamlit main file to display as table --> streamlit main file.
`

## Phase 2: Gather top stock tickers from proprietary website ranked based on ROI of options. 


## Phase 3: Execute trades through IBKR that meet criteria for proprietary columns


## Phase 4: Use ML (NLP) to estimate 3-tier growth rates for companies


# Fundamental data APIs
## AlphaVantage API use:
Limit 25 requests per day
- docs link: https://www.alphavantage.co/documentation/

## FinanceToolkit (opensource)
Limit 250 requests per day and uses FinancialModelingPrep under the hood (only US stocks) and free version only has annual data
- docs link: https://www.jeroenbouma.com/projects/financetoolkit/docs
- pypi link: https://pypi.org/project/financetoolkit/

## No longer using:
## Tiingo
Limit 1000 requests per day, max 50 per hour
- docs link: https://www.tiingo.com/documentation/fundamentals


# Improvements:
- [X] Handled missing financial data case
- [X] Fail safe: Fetch financial data from 2 sources - Tiingo and Yahoo Finance to compare 3FS discrepency. (5% tolerance)
- [X] Automate finding of discount rate as well.
- [X] Add current stock price comparison
- [X] Error handling -> if data not available. Write error message as well.
- [ ] Concurrent fetching of data
- [X] Scrape Options data from online source 




# Change log:
29 May:
1. Webscrape with selenium from a website for highest ROI options.
1. Run intrinsic value calculation on this basket of stocks
1. Error handling of missing values from financial reports

23 May:
1. Added auto pulling of discount rate.   


22 May:
1. Fixed to Annual report data for Cashflow
1. Changed API provider with a higher API limit (AlphaVantage to Tiingo, from 25 req/day to 1000 req/day free)
1. Changed away from Tiingo after realising that their fundamental data is free only for DOW30 stocks. Trying Yahoo finance via Rapid API
1. Changed to FinanceToolkit: an open source toolkit gathering financial data with transparent methods of calculations.
1. Use YahooFinance API through RapidAPI to get current stock price


# Archive
## Public Financial data sources
1. financialmodelingprep.com 
1. https://github.com/JerBouma/FinanceToolkit
1. https://www.alphavantage.co/documentation/
1. https://www.tiingo.com/documentation/fundamentals
1. https://rapidapi.com/apidojo/api/yahoo-finance1


# Uncertain Parts/Details:
> Q: When missing financial data for some companies, for e.g. shortTermDebt is None, should we stop the calc. of Intrinsic Value?
A: Yes

# stock-screener-python
using python to do stock screening among the stocks listed in SnP 500.

## Overview
- 1st section: Equal Weight of SnP 500
- 2nd section: Quantitative Momentum strategy
- 3rd section: Quantitative Value Strategy

### Goal: using computer to list down 50 recommended stocks to buy in SnP 500. The computer make the investment decisions. 
many different type of algorithmic trading, main difference is the speed of the execution.

<details>
<summary>About Numpy Library</summary>

- Most popular python library for numerical computing
- Numpy Array can store & manipulate 1D or 2D data structure
- For more info [Click Here](https://numpy.org/doc/stable/)

</details>

## Algorithmic Trading Process:
1. Collect Data. (from API or other means)
2. Develop hypothesis for a strategy.
3. Back test the strategy.
4. Implement the strategy in practice.

<details>
<summary>API (Application Programming Interface)</summary>

- A way for software to interact with & potentially control someone else's software.
- In this course, GET requests is used to gather stock market data from IEX Cloud API.
- Other API functionality:
  1. POST: Adds data to database exposed by API (create only)
  2. PUT: Add and Overwrite data in database exposed by API (create and replace)
  3. DELETE: Delete data from API's Database

</details>

Momentum investing: investing in assets that increased in price the most  
Value investing: investing in assets that are trading below their intrinsic value.

## Algorithmic value investing relies on the concept of 'multiples'.
- Multiples is calculated by dividing stock price with some measure of the company worth.
  - Price to earning ratio, price to book ratio, price to free cash flow ratio.
- One way to minimize impact of any specific multiples is by using composite.
  - Composite is average of many different valuation strategy.

## Addtional Notes
<details>
<summary>1st Project: Equal Weight of SnP 500</summary>

- Add base url when making API call. Add specific endpoint that to be retrieved from the API.
- In this project, market cap and price endpoint is needed. Only managed to find marketcap only. Hence search for 'quote' endpoint that provide both of those keys.
- API url can be transformed into 'F string' to bind variable into url. Handy for looping url with different variable endpoint.
- /stable/ can be added after the base url to get the latest stable API version. /latest/ can be added instead if we want latest API version in beta mode(not stable nor fully tested)
-use requests.get with API url while adding JSON at the back to retrieve data. Data can be refered to documentation to make sense out of it.

Batch API call
-	Batch API url can be looked up on documentation.
-	Doing batch API by appending empty dataframe with panda series with a list inside. All this within a loop. Eg(dataframe.append(pd.Series([….. , …… , …..]))

Had an error that said (Key error = ‘DISCA’). This is bcs the company was delisted from SnP 500, hence need to exclude a list of companies in the second cell of Jupyter notebook. A better approach is to update the list of stocks in SnP 500.


</details>

<details>
<summary>2nd project & 3rd Project</summary>

- To get % return of a stock, sometimes need to search 'change' instead of 'return'. At around 241/457, we get the parameter we want.
- The parameter can't be initiated with numbers, hence 'year2changepercentage' is basically 2 years change percentage.
- You can put 'price' endpoint to access stock price instead 'quote'. The parsing would appear 'data[symbol]['price']' instead of "data[symbol]['quote']['latestPrice']". It's much faster this way.
- Some stock shows 'None' for 1 year price return because they simply don't have the value. this can be solved by using data cleaning.

Handy formulas
- Position_size = portfolio_size/len(dataframe.index)
- Num of shares to buy = position_size/price

HQM score is the mean score of 1 year, 6 months, 3 months, 1 month price return. From there, we take the top 50 HQM score.

</details>

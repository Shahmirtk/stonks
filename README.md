# stonks
Stocks data and analysis code.<br><br>
link.txt contains a link to Wall Street Journal for downloading a specific stock. Replace FFC with desired symbol. Set startDate and endDate as needed. Might need to update num_rows and range_days. Try downloading from WSJ to get an idea.<br><br>
returns.csv contains stock wise 60 months returns. (For Jul-2020 to Jul-2025)<br><br>
kse100.csv contains 60 months returns of KSE100. (Same as returns.csv)<br><br>
order_by_market_cap.csv orders stocks by market cap. First has highest market cap.<br><br>
portfolios.csv contains the weights for each stock in a portfolio.<br><br>
sbp_yield_data.csv is taken from SBP and provides yield info.<br><br>
yield.ipynb analyzes yield info.<br><br>
benchmark.ipynb analyzes portfolios against the KSE100.<br><br>
algo.md provides instructions on the Genetic Algorithm implementation.<br><br>

Potential further research:<br>
- Enhancing the algorithm by further local search instead of relying on global optimization only.
- Adding fixed income to a portfolio.
<br><br>

Credits: WSJ, PSX, SBP.<br>

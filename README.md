# Finance-related-projects

## Plots with different scales
```
import yfinance as yf
import pandas as pd
import matplotlib.pyplot as plt

# Function to fetch stock data
def get_stock_data(tickers, start_date, end_date):
    data = yf.download(tickers, start=start_date, end=end_date)
    return data['Close']

# Function to fetch VIX data
def get_vix_data(start_date, end_date):
    vix_data = yf.download("^VIX", start=start_date, end=end_date)
    return vix_data['Close']

# Define the time frame
start_date = '2024-01-01'
end_date = '2024-03-10'

# Define the tickers of the stocks you want to plot
stock_tickers = ['NVDA']

# Fetch stock data
stock_prices = get_stock_data(stock_tickers, start_date, end_date)
stock_prices_rgti = get_stock_data(stock_tickers_rgti, start_date, end_date)

# Fetch VIX data
vix_data = get_vix_data(start_date, end_date)

fig, ax1 = plt.subplots()

color = 'tab:red'
ax1.set_xlabel("time")
ax1.set_ylabel('Closing Price of RGTI', color=color)
ax1.plot(stock_prices_rgti, color=color)
ax1.tick_params(axis='y', labelcolor=color)

ax2 = ax1.twinx()

color = 'tab:blue'
ax2.set_ylabel('VIX Index', color=color)  # we already handled the x-label with ax1
ax2.plot(vix_data , color=color)
ax2.tick_params(axis='y', labelcolor=color)


# Adding reference lines
ax1.axhline(y=200, color='gray', linestyle='--')  # Horizontal line at y=200 for stock price
ax2.axhline(y=20, color='green', linestyle='--')  # Horizontal line at y=20 for VIX index

# Adding a vertical line
ax1.axvline(x=pd.Timestamp('2024-02-15'), color='red', linestyle='--')  # Vertical line at February 15, 2024

fig.tight_layout()  # otherwise, the right y-label is slightly clipped
plt.title('Stock Price of NVDA and VIX Index')
plt.show()
```
<img src="images/VIX_and_NVDA.png?" width="400" height="300"/>


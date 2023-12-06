# usdTOeur
# import necessary packages
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

#import historical data of EUR/USD
data = pd.read_csv('/Users/jackneill/Downloads/EUR_USD Historical Data.csv')

#example of raw data
print(data.head())

#convert dates column to date format and initalize as key variable
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)

# EUR to USD Exchange Rate 1999-2019
plt.figure(figsize=(12, 6))
sns.lineplot(x=data.index, y=data['Price'])
plt.title('EUR to USD Exchange Rate 1999-2019')
plt.xlabel('Date')
plt.ylabel('EUR/USD Conversion Rate')
plt.show()

# Calculate Yearly moving average
data['Yearly_MA'] = data['Price'].rolling(window=365).mean()

# Plot the original and moving average data
plt.figure(figsize=(12, 6))
sns.lineplot(x=data.index, y=data['Price'], label='Original')
sns.lineplot(x=data.index, y=data['Yearly_MA'], label='Yearly Moving Average')
plt.title('EUR to USD Exchange Rate with Moving Yearly Average 1999-2019')
plt.xlabel('Date')
plt.ylabel('EUR/USD Conversion Rate')
plt.legend()
plt.show()

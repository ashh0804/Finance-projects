# Finance-projects
Using data manipulation in projects connecting to finance.
git remote add origin https://github.com/ashh0804/Finance-projects.git
git branch -M main
git push -u origin main
import pandas as pd

apple_df = pd.read_csv('AAPL.csv')
microsoft_df = pd.read_csv('MSFT.csv')


df_merge=pd.merge(apple_df,microsoft_df,how='inner',on='Date')
#x represents AAPL, y represents MSFT
df_merge['AAPL_return'] = df_merge['Adj Close_x'].pct_change() #Apple's percentage change (daily returns)
df_merge['MSFT_return'] = df_merge['Adj Close_y'].pct_change() #Microsoft's percentage change (daily returns)

df_merge[['AAPL_return','MSFT_return']].corr()

#252 is the amount of trading days in a year
#volatility growss with the square root of time

#correlation between Apple's and Microsoft's daily returns is roughly 0.56. This indicates positive somewhat strong correlation.
#A lower correlation is needed for managaing portfolio risk as stock with lower correlation 
#means you can diversify away non-systematic risk

df_merge[['AAPL_return','MSFT_return']].std() * (252**0.5)

#the standard deviation of annualized returns are low indiacting low volatility levels and low risk. 
#Apple's annualized returns has slightly higher volatility.

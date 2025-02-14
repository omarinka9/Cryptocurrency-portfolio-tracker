# Cryptocurrency-portfolio-tracker
Cryptocurrency portfolio tracker

import requests
import pandas as pd

def get_cryptocurrency_prices(currencies):
    url = 'https://api.coingecko.com/api/v3/simple/price'
    params = {'ids': ','.join(currencies), 'vs_currencies': 'usd'}
    response = requests.get(url, params=params)
    if response.status_code == 200:
        prices = response.json()
        return prices
    else:
        print(f'Ошибка при получении курсов валют: {response.status_code}')
        return {}

def calculate_portfolio_value(portfolio, prices):
    total_value = 0
    for currency, amount in portfolio.items():
        if currency in prices:
            total_value += amount * prices[currency]['usd']
    return total_value

if __name__ == '__main__':
    portfolio = {
        'bitcoin': 1.5,
        'ethereum': 3.2,
        'litecoin': 10
    }
    currencies = list(portfolio.keys())
    prices = get_cryptocurrency_prices(currencies)
    value = calculate_portfolio_value(portfolio, prices)
    print(f'Общая стоимость вашего портфеля: ${value:.2f}')
```

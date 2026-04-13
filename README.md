# Sales Forecasting Dashboard

## Overview
This project analyzes historical sales data and predicts future sales trends for the next 90 days using a simple moving average method.

## Features
- Historical sales visualization (line chart)
- 90-day sales forecast
- 30-day prediction table
- CSV export for predictions

## Tech Stack
- Python
- Pandas
- Matplotlib
- Google Colab

## How It Works
1. Load historical sales data (last 1 year)
2. Calculate average of last 30 days
3. Use that average to forecast next 90 days
4. Generate dashboard with visual and tabular output

## Code
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

dates = pd.date_range('2024-01-01', '2024-12-31')
sales = [1000 + (i*2) + (50 if d.dayofweek >= 5 else 0) for i, d in enumerate(dates)]

df = pd.DataFrame({'Date': dates, 'Sales': sales})

last_30_avg = df['Sales'].tail(30).mean()
future_dates = pd.date_range('2025-01-01', '2025-03-31')
forecast = [last_30_avg] * 90
forecast_df = pd.DataFrame({'Date': future_dates, 'Forecast': forecast})

plt.figure(figsize=(12, 5))
plt.plot(df['Date'], df['Sales'], label='Historical', color='blue')
plt.plot(forecast_df['Date'], forecast_df['Forecast'], label='Forecast', color='red', linestyle='--')
plt.title('Sales Forecast')
plt.xlabel('Date')
plt.ylabel('Sales ($)')
plt.legend()
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

print(forecast_df.head(30))

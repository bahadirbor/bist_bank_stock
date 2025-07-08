# BIST Bank Stocks Data Scraper

This Python project is a tool that scrapes stock data for banking sector companies listed on Borsa Istanbul (BIST) using Yahoo Finance API and stores them in a CSV file format.

## Features

- **Multi-Stock Support**: 9 different BIST banking companies
- **Automated Data Scraping**: Daily stock data via Yahoo Finance API
- **Data Consolidation**: Combine all stocks into a single DataFrame
- **Daily Return Calculation**: Automatic daily return percentage calculation
- **CSV Export**: Save data in CSV format

## Supported Stocks

| Symbol | Company Name |
|--------|-------------|
| AKBNK.IS | Akbank |
| ALBRK.IS | Albaraka Turk |
| GARAN.IS | Garanti BBVA |
| HALKB.IS | Halk Bankası |
| ISCTR.IS | İş Bankası |
| SKBNK.IS | Sekerbank |
| TSKB.IS | T.S.K.B |
| VAKBN.IS | Vakıfbank |
| YKBNK.IS | Yapı Kredi |

## Requirements

```bash
pip install -r requirements.txt
```

## Usage

### Basic Usage

```python
from multi_stock_dataframe import MultiStockDataFrame

# Initialize the class
multi_fetcher = MultiStockDataFrame()

# Define stock symbols
stock_symbols = ["AKBNK.IS", "GARAN.IS", "ISCTR.IS"]

# Fetch and combine data
combined_df = multi_fetcher.create_combined_dataframe(stock_symbols, period="1y")

# Save as CSV
multi_fetcher.save_to_csv(combined_df)
```

### Parameters

- **period**: Data fetching period
  - `"1d"`: 1 day
  - `"5d"`: 5 days
  - `"1mo"`: 1 month
  - `"3mo"`: 3 months
  - `"6mo"`: 6 months
  - `"1y"`: 1 year (default)
  - `"2y"`: 2 years
  - `"5y"`: 5 years
  - `"10y"`: 10 years
  - `"ytd"`: Year to date
  - `"max"`: Maximum available data

- **interval**: Data interval
  - `"1d"`: Daily (default)
  - `"1wk"`: Weekly
  - `"1mo"`: Monthly

## Data Structure

The generated DataFrame contains the following columns:

| Column | Description |
|--------|-------------|
| `date` | Trading date |
| `stock_name` | Company name |
| `open` | Opening price |
| `high` | Highest price |
| `low` | Lowest price |
| `close` | Closing price |
| `daily_return` | Daily return (%) |
| `adj_close` | Adjusted closing price |
| `volume` | Trading volume |

## Code Example

```python
def main():
    multi_fetcher = MultiStockDataFrame()
    
    # All bank stocks
    stock_symbols = [
        "AKBNK.IS", "ALBRK.IS", "GARAN.IS", "HALKB.IS", 
        "ISCTR.IS", "SKBNK.IS", "TSKB.IS", "VAKBN.IS", "YKBNK.IS"
    ]
    
    # Fetch last 1 year of data
    combined_df = multi_fetcher.create_combined_dataframe(stock_symbols, period="1y")
    
    if combined_df is not None:
        # Display first 10 rows
        print(combined_df.head(10))
        
        # Basic statistics
        print(combined_df.describe())
        
        # Save as CSV
        multi_fetcher.save_to_csv(combined_df)
        print("Data saved to 'all_datas.csv' file.")

if __name__ == "__main__":
    main()
```

## Output

When the program runs successfully:

1. Processing status for each stock is printed to console
2. `all_datas.csv` file is created
3. Data is saved with 3 decimal places precision

## License

This project is licensed under the Apache 2.0 License.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

# Cryptocurrency Price Tracking in SQL
## Description

⏲️ Previously I have tried to fetch real time data of Crypto prices into excel, this time I will fetch it to SQL Local Database. This project involved setting up a local instance of SQL on my desktop to serve as the data repository for my cryptocurrency price tracker. Real time data will be coming from the previously used CoinMarketCap API. I will be gathering price data for 5 coins. Bitcoin, Etherium, XRP, Cardano and Litecoin.

## Let's jump into action

### Step 1: Laying the Foundation with Local SQL Configuration
🖥️ Firstly I had to setup a local SQL instance to create a database for my project. I have:

1. Download the SQL Managmenet Studio and SQL Exrpesserver. 
2. Install both softwares on my desktop.
3. Create a new database named 'API_Crypto1' within SQL Server Express.
<img width="400" alt="image" src="https://github.com/sirmichal/Crypto_Prices_to_SQL/blob/main/SQL_Local_DB_Created.png?raw=true">
5. Assign myself appropriate permissions to access and modify the 'API_Crypto1' database.
<img width="400" alt="image" src="https://github.com/sirmichal/Crypto_Prices_to_SQL/blob/main/SQL_Table_Created.PNG?raw=true">
6. Create table 'CryptoPrices' and set schema.
<img width="400" alt="image" src="https://github.com/sirmichal/Crypto_Prices_to_SQL/blob/main/SQL_Table_schema.png?raw=true">
   
### Step 2: Orchestrating Cryptocurrency Price Data Acquisition

📓 To gather the latest cryptocurrency prices, I used CoinMarketCap API which I already had access to from the past project. I decided to write simple python script to call the API. Firstly, I had to install the Python library 'requests'. Below script is establishing a connection to the API and retrieving the JSON response.

```python
import requests
import json
from datetime import datetime

#Call API and provide parameters
url = 'https://pro-api.coinmarketcap.com/v2/cryptocurrency/quotes/latest'
parameters = {
  'id':'1,2,1027,52,2010',
  'convert':'USD'
}
headers = {
  'Accepts': 'application/json',
  'X-CMC_PRO_API_KEY': 'XXX',
}

response = requests.get(url, headers=headers, params=parameters)

print(response)
```
I got response 200 so the call to API is correct. 

### Step 3: Unraveling Price Data from JSON Response

ℹ️ I have set in the headers all of the paramteres necessary to get the data which I want. The JSON response contained relevant details, including the cryptocurrency name and price in USD. Additionally I wanted to have a timestamp for each of my entry so I have used a datetime library to get timestamp from my local desktop. I have added it to my script above.

```python
import requests
import json
from datetime import datetime

#Call API and provide parameters
url = 'https://pro-api.coinmarketcap.com/v2/cryptocurrency/quotes/latest'
parameters = {
  'id':'1,2,1027,52,2010',
  'convert':'USD'
}
headers = {
  'Accepts': 'application/json',
  'X-CMC_PRO_API_KEY': 'XXX',
}

response = requests.get(url, headers=headers, params=parameters)

coins = response.json()['data']
api_data = []

#Filter data
for y in parameters['id'].split(','):
    name = coins[y]['name']
    price = coins[y]['quote']['USD']['price']
    date = datetime.now().strftime('%Y-%m-%d %H:%M:%S')
    api_data.append((name,price,date))

print(api_data)
```

As a result I got the necessary info for my CryptoPrice Table in the SQL.

## Step 4: Establishing Connection to the SQL Database

🔌 To integrate the retrieved price data into the 'API_Crypto1' database, I utilized the Python library 'pyodbc'. This library established a connection to the SQL Server Express instance and enabled data exchange between the Python script and the database.

```python
import pyodbc

# SQL Server connection details
server = '(localdb)\API_Crypto'  # For a local SQL Server instance, you can use 'localhost' or '.' (period)
database = 'API_Crypto1'

# Database connection using Windows authentication
conn = pyodbc.connect(
    f'DRIVER={{ODBC Driver 17 for SQL Server}};'
    f'SERVER={server};'
    f'DATABASE={database};'
    'Trusted_Connection=yes'  # Use Windows authentication
)

# Create a cursor for database operations
cursor = conn.cursor()
```

### Step 5: Storing Price Data in SQL Database

🔢 To ensure the integrity and accessibility of the price data, I inserted the extracted data into a previously created table named 'CryptoPrices' within the 'API_Crypto1' database. Whenever the data is successfully insert into the table I got the message 'Data inserted successfully".

```python
import api_call
import pythontosqllocaldb


# Define an SQL insert statement with named parameters
sql_insert = """INSERT INTO CryptoPrices (Name, Price, Time)
                VALUES 
                    (?, ?, ?)"""

# Execute the insert statement with named parameters
for api_call.name, api_call.price, api_call.date in api_call.api_data:
    pythontosqllocaldb.cursor.execute(sql_insert, (api_call.name, api_call.price, api_call.date))

# Commit the transaction to save the changes
pythontosqllocaldb.conn.commit()

# Close the database connection
pythontosqllocaldb.conn.close()

print("Data inserted successfully.")
```

## Conclusions

👨‍🎓 To maintain the currency price data's freshness, Python script can be scheduled to run periodically, refreshing the 'API_Crypto1' database within given timeframe. Saved data can be used later to feed different analytics tools such as PowerBI or Tabelau.

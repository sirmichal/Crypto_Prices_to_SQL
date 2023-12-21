Cryptocurrency Price Tracking in SQL

As a business analyst with a burgeoning interest in data analysis, I'm always eager to explore new data sources and automate data-driven tasks. Recently, I embarked on a journey to track cryptocurrency prices and store them in a SQL database. This project involved setting up a local instance of SQL on my desktop to serve as the data repository for my cryptocurrency price tracker.

Step 1: Laying the Foundation with Local SQL Configuration

Install SQL Server Express software on your desktop.
Create a new database named 'API_Crypto1' within SQL Server Express.
Assign yourself appropriate permissions to access and modify the 'API_Crypto1' database.
Step 2: Orchestrating Cryptocurrency Price Data Acquisition

To gather the latest cryptocurrency prices, I employed the powerful CoinMarketCap API. The Python library 'requests' aided in establishing a connection to the API and retrieving the JSON response.

Step 3: Unraveling Price Data from JSON Response

The JSON response contained a wealth of information about the cryptocurrency prices. I extracted the relevant details, including the cryptocurrency name, price, and timestamp, using Python's 'json' library.

Step 4: Establishing Connection to the SQL Database

To seamlessly integrate the retrieved price data into the 'API_Crypto1' database, I utilized the Python library 'pyodbc'. This library established a connection to the SQL Server Express instance and enabled data exchange between the Python script and the database.

Step 5: Storing Price Data in SQL Database

To ensure the integrity and accessibility of the price data, I inserted the extracted data into a dedicated table named 'CryptoPrices' within the 'API_Crypto1' database.

Step 6: Automating Price Data Updating

To maintain the currency price data's freshness, I scheduled the Python script to run periodically, refreshing the 'API_Crypto1' database every minute. This ensured that the database always held the most up-to-date cryptocurrency prices.

This project not only equipped me with the latest cryptocurrency market insights but also honed my Python programming, API interaction, database integration, and SQL database operations skills. It served as a testament to my data analysis prowess and my ability to automate data gathering and processing tasks.

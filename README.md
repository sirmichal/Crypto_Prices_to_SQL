Cryptocurrency Price Tracking in SQL

Previously I have tried to fetch real time data of Crypto prices into excel, this time I will fetch it to SQL Local Database. This project involved setting up a local instance of SQL on my desktop to serve as the data repository for my cryptocurrency price tracker. Real time data will be coming from the previously used CoinMarketCap API. I will be gathering price data for 4 coins. Bitcoin, Etherium, XRP and Cardano.

Step 1: Laying the Foundation with Local SQL Configuration
Firstly I had to setup a local SQL instance to create a database for my project. I have:

1. Download the SQL Managmenet Studio and SQL Exrpesserver. 
2. Install both softwares on my desktop.
3. Create a new database named 'API_Crypto1' within SQL Server Express.
   <screen from cmd about sqllocaldb>
5. Assign yourself appropriate permissions to access and modify the 'API_Crypto1' database.
6. Create table 'CryptoPrices' and set schema.
   <screen from table schema>
   
Step 2: Orchestrating Cryptocurrency Price Data Acquisition

To gather the latest cryptocurrency prices, I used CoinMarketCap API which I already had access to from the past project. I decided to write simple python script to call the API. Firstly, I had to install the Python library 'requests'. Below script is establishing a connection to the API and retrieving the JSON response.

<code from the call api, remove the api key>

Step 3: Unraveling Price Data from JSON Response

I have set in the headers all of the paramteres necessary to get the data which I want. The JSON response contained relevant details, including the cryptocurrency name and price in USD. Additionally I wanted to have a timestamp for each of my entry so I have used a datetime library to get timestamp from my local desktop. 

<code snippet but only about the list creation>

Step 4: Establishing Connection to the SQL Database

To seamlessly integrate the retrieved price data into the 'API_Crypto1' database, I utilized the Python library 'pyodbc'. This library established a connection to the SQL Server Express instance and enabled data exchange between the Python script and the database.

Step 5: Storing Price Data in SQL Database

To ensure the integrity and accessibility of the price data, I inserted the extracted data into a dedicated table named 'CryptoPrices' within the 'API_Crypto1' database.

Step 6: Automating Price Data Updating

To maintain the currency price data's freshness, I scheduled the Python script to run periodically, refreshing the 'API_Crypto1' database every minute. This ensured that the database always held the most up-to-date cryptocurrency prices.

This project not only equipped me with the latest cryptocurrency market insights but also honed my Python programming, API interaction, database integration, and SQL database operations skills. It served as a testament to my data analysis prowess and my ability to automate data gathering and processing tasks.

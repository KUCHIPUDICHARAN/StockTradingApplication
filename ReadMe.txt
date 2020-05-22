Assumptions:

One of the first question raised to consulatant is do I need to connect to a live data source for live stock data updates 
and storing them in local database or storing sample data in local database and work on them? the answer is 
"Executing BUY/SELL and see the relevent price listeners are working as expected is the primary goal".

so based on that I have choosen to create a stock table which contains all the sample stock data I want to use for the application.
the IDEA in 3 simple steps below, 
1. create a sample stock for e.g. IBM, set price and volume as 50.00 & 1000 respectively.
2. add priceListener to stock table to listen for price updates on interested stocks and if it reaches the specified threshold execute BUY.
   Here the price update is done on the particular stock for e.g. IBM and
3. display the purchased/sold stock on the t_order table to see if the BUY/SELL instruction worked as expected.

To implement above steps, 

-> I have utilized REST Api to perform essential CRUD operations for stocks on stock table.
   the classes utilized are StockController, StockService and StockRepository 

-> I have utilized REST Api to perform essential CRUD operations for priceListeners on priceListener table.
   the classes utilized are PriceListenerController, PriceListenerService and PriceListenerRepository

-> I have utilized REST Api to perform essential CRUD operations for order on t_order table.
   the classes utilized are OrderController, OrderService and OrderRepository 

-> ExecutorService to perform BUY operations and PriceListenerEvent for onPostEvent

Tech stack used in the project:

Java, SpringBoot, Hibernate, Junit 5, Mockito, MariaDB.


URL's for POSTMAN or WebBrowser to evaluate the results: e.g. stock name = "IBM"

-> Create sample stock data on stock table: localhost:8080/addStock   --e.g.--> {"name":"IBM", "price":90.08, "volume":1000}
-> Check all stocks on stock table: localhost:8080/getAllStock
-> Add price listener for choosen stock : localhost:8080/addPriceListener --e.g.--> {"security": "IBM", "price": 89.00, "quantity": 100}
-> Update choosen stock on stock table: localhost:8080/updatePrice?name=charan&price=88.00
-> verify the t_order table for BUY instruction: localhost:8080/getAllOrders
-> verify the stock table to see stocks left after purchase: localhost:8080/getAllStock


Optional MariaDB Instructions:
once you have the MariaDB installed, The login details can be found in applciation.properties file but you can also find below.

database name : trading
username: root
password: smartboy009
server port: 8080

Summary:

'stock' table is created to add and update sample stocks to work on and is considered as "Stock Market" 

't_order' table is created for the sole purpose of displaying the executed BUY/SELL stocks only.

'price_listener' table is created to display the particular stocks we interested to BUY/SELL with the given
 threshold price and quantity(number of stocks) to be purchased.


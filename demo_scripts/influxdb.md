#
# Get into influxdb docker shell
```shell
docker exec -it influxdb-demo /bin/bash
```

# download the data file
```
```shell
curl https://raw.githubusercontent.com/PacktPublishing/Seven-NoSQL-Databases-in-a-Week/master/Chapter08/data/ticker_data.txt -o ticker_data.txt
```

# import the data
```
```shell
influx -import -path=ticker_data.txt -database=market -precision=s
# login to influx cli
influx

# check the data
```
```shell
show databses;
use market;
show measurements;
SELECT * from tickers limit 10;
```
# Queries
```shell
SELECT * FROM tickers WHERE ticker='JPM' AND high> low* 1.002 limit 5;
SELECT ticker::tag,company::field,volume::field,close::field FROM tickers limit 3;
SELECT *::field FROM tickers limit 3;
SELECT ticker, company, volume, close FROM market.autogen.tickers limit 3;
SELECT * FROM tickers WHERE ticker='AAPL' AND high> 174.6 limit 3;
select MAX(volume), MIN(volume), MEDIAN(volume) from tickers where time <= '2017-11-27T19:00:00.000000000Z' AND time >= '2017-11-27T10:00:00.000000000Z' group by ticker;
select MAX(volume), MIN(volume), MEDIAN(volume) from tickers where time <= '2017-11-27T19:00:00.000000000Z' AND time >= '2017-11-27T10:00:00.000000000Z' group by *;
select mean(volume) from tickers where time <= '2017-11-27T19:00:00.000000000Z' AND time >= '2017-11-27T10:00:00.000000000Z' group by time(60m), ticker;
SELECT MEAN(*) INTO market_watch.autogen.avgvol FROM /.*/ WHERE time >= '2017-11-27T00:00:00.000000000Z' AND time <= '2017-11-27T23:59:59.000000000Z' GROUP BY time(60m);
```
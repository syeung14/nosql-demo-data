```shell
#get all keys
keys *
keys product*
set name Peter
get name
del name
unlink name

expire name 10    #10 seconds
ttl name          #check expiration
```

```
# counter
set hits
incr hits
incrby hits 5
get hits
decrby hits 2
```

```shell
# Strings
SET ckey "Redis demo"
EXPIRE ckey 10
GET ckey
TTL ckey
GET ckey
```

```shell
# Lists
LPUSH books "NoSQL"
RPUSH books "Go Coding"
LPUSH books "Algorithm"
LLEN books
LINDEX books 1
```

```shell
# Hashes
HSET movie "title" "The Godfather"
HMSET movie "year" 1972 "rating" 9.2 "watchers" 10000000
HINCRBY movie "watchers" 3
HGET movie "title"
HMGET movie "title" "watchers"
HDEL movie "watchers"
HGETALL movie

```

```shell
# Set 
SADD user:max:favorite_artists "Arcade Fire" "Arctic Monkeys" "Belle & Sebastian" "Lenine"
SADD user:hugo:favorite_artists "Daft Punk" "The Kooks" "Arctic Monkeys"

SMEMBERS user:max:favorite_artists    #return all members in a set

SINTER user:max:favorite_artists user:hugo:favorite_artists
help SINTER

SDIFF user:max:favorite_artists user:hugo:favorite_artists
SDIFF user:hugo:favorite_artists user:max:favorite_artists
SUNION user:max:favorite_artists user:hugo:favorite_artists

SRANDMEMBER user:max:favorite_artists

SISMEMBER user:max:favorite_artists "Arctic Monkeys" #whether a member exists
SREM user:max:favorite_artists "Arctic Monkeys"
```

```shell
# Sorted Set
MULTI
HMSET product:10200 name ZXYW desc “Description for ZXYW” price 300
ZADD product_list 10200 product:10200
ZADD product_price 300 product:10200
EXEC

# query by product id
hgetall product:10200

# query by price
ZRANGEBYSCORE product_price 0 300 
```
#MongoDB Notes

##### Table of Contents
[Infos](#infos)  
[Import](#import)  
[Ruby](#ruby)  
[Connection](#connection)  
[Mongo](#mongo)  
[Rails Install](#rails)  
[rails console](#railsc)  
[SQL to Mongo](#sqlmongo)  


<a name="infos"/>
## Infos and useful stuff

[Official documentation](https://docs.mongodb.com/manual/introduction/)

BSON => Binary JSON
Binary Serialization format used to Store Documents and make remote procedure calls in MongoDB
[BSON types](https://docs.mongodb.com/manual/reference/bson-types/)

<a name="import"/>

## start server 

# Data Importing
```bash
mongoimport --db test --collection zips --drop --file zips.json 
```

<a name="ruby"/>

## Install

```ruby
gem update --system
gem install mongo
gem install bson_ext
```

<a name="connection"/>

```ruby
#disable logging
require 'mongo'
Mongo::Logger.logger.level = ::Logger::INFO

#get a connection
db = Mongo::Client.new('mongodb://localhost:27017')

#use test
db = db.use('test')

#database name
db.database.name

# List collections
db.database.collections #  OR
db.database.collection_names

# Find first
db[:zips].find.first 
```

<a name="mongo"/>

## Use Mongo cli

```bash
mongo

use test

db.zips.findOne()

```

<a name="rails"/>

## Rails installation

See the code [here](https://github.com/nicolasboulet/fullstack-course3-module1-zips)

### Gemfile
gem 'mongoid'

### Create config/mongoid.yml

```bash
rails g mongoid:config
```
### Bootstrap mongoid with the application config/application.rb

See conf [here](https://github.com/nicolasboulet/fullstack-course3-module1-zips/blob/master/config/application.rb)

```ruby
Mongoid.load!('./config/mongoid.yml')
```

<a name="railsc"/>

# Rails c

```ruby
mongo_client = Mongoid::Clients.default # Mongo Client object
mongo_client.database.name
collection = mongo_client[:zips]
collection.count

```

<a name="sqlmongo"/>

# SQL To Mongo

https://docs.mongodb.com/manual/reference/sql-comparison/

SQL | Mongo
--- | ---
WHERE | $match
GROUP BY | $group
SELECT | $project
ORDER BY | $sort
LIMIT | $limit
SUM | $sum
COUNT | $count

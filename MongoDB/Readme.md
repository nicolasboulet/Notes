#MongoDB Notes

##### Table of Contents
[Import](#import)  
[Ruby](#ruby)  
[Connection](#connection)  


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



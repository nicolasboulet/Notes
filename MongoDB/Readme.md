#MongoDB Notes

##### Table of Contents
[Import](#import)  
[Ruby](#ruby)  
[Connection](#connection)  
[Mongo](#mongo)  
[Rails]#(#rails)


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

## Rails

See the code [here](https://github.com/nicolasboulet/fullstack-course3-module1-zips)

### Gemfile
gem 'mongoid'

### Create mongoid.yml

```bash
rails g mongoid:config
```
### Bootstrap mongoid with the application

See conf [here](https://github.com/nicolasboulet/fullstack-course3-module1-zips/blob/master/config/application.rb)

```ruby
Mongoid.load!('./config/mongoid.yml')
```

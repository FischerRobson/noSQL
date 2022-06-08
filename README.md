# noSQL

### Properties:

* SCHEMALESS
* Document, Key-value, Graph types
* no conventions
* dont have joins
* less security
* faster
* horizontal growth
* dinamic systems

### Objects:

* Collections
* Documents
* Nodes
* Key
* Value
* Labels
* Properties

# MongoDB

### Architecture

DB -> Collections -> Documents

![mongo_architecture](https://media.geeksforgeeks.org/wp-content/uploads/20200127193216/mongodb-nosql-working.jpg)

Stores data in JSON.


## MongoDB install

[Tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-20-04-pt#passo-2-iniciando-o-servico-do-mongodb-e-testando-o-banco-de-dados)

#### start mongodb service
```sh
sudo systemctl start mongod
```

#### check status mongodb service
```sh
sudo systemctl status mongod
```

#### stopmongodb service
```sh
sudo systemctl stop mongod
```

#### enter on mongo CLI
```sh
mongo
```

### Utils

[Mockaroo](https://www.mockaroo.com/) -> Generate custom JSON data 
[Anaconda install](https://www.digitalocean.com/community/tutorials/how-to-install-the-anaconda-python-distribution-on-ubuntu-20-04-pt) -> manage data with python

### Graphic interface

* RoboMongo (for devs)
* MongoCompass (for DBA)
* Mongochef (payed)

### Managing 

#### List databases

```sh
show dbs
```

#### Get database name

```sh
db.getName()
```

#### Create database

```sh
use [db_name]

use flyes
```

#### Insert one

```sh
db.[collection_name].insertOne([data])

db.flyes.insertOne(
  {
    airportOrigin: "GRU",
    airportDestiny: "MIA",
    airplane: "Airbus A380",
    distance: 6500,
    international: true
  }
)
```

#### Using custom ID

```sh
db.flyes.insertOne(
  {
    airportOrigin: "GRU",
    airportDestiny: "MIA",
    airplane: "Airbus A380",
    distance: 6500,
    international: true,
    _id: 1 // isn't auto increment
  }
)
```

#### Insert many

```sh
db.[collection_name].insertMany([data, data, data])

db.flyes.insertMany([
  {
    airportOrigin: "GRU",
    airportDestiny: "MIA",
    airplane: "Airbus A380",
    distance: 6500,
    international: true
  },
  {
    airportOrigin: "GRU",
    airportDestiny: "SDU",
    airplane: "Boeing 737",
    distance: 450,
    international: false
  }
])
```

#### Select data

Brings the last data
```sh
db.[collection_name].findOne()

db.flyes.findOne()
```

Brings all data
```sh
db.[collection_name].find()

db.[collection_name].find().pretty() //for better view

db.flyes.find().pretty()
```

#### Delete data

Delete one data
```sh
db.[collection_name].deleteOne({ [key]: [value] })

db.[collection_name].deleteOne({}) //delete the last inserted data

db.flyes.deleteOne({ _id: 1 }) // delete the fly with id 1
```

Delete more than one data
```sh
db.[collection_name].deleteMany({ [key]: [value] })

db.flyes.deleteMany({ international: true }) //delete all international flyes 
```

Delete all data
```sh
db.[collection_name].deleteMany({})

db.flyes.deleteMany({}) //delete all flyes 
```

### Update data

| Operator | Effect                               |
| -------- | ------------------------------------ |
| $set     | appends new key, or update if exists |
| $unset   | remove the key from document         | 

Update one data
```sh
db.[collection_name].updateOne({ [key]: [value] }, {$set:{[key]: [new_value]}}) // (filter, new_data)

db.flyes.updateOne({ _id: 1 }, {$set:{late: true}}) // update the fly with id 1, appending new key late

db.flyes.updateOne({_id: 1}, {$unset:{late: ''}}) //remove key late from fly with id 1
```

Update more than one data
```sh
db.[collection_name].updateMany({}, {$set:{[key]: [new_value]}}) // (filter, new_data)

db.flyes.updateMany({}, {$set:{late: false}}) // update all flyes appending key late (or updating if exists)
```

#### Import data

Without array

```sh
mongoimport --stopError --db [db_name] --collection [collection_name] < [file_path]
```

With array

```sh
mongoimport --stopError --db [db_name] --collection [collection_name] < [file_path] --jsonArray
```

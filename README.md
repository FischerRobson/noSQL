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
```

```json
[
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
]
```

```sh
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

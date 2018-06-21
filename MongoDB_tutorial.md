MongoDB tutorial

|desc  | usage|
|------|------|
|create database |use DATABASE_NAME|
| check currently selected database| db|
| check  databases list   |  show dbs |
| insert document   | db.colName.insert({...})   |
|drop a existing database   | db.dropDatabase()  |
|create collection   | db.createCollection(name, options)  |
|check the created collection   | show collections  |
|drop a collection   | db.COLLECTION_NAME.drop()  |
| insert data  | db.COLLECTION_NAME.insert(document)  |
|  query data  | db.COLLECTION_NAME.find()  |
|display the results in a formatted way   | db.mycol.find().pretty()  |
| updates the values in the existing document   | db.COLLECTION_NAME.update(SELECTION_CRITERIA, UPDATED_DATA)  |
|  replaces the existing document with the new document passed  |db.COLLECTION_NAME.save({_id:ObjectId(),NEW_DATA})   |
|remove a document from the collection   | db.COLLECTION_NAME.remove(DELLETION_CRITTERIA)  |
| limit the records in MongoDB   | db.COLLECTION_NAME.find().limit(NUMBER)  |
|skip the number of documents   |  db.COLLECTION_NAME.find().limit(NUMBER).skip(NUMBER) |
|sort documents in MongoDB   |  db.COLLECTION_NAME.find().sort({KEY:1/-1}) |
|create an index   | db.COLLECTION_NAME.ensureIndex({KEY:1/-1})  |
|the aggregation in MongoDB   |  db.COLLECTION_NAME.aggregate(AGGREGATE_OPERATION) |
|create backup of database   |  mongodump |
|restore backup data   | mongorestore  |
| checks the status of all running mongod instances   | mongostat (run in cmd)  |
|tracks and reports the read and write activity of MongoDB instance   | mongotop [N] (run in cmd)  |


RDBMS Where Clause Equivalents in MongoDB

Replica Set
 * Set Up a Replica Set
    mongod --port "PORT" --dbpath "YOUR_DB_DATA_PATH" --replSet "REPLICA_SET_INSTANCE_NAME"
 * Add Members to Replica Set
    rs.add(HOST_NAME:PORT)

Sharding is the process of storing data records across multiple machines

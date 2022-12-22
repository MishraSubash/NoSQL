### Some common basic MongoDB Queries 

### Start MongoDB Server
`start_mongo`

### Check Version of MongoDB
`db.version()`

### List Databases
`show dbs`

### Create or use database 
`use db_name`

### Create collection (collection is a table in SQL)
`db.createCollection("collection_name")`

### List collections
`show collections`

## Insert documents into a collection 
### Insert one document
`db.collection_name.insert({"attribute1" : "value_one", "attribute2", "vakue_two"})`

### Insert multiple documents at once

`db.collection_name.insertMany([
   {
      "attribute1": "Eiffel Tower",
      "attribute2": "Paris",
      "attribute3": "France"

    },
    {
        "attribute1": "Statue of Liberty",
        "attribute2": "New York",
        "attribute3": "USA"
    },
    {
        "attribute1": "Dharahara",
        "attribute2": "Kathmandu",
        "attribute3": "Nepal"
    },
    {
        "attribute1": "CN Tower",
        "attribute2": "Toronto",
        "attribute3": "Canada"
    }
])`

### Count the number of documents in a collection 
`db.collection_name.count()`

### List all documents in a collection
`db.collection_name.find()`

### List the first document in the collection
`db.collection_name.findOne()`

### List all documents in the collection
`db.collection_name.find()`

### List first N documents in the documents
`db.collection_name.find().limit(N)`

### Filter data by column attribute
`db.collection_name.find("attribute_name": "value key")`

### Lists all documents with only certain field in the output
`db.collection_name.find({}, {"attribute_name" :1})`

### Lists all document without a specified attribute/field
`db.collection_name.find({}, {"attribute_name" :0})`

### Lists documents that match certain filter with only specific attribute/field 
`db.collection_name.find({"attribute_name": "fileter_value"}, {"attribute_name": 1})`

## Update documents based on a criteria. 
### Add a field to all the documents

`db.collection_name.updateMany({What documents to field}, {$set:{what fields to set}})`

### Example where collection_name is "languages"
`db.languages.updateMany({}, {$set:{"description":"programming language"}})`

### Set the create for all documents for python languages 
`db.languages.updateMany({"name":"python"}, {$set:{"creator":"Guido van Rossum"}})`

### Delete documents based on criteria
`db.collaction_name.remove({"attribute_name": "delete_by_value"})`

### Delete all the documents in a collection
`db.collection_name.remove({})`

### Insert large random dataset into a collection
`for (i=1; i<20000; i++){print(i); db.bigdata.insert({"account_no":i, "balance":Math.round(Math.random()*1000000)})}`

### Find out query run time in milliseconds
`db.bigdata.find({"account_no": 589545}).explain("executionStats").executionStats.executionTimeMillis`

### Create index on certain field 
`db.collection_name.createIndex({"field_name":1})`

### Get a list indexes from collection
`db.collection_name.getIndexes()`

### delete an index
`db.collection_name.dropIndex({"index_field_name":1})`


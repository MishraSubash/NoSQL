# Collection of common IBM Cloudant NoSQL querris. 

## Retrive Data 
### Retrive all data from the table. Equivalent to [SELECT * FROM TABLE] in SQL
`{
   "selector": {}
}`

### Retriving only certain data
#### e.g: Select all fields in all documents with _id greater than 4

`{
   "selector": {
      "_id": {
         "$gt": "4"
      }
   }
}`

#### Select all fields in all documents with _id less than 4
`{
   "selector": {
      "_id": {
         "$lt": "4"
      }
   }
}`

#### Select only certain columns from the table 
`{
    "selector": {},
    "fields": [
       "Column_one",
       "Column_two",
       "Columns_three"
    ]
 }`

#### Select only certain fields  in documents with _id less than 4
{
    "selector": {
    "_id": {
          "$lt": "4"
       }
    },
    "fields": [
        "Column_one",
        "Column_two",
        "Columns_three"
     ]
  }`

#### Select specific fields in documents with _id greater than 2 and sort by _id ascending 
 `{
    "selector": {
       "_id": {
          "$gt": "2"
       }
    },
    "fields": [
        "Column_one",
        "Column_two",
        "Columns_three"
    ],
    "sort": [
       {
          "_id": "asc"
       }
    ]
 }`


## ALTER table can be performed in the interface itself. No query required

## Creating Indexes on Cloudant using HTTP API and curl
#### This command creates a json index on the field "firstname", on the employees database
`curl -X POST $SERVERURL/employees/_index \
-H"Content-Type: application/json" \
-d'{
    "index": {
        "fields": ["firstname"]
    }
}'`

## This command creates a json index on the field "firstname", and names the index as firstname-index.
#### You can mention JSON index explicitly. The default is JSON index

`curl -X POST $SERVERURL/employees/_index \
-H"Content-Type: application/json" \
-d'{
    "index": {
        "fields": ["firstname"]
    },
    "name" : "firstname-index",
    "type" : "json"
}'`

#### This command creates a text index on the employees database.
`curl -X POST $SERVERURL/employees/_index \
-H"Content-Type: application/json" \
-d'{ "index": {},
     "type": "text"
}'`



####Create a database 
`curl -X PUT $CLOUDANTURL/DB_name`
    * A response of {"ok":true} indicates that the database is successfully created*

#### Verify by listing all databases.
`curl $CLOUDANTURL/_all_dbs`

####  Drop a database
`curl -X DELETE $CLOUDANTURL/DB_name`

#### Verify that the database is deleted by listing all databases.
`curl $CLOUDANTURL/_all_dbs`

### Insert a document
#### eg: Run the below command to insert a document in the planets database with _id of "1".
`curl -X PUT $CLOUDANTURL/planets/"1" -d '{ 
    "name" : "Mercury" ,
    "position_from_sum" :1 
     }'`

####  Verify by listing the document with the _id "1".
`curl -X GET $CLOUDANTURL/planets/1`

### Update a document
#### To update a document you need its revision id.
#### Replace the "_rev" below with the one you noted from INSERT step.

`curl -X PUT $CLOUDANTURL/planets/1 -d '{ 
    "name" : "Mercury" ,
    "position_from_sum" :1,
    "revolution_time":"88 days",
    "_rev":"1-3fb3ccfe80573e1ae334f0cfa7304f6c"
    }'`


#### Command to update the document in the planets database with _id of "1".    
`curl -X PUT $CLOUDANTURL/planets/1 -d '{
    "name": "Mercury",
    "position_from_sum": 1,
    "revolution_time": "88 days",
    "rotation_time": "59 days",
    "_rev": "1-3fb3ccfe80573e1ae334f0cfa7304f6c"
}'`


###  Delete a document
#### To delete a document you need its revision id.
#### REPLACE the value of "_rev" with what you have noted earlier and run the command.

`curl -X DELETE $CLOUDANTURL/planets/1?rev=2-de9fdd2d971e377c5db2d6425cb38ff1`


### Querying the Database using curl 
#### for example: Select data with _id 1
`curl -X POST $CLOUDANTURL/diamonds/_find \
-H"Content-Type: application/json" \
-d'{ 
    "selector":
        {
            "_id":"1"
        }
    }'`

### Query with filter argument    
###  for eg: Query  table with price more than 345   

`curl -X POST $CLOUDANTURL/table_name/_find \
-H"Content-Type: application/json" \
-d'{ "selector":
        {
            "price":
                {
                    "$gt":345
                }
        }
    }'`






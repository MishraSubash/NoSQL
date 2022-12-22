### Collection of common Cassandra database tips and querries

## Important Tips

#### Cassandra is a good fit for append-like type of data.
#### MongoDB usually covers search-related use cases, and Cassandra focuses on "always available" services.
#### At the node level, writes are performed in memory so there is no read before write.
####  Cassandra sacrifices availability to guarantee consistency. If one of the replicas is down or unreachable, the write operation will fail since Cassandra cannot meet the required consistency level
#### Tables are logical entities that organize data storage at cluster and node level (according to a declared schema), and keyspaces are logical entities that each contain one or more tables.
### Guidelines to follow for data modeling
    * Choose a partition key that starts answering your query but that also spreads the data uniformly around the cluster 
    * Build a primary key that allows you to minimize the number of partitions read in order to answer a certain query
    * Build a clustering key that helps you reduce the amount of data that needs to be read by ordering your clustering key columns according to your query

#### Cassandra supports built-in, collection, and user-defined data types 
#### Both collection and user-defined data types offer a way to group and store data together 
#### Collection data types can emulate one-to-many relationships 
#### There are three types of collection data types: lists, maps, and sets 
#### User-defined data types can emulate one-to-one relationships
#### User-defined data types can attach multiple data fields to a column
#### A keyspace needs to be defined before creating tables, as there is no default keyspace. 
#### A keyspace can contain any number of tables, and a table belongs to only one keyspace. 
#### Replication is specified at the keyspace level. 
#### You specify the replication factor during the creation of a keyspace, but the replication factor can be modified later



## find host details
`show host`

## Find the version of the server
`show version`

## Key Space Operations

## Create KEYSPACE 
#### This is an example. Creating a keyspace names "Training" using 
#### using SimpleStrategy and Replication factor of 3 
`CREATE KEYSPACE training
WITH replication = {'class': 'SimpleStrategy', 'replication_factor:3'};`

### List keyspaces
`describe keyspaces`

### Alter a Keyspace
#### This is an example

`ALTER KEYSPACE training
WITH replication = {'class': 'NetworkTopologyStrategy'};`

### Use a keyspace
`use keyspace_name;`

### List all tables in the keyspace
`describe tables`


### Drop a keyspace
`drop keyspace keyspace_name;`

### Verify the changes using the describe command.
`use system;`
`describe keyspaces`


### Table Operations
#### Data in Cassandra is organized logically in tables.
#### A table’s metadata specifies the primary key – instructing Cassandra how to distribute the table data at the cluster level and at node level 
#### You can add the Time-To-Live parameter at the table level – meaning that you can expire (or delete) all data that has surpassed the TTL 
#### You can modify the columns and column names but only for regular columns 
#### A Primary Key, once defined at table creation, cannot be modified

### Create a table. Make sure you create KEYSPACE first
#### example table creation 

`CREATE TABLE movies(
movie_id int PRIMARY KEY,
movie_name text,
year_of_release int
);`

### Describe a table 
`describe table_name (eg. movies)`

### Insert data into tables 
`INSERT INTO table_name(
    column_name, column_name2, ..)
    VALUES(value1, value2,...;)`

### Update Table
`UPDATE table_nameSET column_name = 'value_to_update'
WHERE column_name = 'Column_ID'`

### Delete Record
`DELETE from table_name
WHERE column_name = "Column_value"`

### Alter table. adding new attribute/column into the table
`ALTER TABLE table_name
ADD new_column_name column_data_type;`

### Drop a table 
`drop table table_name;`

### clear screen 
`cls`

### Disconnect cassandra server
`exit`


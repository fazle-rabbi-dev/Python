<h1 align="center">Pymongo</h1>

* `Pymongo is a MongoDB driver`


* ### Add The Bellow Code In The Top
	```py
	import dns.resolver
	dns.resolver.default_resolver=dns.resolver.Resolver(configure=False)
	dns.resolver.default_resolver.nameservers=['8.8.8.8']
	```

### Create Database

```py
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")

mydb = myclient["mydatabase"]
```


### Check Check if Database Exists
```py
dblist = myclient.list_database_names()
if "mydatabase" in dblist:
  print("The database exists.")
```

### Creating a Collection
```py
import pymongo

myclient = pymongo.MongoClient("mongodb://localhost:27017/")
mydb = myclient["mydatabase"]

mycol = mydb["customers"]
```

### Check if Collection Exists
```py
print(mydb.list_collection_names())

# check a specific collection by name:
collist = mydb.list_collection_names()
if "customers" in collist:
  print("The collection exists.")
```

### Insert Document Into Collection
```py
# Insert Single Document
mycol = mydb["customers"]

mydict = { "name": "John", "address": "Highway 37" }

x = mycol.insert_one(mydict)
print(x.inserted_id)

# Insert Multiple Documents
mycol = mydb["customers"]

mylist = [
  { "name": "Amy", "address": "Apple st 652"},
  { "name": "Hannah", "address": "Mountain 21"},
  { "name": "William", "address": "Central st 954"},
  { "name": "Chuck", "address": "Main Road 989"},
  { "name": "Viola", "address": "Sideway 1633"}
]

x = mycol.insert_many(mylist)

#print list of the _id values of the inserted documents:
print(x.inserted_ids)
```

### Find Documents
```py
# find single document
mycol = mydb["customers"]
x = mycol.find_one({"_id":"92kskskjsx"})
print(x)

# find multiple document
mycol = mydb["customers"]
x = mycol.find()
print(x)

# Return Only Some Fields
mycol = mydb["customers"]
for x in mycol.find({},{ "_id": 0, "name": 1, "address": 1 }):
  print(x)
  
  
# Find Document Bt Id
from bson import *
id = "5fec2c0b348df9f22156cc07"

objInstance = ObjectId(id)
 

collection.find_one({"_id": objInstance})
 
# below line works same as the above

collection.find_one({"_id": ObjectId(id)})

collection.find_one(ObjectId(id))
```

### Sort the Result
```py
mycol = mydb["customers"]
mydoc = mycol.find().sort("name",1) # --> -1 for descending
for x in mydoc:
  print(x)
```

### Delete Document
```py
# Delete one
mycol = mydb["customers"]
myquery = { "address": "Mountain 21" }
mycol.delete_one(myquery)

# Delete many
mycol = mydb["customers"]
myquery = { "address": {"$regex": "^S"} }
x = mycol.delete_many(myquery)
print(x.deleted_count, " documents deleted.")
```

### Delete All Documents in a Collection
```py
mycol = mydb["customers"]
x = mycol.delete_many({})
print(x.deleted_count, " documents deleted.")
```

### Delete Collection
```py
mycol = mydb["customers"]
mycol.drop()
```

### Update Collection
```py
# Update one
mycol = mydb["customers"]

myquery = { "address": "Valley 345" }
newvalues = { "$set": { "address": "Canyon 123" } }

mycol.update_one(myquery, newvalues)

#print "customers" after the update:
for x in mycol.find():
  print(x)
  
  
# Update many
mycol = mydb["customers"]

myquery = { "address": { "$regex": "^S" } }
newvalues = { "$set": { "name": "Minnie" } }

x = mycol.update_many(myquery, newvalues)

print(x.modified_count, "documents updated.")
```

### Limit
```py
mycol = mydb["customers"]

myresult = mycol.find().limit(5)

#print the result:
for x in myresult:
  print(x)
```

##
```shell
$ mongo
$ db.test.insert({"company": "O'Reilly Media", "technology": "MongoDB"})
$ db.test.find()
$ db.test.find().pretty()

$ show collections

# current database
$ show dbs
$ use demo
$ db 
$ db.help()

# Creating Documents
# insertMany
# insertOne
$ db.inventory.insertOne( { item: "canvas", 
                            qty: 100, tags: ["cotton"], 
                            size: { h: 28, w: 35.5, uom: "cm" } 
                          })
$ db.inventory.find()
$ db.inventory.find()
$ db.inventory.findOne()
#
# A board game with a stock of 75 and the tag "games"
# An unique painting of dimensions 75 cm by 125 cm and the tag "oil painting"
$ db.inventory.insertMany([
    { item: "board game", qty: 75, tags: ["games"]},
    { item: "painting", qty: 1, tags: ["oil"], size: { h: 75, w: 125, uom: "cm" }}
])

# Finding Document
# SELECT * FROM inventory WHERE item = "board game"
$ db.inventory.find({item: "board game"})
$ db.inventory.find({tags: {$exists: true }} )
$ db.inventory.find( { tags: {$exists: true }, qty: { $gt : 50} })

# Exists
$ db.inventory.find({tags: {$exists: true }} )
# Equals
$ db.inventory.find( { qty: { $eq: 25 } } )
# Not Equals
$ db.inventory.find({ qty: { $ne: 25 } })
# Not In
$ db.inventory.find( { qty: { $nin: [ 100, 25 ] } } )
# In
$ db.inventory.find( { qty: { $in: [ 100, 25 ] } } )

# nested Object
$ db.example.insertMany([
     {grades: [1,2,3]},
     {grades: [4,5,6]}
 ])

# Do not have an "oil" or "games" tag
# Have a size unit of measure (uom) of "cm"
# Contain only the item field and not the others
$ db.inventory.find({
    "tags": { $ne: [ "oil", "games" ] },
    "size.uom" : "cm"
 }, {
    "_id": 0, 
    "item":1
 })

# Updating Documents
# updateOne
# updateMany
# replaceOne
$ db.inventory.updateMany(
    { "qty": { $lt: 50 } },
    {
        $set: { "size.uom": "in", status: "P" },
        $currentDate: { lastModified: true }
    },
    {upsert: true}
)
$ db.inventory.find({ "qty": { $lt: 50 } })
$ db.inventory.replaceOne(
   { item: "board game" },
   { item: "paper", instock: [ { warehouse: "A", qty: 60 }, { warehouse: "B", qty: 40 } ] } )

# Find all the elements without tags
# Also set the tags field as an empty array
# Also add another field into them to mark them as {"noTags" : True}
$ db.inventory.updateMany(
    { "tags": { $exists: false } },
    {
    $set: {
        "tags" : [],
        "noTags" : true
    }
})

# Deleting 
$ db.inventory.deleteMany( { qty: {$lt: 120} } )

```

### import
docker exec -i mongo-demo sh -c 'mongoimport -d demo -c rent --type csv --headerline --drop' < newyork-rent.csv

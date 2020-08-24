# MongoDB Cheat Sheet

## [MongoDB vs SQL](https://docs.mongodb.com/manual/reference/sql-comparison/)


### Start Local MongoDb Server

```
mongod
```

### Start using mongo db in command line

```
mongo
```

### Look for help

```
help
```

### help on db methods

```
db.help()                    
                
```

###  help on collection methods

```
db.mycoll.help()  
```

### set default number of items to display on shell

```
DBQuery.shellBatchSize = x   
```

* * *
* * *


### Show All Databases

```
show dbs
```

### Show Current Database

```
db
```

### Create Or Switch Database

```
use <dbname>
use acme
```

- unless you create a collection mongo wont show database

### Drop

```
db.dropDatabase()
```

### Create Collection

```
db.createCollection(<collection_name>)
db.createCollection('posts')
db.createCollection('multidocs')
```

### Show Collections

```
show collections
```

* * *
* * *

### Insert Row

```
db.posts.insert({
  title: 'Post One',
  body: 'Body of post one',
  category: 'News',
  tags: ['news', 'events'],
  user: {
    name: 'John Doe',
    status: 'author'
  },
  date: Date()
})
```

### Insert Multiple Rows

```
db.posts.insertMany([
  {
    title: 'Post Two',
    body: 'Body of post two',
    category: 'Technology',
    date: Date()
  },
  {
    title: 'Post Three',
    body: 'Body of post three',
    category: 'News',
    date: Date()
  },
  {
    title: 'Post Four',
    body: 'Body of post three',
    category: 'Entertainment',
    date: Date()
  }
])
```
### can insert in any form example

- array of objects
```
db.multidocs.insert({
    title: "Multiple Docs",
    multipleDocs :[{
        title: 'Multiple Docs 1',
        body: 'Body of post two',
        category: 'Hate Java',
        date: Date()
    },
    {
        title: 'Multiple Docs 2',
        body: 'Body of post three',
        category: 'Programming',
        date: Date()
    },
    {
        title: 'Multiple Docs 3',
        body: 'Body of post three',
        category: 'Coding',
        date: Date()
    }],
    Workdone:"YES"
})
```

- object of object
```
db.multidocs.insert({
    title: "Multiple Docs",
    multipleDocs :{
        title: 'Multiple Docs 1',
        body: 'Body of post two',
        category: 'Hate Java',
        date: Date()
    },
    Workdone:"YES"
})
```

- object of objects
```
db.multidocs.insert({
    title: "Multiple Docs",
    multipleDocs :{
        testdoc:{
            title: 'Multiple Docs 1',
            body: 'Body of post two',
            category: 'Hate Java',
            date: Date()
        },
        testdoc1:{
            title: 'Multiple Docs 1',
            body: 'Body of post two',
            category: 'Hate Java',
            date: Date()
        },
        testdoc1:{
            title: 'Multiple Docs 1',
            body: 'Body of post two',
            category: 'Hate Java',
            date: Date()
        }
    },

    Workdone:"YES"
})
```

### Get All Rows

```
db.posts.find()
```

### Get All Rows Formatted

```
db.posts.find().pretty()
```

### Find Rows

```
db.posts.find({ category: 'News' }).pretty()
```

### Sort Rows

#### asc
```
db.posts.find().sort({ title: 1 }).pretty()
```
#### desc
```
db.posts.find().sort({ title: -1 }).pretty()
```

### Count Rows

```
db.posts.find().count()


db.posts.find({ category: 'News' }).count()
```

### Limit Rows

```
db.posts.find().limit(2).pretty()
```

### Chaining

- sequence of chaining is immaterial
```
db.posts.find().limit(2).sort({ title: 1 }).pretty()

db.posts.find().sort({ title: 1 }).limit(2).pretty()

db.posts.find().pretty().sort({ title: 1 }).limit(2)
```

### Foreach

```
db.posts.find().forEach(function(doc) {
  print("Blog Post: " + doc.title)
})
```

### Find One Row

```
db.posts.findOne({ category: 'News' })
```

### Find Specific Fields

```
db.posts.find({ title: 'Post One' }, {
  title: 1,
  author: 1
})

db.posts.find({}, {
  title: 1,
}).pretty()

db.posts.find({}, {
   body: 1
}).pretty()
```

### Update Row

```
db.posts.update({ title: 'Post Two' },
{
  title: 'Post Two',
  body: 'New body for post 2',
  date: Date()
},
{
  upsert: true
})
```

### Update Specific Field

```
db.posts.update({ title: 'Post Two' },
{
  $set: {
    body: 'Body for post 2',
    category: 'Technology'
  }
})
```

### Increment Field (\$inc)

```
db.posts.update({ title: 'Post Two' },
{
  $inc: {
    likes: 5
  }
})
```

### Rename Field

```
db.posts.update({ title: 'Post Two' },
{
  $rename: {
    likes: 'views'
  }
})
```

### Delete Row

```
db.posts.remove({ title: 'Post Four' })
```

### Sub-Documents

```
db.posts.update({ title: 'Post One' },
{
  $set: {
    comments: [
      {
        body: 'Comment One',
        user: 'Mary Williams',
        date: Date()
      },
      {
        body: 'Comment Two',
        user: 'Harry White',
        date: Date()
      }
    ]
  }
})
```

### Find By Element in Array (\$elemMatch)

```
db.posts.find({
  comments: {
     $elemMatch: {
       user: 'Mary Williams'
       }
    }
  }
)
```

### Add Index

- adding index of title

```
db.posts.createIndex({ title: 'text' })
```

### Text Search

```
db.posts.find({
  $text: {
    $search: "\"Post O\""
    }
}).pretty()
```

### Greater & Less Than

```
db.posts.find({ views: { $gt: 2 } })
db.posts.find({ views: { $gte: 7 } })
db.posts.find({ views: { $lt: 7 } })
db.posts.find({ views: { $lte: 7 } })
```

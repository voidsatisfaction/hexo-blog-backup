---
layout: post
title: AWS DynamoDB 정리 2부 테이블 만들기, 정보보기, 데이터 읽기(secondary index), 데이터 수정하기, 삭제하기
categories:
  - Database
tags:
  - Database
  - Dynamodb
---

## 참조

- [Performing Conditional Writes with Condition Expressions - AWS](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Expressions.SpecifyingConditions.html)
- [Improving Data Access with Secondary Indexes in DynamoDB](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SecondaryIndexes.html)

## 핵심

## 기본 내용

### Query and Scan the Table

**Step 5.1: Run a Query**

This section provides examples of Query operations. The queries are specified against the Music table. Remember, the table primary key is made of Artist (partition key) and SongTitle (sort key).

- Query using only the partition key. For example, find songs by an artist.
- Query using both the partition key and the sort key. For example, find songs by an artist and song title starting with a specific string.
- Filter query results. Find songs by an artist and then return only those songs that have more than three radio stations playing them.

```js
var params = {
    TableName: "Music",
    KeyConditionExpression: "Artist = :artist",
    ExpressionAttributeValues: {
        ":artist": "No One You Know"
    }
};

docClient.query(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});
```

```js
// query for songs by an artist with song title starting with a specific string(s)
var params = {
    TableName: "Music",
    ProjectionExpression: "SongTitle",
    KeyConditionExpression: "Artist = :artist and begins_with(SongTitle, :letter)",
    ExpressionAttributeValues: {
        ":artist": "The Acme Band",
        ":letter": "S"
    }
};

docClient.query(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});
```

**Step 5.2: Filter Query Results**

You can filter results of a query by adding the FilterExpression parameter.

In this example you specify a query to find songs by an artist (The Acme Band).
The query also specifies the FilterExpression to request DynamoDB to return only the song items that are being played on more than three radio stations.

```js

var params = {
    TableName: "Music",
    ProjectionExpression: "SongTitle, PromotionInfo.Rotation",
    KeyConditionExpression: "Artist = :artist",
    FilterExpression: "size(PromotionInfo.RadioStationsPlaying) >= :howmany",
    ExpressionAttributeValues: {
        ":artist": "The Acme Band",
        ":howmany": 3
    },
};

docClient.query(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

```

**Step 5.3: Scan the Table**

You can use the Scan operation to retrieve all of the items in a table.
In the following example you scan the Music table.

```js

var params = {
    TableName: "Music"
};

docClient.scan(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

```

### Work with a Scondary Index

**Without an index, you can query for items based on primary key.**
You can add indexes to your table depending on your query patterns.
DynamoDB supports two different kinds of indexes:

- Global secondary index — an index with a partition key and sort key that can be different from those on the table. You can create or delete a global secondary index on a table at any time.
- Local secondary index — an index that has the same partition key as the primary key of the table, but a different sort key. You can only create a local secondary index when you create a table; when you delete the table, the local secondary index is also deleted.

**Step 6.1: Create a Global Secondary Index**

The Music table has a primary key made of Artist (partition key) and SongTitle (sort key). Now suppose you want to query this table by Genre and find all of the Country songs. Searching on the primary key does not help in this case. To do this, we build a secondary index with Genre as the partition key.

To make this interesting, we use the Price attribute as the sort key. So you can now run a query to find all Country songs with Price less than 0.99.

You can add an index at the time that you create a table or later using the UpdateTable operation.

```js

var params = {
    TableName: "Music",
    AttributeDefinitions:[
        {AttributeName: "Genre", AttributeType: "S"},
        {AttributeName: "Price", AttributeType: "N"}
    ],
    GlobalSecondaryIndexUpdates: [
        {
            Create: {
                IndexName: "GenreAndPriceIndex",
                KeySchema: [
                    {AttributeName: "Genre", KeyType: "HASH"},  //Partition key
                    {AttributeName: "Price", KeyType: "RANGE"},  //Sort key
                ],
                Projection: {
                    "ProjectionType": "ALL"
                },
                ProvisionedThroughput: {
                    "ReadCapacityUnits": 1,"WriteCapacityUnits": 1
                }
            }
        }
    ]
};

dynamodb.updateTable(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

```

- *AttributeDefinitions* lists data types of attributes that are later defined as the partition key and sort key of the index.
- *GlobalSecondaryIndexUpdates* specifies the index operations. You can create index, update index, or delete an index.
- The *ProvisionedThroughput* parameter is required, but the downloadable version of DynamoDB ignores it.

**Step 6.2: Query the Index**

Now we use the index to query for all Country songs.
The index has all of the data you need, so you query the index and not the table.

You use the same Query operation to query a table (see Step 5: Query and Scan the Table) or an index on the table.
When you query an index you specify both the table name and the index name.

```js

var params = {
    TableName: "Music",
    IndexName: "GenreAndPriceIndex",
    KeyConditionExpression: "Genre = :genre",
    ExpressionAttributeValues: {
        ":genre": "Country"
    },
    ProjectionExpression: "SongTitle, Price"
};

docClient.query(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

```

### Modify Items in the Table

**Step 7.1: Update an Item**

The UpdateItem API operation lets you do the following:

- Add more attributes to an item.
- Modify the values of one or more attributes in the item.
- Remove attributes from the item.

By default, UpdateItem operation does not return any data (empty response).
You can optionally specify the ReturnValues parameter to request attribute values as they appeared before or after the update:

- `ALL_OLD` returns all attribute values as they appeared before the update.
- `UPDATED_OLD` returns only the updated attributes as they appeared before the update.
- `ALL_NEW` returns all attribute values as they appear after the update.
- `UPDATED_NEW` returns only the updated attributes as they appeared after the update.

```js
// add new 'RecordLabel attribute and the value'
var params = {
    TableName: "Music",
    Key: {
        "Artist":"No One You Know",
        "SongTitle":"Call Me Today"
    },
    UpdateExpression: "SET RecordLabel = :label",
    ExpressionAttributeValues: { 
        ":label": "Global Records"
    },
    ReturnValues: "ALL_NEW"
};

docClient.update(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

// update price and remove Tags.Composers value
var params = {
    TableName: "Music",
    Key: {
        "Artist":"No One You Know",
        "SongTitle":"Call Me Today"
    },
    UpdateExpression: 
        "SET Price = :price REMOVE Tags.Composers[2]",
    ExpressionAttributeValues: { 
        ":price": 0.89
    },
    ReturnValues: "ALL_NEW"
};
docClient.update(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

```

**Specify a Conditional Write**

By default updates are performed unconditionally.
You can specify a condition in the UpdateItem operation to perform conditional update.
For example, you may want to check if an attribute exists before changing its value, or check the existing value and apply an update only if the existing value meets certain criteria.

The UpdateItem operation provides ConditionExpression parameter for you to specify one or more conditions.

```js
var params = {
    TableName: "Music",
    Key: {
        "Artist":"No One You Know",
        "SongTitle":"Call Me Today"
    },
    UpdateExpression: "SET RecordLabel = :label",
    ExpressionAttributeValues: { 
        ":label": "New Wave Recordings, Inc."
    },
    ConditionExpression: "attribute_not_exists(RecordLabel)",
    ReturnValues: "ALL_NEW"
};

docClient.update(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});
```

**Specify an Atomic Counter**

DynamoDB supports atomic counters, where you use the UpdateItem operation to increment or decrement the value of an existing attribute without interfering with other write requests.
(All write requests are applied in the order in which they were received.) For example, a music player application might want to maintain a counter each time song is played.
In this case, the application would need to increment this counter regardless of its current value.
For more information, go to Atomic Counters in the Amazon DynamoDB Developer Guide.

```js
var params = {
    TableName: "Music",
    Key: {
        "Artist":"No One You Know",
        "SongTitle":"Call Me Today"
    },
    UpdateExpression: "SET Plays = :val",
    ExpressionAttributeValues: { 
        ":val": 0
    },
    ReturnValues: "UPDATED_NEW"
};
docClient.update(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

var params = {
    TableName: "Music",
    Key: {
        "Artist":"No One You Know",
        "SongTitle":"Call Me Today"
    },
    UpdateExpression: "SET Plays = :val",
    ExpressionAttributeValues: { 
        ":val": 0
    },
    ReturnValues: "UPDATED_NEW"
};
docClient.update(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});
```

**Step 7.2: Delete an Item**

You now use the DeleteItem API operation to delete an item from the table.
Note that this operation is permanent—there is no way to restore an item.

```js
var params = {
    TableName: "Music",
    Key: {
        Artist: "The Acme Band", 
        SongTitle: "Look Out, World"
    }
};

docClient.delete(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

// conditional
var params = {
    TableName: "Music",
    Key: {
        Artist: "No One You Know", 
        SongTitle: "My Dog Spot"
    },
    ConditionExpression: "Price = :price",
    ExpressionAttributeValues: {
        ":price": 0.00
    }
};
```

### Clean Up

```js
var params = {
    TableName: "Music"
};

dynamodb.deleteTable(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});
```

## 정리

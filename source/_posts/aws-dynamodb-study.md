---
layout: post
title: AWS DynamoDB 정리 1부 테이블 만들기, 테이블 정보보기, 데이터 읽기
categories:
  - Database
tags:
  - Database
  - Dynamodb
---

## 참조


- [Amazon DynamoDB 사용 방법](http://docs.aws.amazon.com/ko_kr/amazondynamodb/latest/developerguide/HowItWorks.html)

## 배경

드디어 나와 사부가 만들던 어플리케이션에서 서버 부분까지 내가 담당해 보기로 했다.

사부는 nodejs와 aws dynamodb로 서버를 개발하고 있었는데 나도 처음으로 그 부분에 대해서 공부하게 되었다.

그런데 이제까지는 mysql정도 밖에 다루어 보지 않았어서 aws dynamodb는 정말 생소하였다.

그래서 이 포스트를 남겨 앞으로 dynamodb를 쓸 때 참고를 하고자 한다. 

## 핵심

- primaryKey에는 partitionKey와 sortKey로 나누어져있다.(paritionKey만 있는 경우도 있음.)

- partitionKey는 겹치더라도, sortKey는 겹치지 않는다.

## 기본 내용

### Create a Table

```js
// setting dynamo db table
var params = {
    TableName : "Music",
    KeySchema: [       
        { AttributeName: "Artist", KeyType: "HASH" },  //Partition key
        { AttributeName: "SongTitle", KeyType: "RANGE" }  //Sort key
    ],
    AttributeDefinitions: [       
        { AttributeName: "Artist", AttributeType: "S" },
        { AttributeName: "SongTitle", AttributeType: "S" }
    ],
    ProvisionedThroughput: {       
        ReadCapacityUnits: 1, 
        WriteCapacityUnits: 1
    }
};

dynamodb.createTable(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

```

- The params object holds the parameters for the corresponding DynamoDB API operation.
- The dynamodb.<operation> line invokes the operation, with the correct parameters. In the example above, the operation is createTable.

### Get Information About Tables

```js
// Retrieve a Table Description
var params = {
    TableName: "Music"
};

dynamodb.describeTable(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

// Retrieve a List of Tables
var params = {};

dynamodb.listTables(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});


```

### Write Items to the Table

```js
// Write a Item
var params = {
    TableName: "Music",
    Item: {
        "Artist":"No One You Know",
        "SongTitle":"Call Me Today",
        "AlbumTitle":"Somewhat Famous",
        "Year": 2015,
        "Price": 2.14,
        "Genre": "Country",
        "Tags": {
            "Composers": [
                  "Smith",
                  "Jones",
                  "Davis"
            ],
            "LengthInSeconds": 214
        }
    }
    // Writing succeed only when it satisfy the ConditionExpression's content. if not, it simply overwrite.
    // "ConditionExpression": "attribute_not_exists(Artist) and attribute_not_exists(SongTitle)"
};

```
- Artist and SongTitle are primary key attributes (partition key and sort key, respectively). Both are of string type. Every item that you add to the table must have values for these attributes.
- Other attributes are AlbumTitle (string), Year (number), Price (number), Genre (string), and Tags (map).
- DynamoDB allows you to nest attributes within other attributes. The Tags map contains two nested attributes—Composers (list) and LengthInSeconds (number).
- Artist, SongTitle, AlbumTitle, Year, Price, Genre, and Tags are top-level attributes because they are not nested within any other attributes.

```js
// Write Multiple Items
var params = {
    RequestItems: {
        "Music": [ 
            {  
                PutRequest: {
                    Item: {
                        "Artist": "No One You Know",
                        "SongTitle": "My Dog Spot",
                        "AlbumTitle":"Hey Now",
                        "Price": 1.98,
                        "Genre": "Country",
                        "CriticRating": 8.4
                    }
                }
            }, 
            { 
                PutRequest: {
                    Item: {
                        "Artist": "No One You Know",
                        "SongTitle": "Somewhere Down The Road",
                        "AlbumTitle":"Somewhat Famous",
                        "Genre": "Country",
                        "CriticRating": 8.4,
                        "Year": 1984
                    }
                }
            }, 
            { 
                PutRequest: {
                    Item: {
                        "Artist": "The Acme Band",
                        "SongTitle": "Still In Love",
                        "AlbumTitle":"The Buck Starts Here",
                        "Price": 2.47,
                        "Genre": "Rock",
                        "PromotionInfo": {
                            "RadioStationsPlaying":[
                                "KHCR", "KBQX", "WTNR", "WJJH"
                            ],
                            "TourDates": {
                                "Seattle": "20150625",
                                "Cleveland": "20150630"
                            },
                            "Rotation": "Heavy"
                        }
                    }
                }
            }, 
            { 
                PutRequest: {
                    Item: {
                        "Artist": "The Acme Band",
                        "SongTitle": "Look Out, World",
                        "AlbumTitle":"The Buck Starts Here",
                        "Price": 0.99,
                        "Genre": "Rock"
                    }
                }
            }
        ]
    }
};

docClient.batchWrite(params, function (err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

```

### Read an Item Using Its Primary Key

```js
// Read an Item Using GetItem

var params = { 
    TableName: "Music",
    Key: {
        "Artist": "No One You Know",
        "SongTitle": "Call Me Today"
    }
};

docClient.get(params, function(err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

//// Result : It is very different from get multiple datas using batchGet api.

{
  "Item": {
    "Artist": "No One You Know",
    "Year": 2015,
    "Price": 2.14,
    "SongTitle": "Call Me Today",
    "AlbumTitle": "Somewhat Famous",
    "Genre": "Country",
    "Tags": {
      "Composers": [
        "Smith",
        "Jones",
        "Davis"
      ],
      "LengthInSeconds": 214
    }
  }
}

// only Read an item's subset of attributes

var params = { 
    TableName: "Music",
    Key: {
        "Artist": "No One You Know",
        "SongTitle": "Call Me Today"
    },
    ProjectionExpression: "AlbumTitle"
};

// when it comes to Reserved word (Year)

var params = { 
    TableName: "Music",
    Key: {
        "Artist": "No One You Know",
        "SongTitle": "Call Me Today"
    },
    ProjectionExpression: "AlbumTitle, #y", // #y is placeholder token
    ExpressionAttributeNames: {"#y": "Year"}
};

// Read maps / list data

var params = { 
    TableName: "Music",
    Key: {
        "Artist": "No One You Know",
        "SongTitle": "Call Me Today"
    },
    ProjectionExpression: "AlbumTitle, #y, Tags.Composers[0], Tags.LengthInSeconds",
    ExpressionAttributeNames: {"#y": "Year"}
};

// Read multiple items

var params = {
    RequestItems: {
        "Music": {
            Keys: [
                {
                    "Artist": "No One You Know",
                    "SongTitle": "My Dog Spot"
                },
                {
                    "Artist": "No One You Know",
                    "SongTitle": "Somewhere Down The Road"
                },
                {
                    "Artist": "The Acme Band",
                    "SongTitle": "Still In Love"
                },
                {
                    "Artist": "The Acme Band",
                    "SongTitle": "Look Out, World"
                }
            ],
        }
    }
};

docClient.batchGet(params, function (err, data) {
    if (err)
        console.log(JSON.stringify(err, null, 2));
    else
        console.log(JSON.stringify(data, null, 2));
});

// Result

{
  "Responses": {
    "Music": [
      {
        "Artist": "The Acme Band",
        "PromotionInfo": {
          "TourDates": {
            "Seattle": "20150625",
            "Cleveland": "20150630"
          },
          "Rotation": "Heavy",
          "RadioStationsPlaying": [
            "KHCR",
            "KBQX",
            "WTNR",
            "WJJH"
          ]
        },
        "AlbumTitle": "The Buck Starts Here",
        "Genre": "Rock",
        "Price": 2.47,
        "SongTitle": "Still In Love"
      },
      {
        "Artist": "No One You Know",
        "AlbumTitle": "Somewhat Famous",
        "Genre": "Country",
        "Year": 1984,
        "SongTitle": "Somewhere Down The Road",
        "CriticRating": 8.4
      },
      {
        "Artist": "The Acme Band",
        "AlbumTitle": "The Buck Starts Here",
        "Genre": "Rock",
        "Price": 0.99,
        "SongTitle": "Look Out, World"
      },
      {
        "Artist": "No One You Know",
        "AlbumTitle": "Hey Now",
        "Genre": "Country",
        "Price": 1.98,
        "SongTitle": "My Dog Spot",
        "CriticRating": 8.4
      }
    ]
  },
  "UnprocessedKeys": {}
}

```

## 정리

To be continued...
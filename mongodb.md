# MongoDB

## From console
`db.iMatrixBin.find({binBarcode: "A2_RFID"}).pretty()`
`db.iMatrixBin.find({binBarcode: "A2_RFID"},{_id:1}).pretty()`
**Second find argument is PROJECT which is columns to return**
 
## From compass just get the _id
`FILTER: {binBarcode: "A2_RFID"}`  
`PROJECT: {_id:1}`
 
### Bins created after x
`{"createTime" : { $gte : new ISODate("2018-09-17T00:00:00Z") }}`
 
### Bins latest status inTransit after a time
`{$and: [{"status.stateTime" : { $gte : new ISODate("2020-06-02T17:00:00Z") }}, { "status.state": 'inTransit' }]}` 
### Bins created after x and that have tubes in them
`{$and: [{"createTime" : { $gte : new ISODate("2018-09-17T00:00:00Z") }},{ tubes: { $ne: 1.99 } }, { tubes: { $exists: true } }]}` 
### BinEvents inTransit after 
`{$and: [{"eventTime" : { $gte : new ISODate("2020-06-01T00:00:00Z") }}, { binState: 'inTransit' }]}` 

### Filtered without _Id and only binBarcode and sortSessionId
`{_id: 0, binBarcode : 1, sortSessionId: 1}` 

### Bins where barcode ends in _rfid
`{ "binBarcode": /.*_rfid$/ }`
 
### Bins with a tube barcode
`{'tubes._id' : "0095447683010a5007 507349"}`
 
### Find sortgroup starts with BAD... and has a specific barcode
`{$and: [{ "sortGroup": /^BAD.*/ },{ "binBarcode": "PB017321B0000096" }]}`
 
### Count
```
db.iMatrixBin.aggregate( [
   { $count: "count" }
])
```
 
## Group By Examples
### select binBarcode, count(*) from iMatrixBin group by binBarcode
```
db.iMatrixBin.aggregate(
    { $group : { 
        _id : "$binBarcode",
        count : { $sum : 1 } 
      } 
    }
)    
 
db.iMatrixBin.aggregate([
    { $group : { 
        _id : { binBarcode : "$binBarcode", sortGroup : "$sortGroup" },
        count : { $sum : 1 } 
      } 
    },
    {$sort:{"_id.binBarcode" : 1}}
]).pretty()    
```

### Interesting SQL to Mongo Aggregation Chart 
https://docs.mongodb.com/manual/reference/sql-aggregation-comparison/
 
 
## !!! These are still under investigation !!!
```
db.iMatrixBin.group(
   {
     key: { "binBarcode": 1, "_id": 1},
     cond: { "binBarcode": "A2_RFID"},
     reduce: function ( curr, result ) { 
            result.total += 1
        },
     initial: { total : 0 }
   }
)
 
 
db.iMatrixBin.aggregate( [
{ "$group": {
  "_id": "$_id",
  "name": { "$first": "$name" },  //$first accumulator
  "count": { "$sum": 1 },  //$sum accumulator
  "totalValue": { "$sum": "$value" }  //$sum accumulator
}}
] )
```

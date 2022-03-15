# GET Bill

Method | syntax
----- | ----------
GET | https://www.putnamapp.com/bill


## Description

Receives a table number and returns that table's bill including the details of all item's ordered.

Parameters

Name | type | Req. | Description
---- | ----- | ----- | --------------------
tableNumber | int | Y |  The table number for the desired bill. For takeout orders, use 99.


## Examples

### Request

```BASH
// Sample request using cURL
curl -XGET 'https://putnamapp.com/bill?tableNumber=12'
```

<!-- Follow with comments to explain what each part of the request is doing -->

### Response

```JSON
{
   "orderNum":123,
   "timestamp":"2020-01-21T07:44:45-05:00",
   "Item1":{
  	"ItemOrdered":{
     	"type":"burgerMeal",
     	"Cost":10.99
  	}
   },
   "Item2":{
  	"ItemOrdered":{
     	"type":"salad",
     	"Cost":9.50
  	}
   }
}
```

<!-- Write a comment explaining the response, if it would be helpful. For a response with a complicated schema, create a table like the one used above for the request.  -->

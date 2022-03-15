# GET Bill

Method | syntax
----- | ----------
GET | https://www.putnamapp.com/bill


## Description

Receives a table number and returns that table's bill including the details of all item's ordered.

### Query Parameters

Name | type | Req. | Description
---- | ----- | ----- | --------------------
tableNumber | int | Y |  The table number for the desired bill. For takeout orders, use 99.

### Response Object

Name | type | Description
-----| -----| -----------
orderNumber | int | The order ID number used to generate the bill.
timestamp | ISO 8601 timestamp | The date and time when the bill was generated.
totalCost | float | The total cost of all the items on the bill.
items | Array\<item\> | An array of 'item' objects representing all the items on the bill.
   
#### Item object

Name | type | Description
-----| -----| -----------
item | string | The menu item.
cost | float | The menu item's cost.


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
  "orderNumber": 123,
  "timestamp": "2020-01-21T07:44:45-05:00",
  "totalCost" : 20.49,
  "items": [
    {
      "item": "burgerMeal",
      "cost": 10.99
    },
    {
      "item": "salad",
      "cost": 9.50
    }
  ]
}
```

<!-- Write a comment explaining the response, if it would be helpful. For a response with a complicated schema, create a table like the one used above for the request.  -->

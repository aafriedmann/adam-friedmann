# Order Meal

Method | syntax
----- | ----------
POST | https://putnamapp.com/order


## Description

Creates a meal order and associates it with a table.

> **Note**  
> The POC version of the app only supports the `burgerMeal` menu item.

### Parameters

Requests to this endpoint must include an object that defines the type of meal, the menu items ordered

Name | type | Req. | Description
---- | ----- | ----- | --------------------
Parameter_one | string | Y |  Stores the customer name
Parameter_two | int  | N | Stores a postal code, like the U.S. ZIP code.

<!-- Replace the two example rows and include rows for all your parameters. -->
<!-- If one of the parameters has a set of sub-parameters, create a table or bulleted list for that, but proceed with caution. If the API is complex, there might be an easier way to do your reference section than writing markup by hand. -->

## Examples

### Request

```HTTP
<!--  A copy-and-paste working request, if possible. Not one with values replaced by their names, such as "ID." -->

```

<!-- Follow with comments to explain what each part of the request is doing -->

### Response

```HTTP
<!--  An actual response returned by this endpoint for the request above.  -->

```

<!-- Write a comment explaining the response, if it would be helpful. For a response with a complicated schema, create a table like the one used above for the request.  -->

```JSON
{
    "mealType": "lunch",
    "menuItem": "burgerMeal", // If it's a burgerMeal, the app accepts the following in the "mealComponents" section (burger (required), sides (optional), drink(optional))
    "mealComponents": {
        "burger": {
            "pattyType": "beef",
            "pattyQuantity": 1,
            "pattyWeight": 300, // In grams
            "pattyCook": "MR",
            "bunType": "wholeWheat", //white, glutenFree
            "condiments": [
                "ketchup",
                "secretSauce" //mustard, chimichuri, relish
            ], //2 included
            "toppings": [
                "lettuce",
                "pickles"
            ] // 3 included
        },
        "sides": [ // limit of 2
            {
                "type": "frenchFries",
                "size": "L" // S, M, L (small included in price, M and L add to price)
            },
            {
                "type": "none", //No need for this.
                "size": ""
            }
        ],
        "drink": {
            "type": "coke",
            "size": "L", // S, M, L, XL (small or medium included in price, L, XL add to price)
            "ice": true
        }
    }
}
```

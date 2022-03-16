# Order Meal

Method | syntax
----- | ----------
POST | https://putnamapp.com/order


## Description

Creates a meal order and associates it with a table.

> **Note**  
> The POC version of the app only supports the `burgerMeal` menu item.

### Parameters

Name | type | Req. | Description
---- | ----- | ----- | --------------------
mealType | string | Y |  The meal being ordered. <br>Options: <ul><li>`"breakfast"`</li><li>`"lunch"`</li><li>`"dinner"`</li></ul>
tableNumber | int  | Y | The table to associated with the order.
menuItems | Array\<menuItem\>| Y | An array of the `menuItem` objects included in the order

#### Menu Items

These are the menu items you can include in the `menuItems` array. They represent all the things available on Putnam Diner menu. `Meal` items are collection objects that contain the components that make up a meal, including other menu items.

##### burger
An object representing a burger. `burger` items contain the following properties:

Name | type | Req. | Description
-----| -----| ---- | -----------
pattyType | string | Y | The type of patty in the burger. <br>Options: <ul><li>`"beef"`</li><li>`"chicken"`</li><li>`"veggie"`</li></ul>
pattyWeight | int | Y | The weight of the patty, in grams. <br>Options: <ul><li>`100`</li><li>`200`</li><li>`300`</li></ul>
pattyCook | string | Y | How cooked the patty is. <br>Options: <ul><li>`"rare"`</li><li>`"mediumRare"`</li><li>`"wellDone"`</li></ul>
pattyQuantity | int | Y | The number of patties in the burger. The maximum value is `3`. The values for `pattyType`, `pattyWeight`, and `pattyCook` are the same for all patties.
bunType | string | Y | The type of bun for the burger. <br>Options: <ul><li>`"white"`</li><li>`"wholeWheat"`</li><li>`"glutenFree"`</li></ul>
condiments | Array\<string\> | N | The condiments for the burger. You can only add 2 condiments to a burger. If the `condiments` array includes more than 2 items, only the first 2 are included in the order. <br>Options: <ul><li>`"ketchup"`</li><li>`"mustard"`</li><li>`"chimichurri"`</li><li>`"mayo"`</li></ul>
toppings | Array\<string\> | N | The toppings for the burger. You can only add 3 toppings to a burger. If the `toppings` array includes more than 3 items, only the first 3 are included in the order. <br>Options: <ul><li>`"lettuce"`</li><li>`"pickles"`</li><li>`"tomatoes"`</li><li>`"friedEgg"`</li></ul>


##### sides
An array of objects representing any side dishes included in the order. Meal items have limits for the amount and size of the side dishes that you can add to the meal. Each side dish object contains the following properties:

Name | type | Req.| Description
---- | ---- | --- | -----------
type | string | Y | The type of side dish. <br>Options: <ul><li>`"frenchFries"`</li><li>`"mashedPotatoes"`</li><li>`"onionRings"`</li><li>`"coleslaw"`</li></ul>
size | string | Y | The size of the side dish. Either `"small"` or `"large"`.

##### Meal Items
Name | Description
---- | -----------
burgerMeal | An object representing a burger meal, containing the following menu items: <ul><li>`burger` (required)</li><li>`sides` (optional, limit: 2 small dishes)</li><li>`drink` (optional)</li></ul>


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
    "tableNumber" : 12,
    "menuItems": [
        { // If it's a burgerMeal, the app accepts the following in the "mealComponents" section (burger (required), sides (optional), drink(optional))
            "burgerMeal" : {
                "burger": {
                    "pattyType": "beef",
                    "pattyQuantity": 1,
                    "pattyWeight": 300, // In grams
                    "pattyCook": "mediumRare",
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
                        "size": "large" // S, M, L (small included in price, M and L add to price)
                    },
                    {
                        "type": "none", //No need for this.
                        "size": ""
                    }
                ],
                "drink": {
                    "type": "coke",
                    "size": "large", // S, M, L, XL (small or medium included in price, L, XL add to price)
                    "ice": true
                }
            }
        }
    ]
}
```

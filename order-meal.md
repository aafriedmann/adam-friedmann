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
mealType | string | Y |  The meal being ordered. <br>Options: `"breakfast"`,`"lunch"`, `"dinner"`
tableNumber | int  | Y | The table to associated with the order.
menuItems | Array\<menuItem\>| Y | An array of the `menuItem` objects included in the order

#### Menu Items

These are the menu items you can include in the `menuItems` array. They represent all the things available on Putnam Diner menu. `Meal` items are collection objects that contain the components that make up a meal, including other menu items.

##### burger
An object representing a burger. `burger` items contain the following properties:

Name | type | Req. | Description
-----| -----| ---- | -----------
pattyType | string | Y | The type of patty in the burger. <br>Options: `"beef"`, `"chicken"`, `"veggie"`
pattyWeight | int | Y | The weight of the patty, in grams. <br>Options: `100`, `200`, `300`
pattyCook | string | Y | How cooked the patty is. <br>Options: `"rare"`, `"mediumRare"`, `"wellDone"`
pattyQuantity | int | Y | The number of patties in the burger. The maximum value is `3`. The values for `pattyType`, `pattyWeight`, and `pattyCook` are the same for all patties.
bunType | string | Y | The type of bun for the burger. <br>Options: `"white"`, `"wholeWheat"`, `"glutenFree"`
condiments | Array\<string\> | N | The condiments for the burger. You can only add 2 condiments to a burger. If the `condiments` array includes more than 2 items, only the first 2 are included in the order. <br>Options: `"ketchup"`, `"mustard"`, `"chimichurri"`, `"mayo"`
toppings | Array\<string\> | N | The toppings for the burger. You can only add 3 toppings to a burger. If the `toppings` array includes more than 3 items, only the first 3 are included in the order. <br>Options: `"lettuce"`, `"pickles"`, `"tomatoes"`, `"friedEgg"`


##### sides
An array of objects representing side dishes included in the order. Meal items have limits for the amount and size of the side dishes that you can add to the meal. Each side dish object contains the following properties:

Name | type | Req.| Description
---- | ---- | --- | -----------
type | string | Y | The type of side dish. <br>Options: `"frenchFries"`, `"mashedPotatoes"`, `"onionRings"`, `"coleslaw"`
size | string | Y | The size of the side dish. Either `"small"` or `"large"`.

##### drink
An array of objects representing drinks included in the order. Meal items have limits for the amount and size of the drinks that you can add to the meal. Each drink object contains the following properties:

Name | type | Req.| Description
---- | ---- | --- | -----------
type | string | Y | The type of drink. <br>Options: `"coke"`, `"dietCoke"`, `"sprite"`, `"water"`
size | string | Y | The size of the side dish. <br>Options: `"small"`, `"large"`
ice | boolean | N | A boolean representing if a drink comes with ice. Defaults to `true`.



##### Meal Items

Each meal item contains several other menu item objects and defines the limits of those items in the meal.

Name | Description
---- | -----------
burgerMeal | An object representing a burger meal, containing the following menu items: <ul><li>`burger`(required, limit: 1)</li><li>`sides` (optional, limit: 2 small dishes)</li><li>`drink` (optional, limit: 1 small or medium drink)</li></ul>



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

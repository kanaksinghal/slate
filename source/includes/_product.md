# Product

The API allows you to create, delete, and update product. The api gives ability to set authorization level privileges using the rules object and metadata storage.

<aside style="background:#5bc0de;">

The Authorization token is a secure token that is only accessible to administrators of Goodcop Api. 
Please contact GoodCop Team for access.

Api that needs a secure token are :

1.  Create Product
2.  Get All Products

</aside>


## Create Product

> Definition

```
POST  https://[GOODCOP_URL]/v1/product

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product"
  -X POST
  -H "Authorization: test_hHHJujfwvRyjjuR" \
  -H "Content-Type: application/json"
  -d '{
	    "name":"test_product"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "id": 6308443803615232,
    "name": "test_product",
    "description": "",
    "authCallback": "",
    "apiRules": null,
    "apiMeta": "",
    "userRules": null,
    "userMeta": "",
    "apiKeys": [
        {
            "name": "default",
            "value": "test_2va8vfZ4j1Ci1qvGreQ-u8OwD3LjYQ9ksegxEp0="
        }
    ]
}

```

Creates a new product object.

### HTTPS Request

`POST https://[GOODCOP_URL]/v1/group`

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
name | required | string | The name of the product.
 

### Returns

Returns a product object. The returned object will have information about the rules, description, metadata and api keys that needs to be used as authorization token for accessing other goodcop api modules. If no product name was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide correct API key`
2.  <code style="background:#FFC107;"> 400 </code> `Name is required field`

## List Products

> Definition

```
GET  https://[GOODCOP_URL]/v1/product

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product"
  -X GET
  -H "Authorization: test_hHHJujfwvRyjjuR" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "Products": [
        {
            "id": 5735995932672000,
            "name": "product_1",
            "description": "product_1",
            "authCallback": "https://requestb.in/1f4y9ho1",
            "apiRules": [
                {
                    "verb": "POST",
                    "path": "/product_1/billing",
                    "effect": false
                },
                {
                    "verb": "POST",
                    "path": "/product_1/billin",
                    "effect": true
                },
                {
                    "verb": "POST",
                    "path": "/dkd",
                    "effect": false
                }
            ],
            "apiMeta": "123",
            "userRules": null,
            "userMeta": "",
            "apiKeys": [
                {
                    "name": "default",
                    "value": "FIaxZkJNOmj3MjPNgo2tFvZOXvWbNAdlAWWaAZnb9fg="
                }
            ]
        },
        {
            "id": 5760586365272064,
            "name": "product_2",
            "description": "product_2",
            "authCallback": "",
            "apiRules": null,
            "apiMeta": "",
            "userRules": [
                {
                    "verb": "GET",
                    "path": "/hello/hi",
                    "effect": true
                }
            ],
            "userMeta": "",
            "apiKeys": [
                {
                    "name": "default",
                    "value": "II4htdb2eUx0FKDrA7Fr0INyd4WsamLlrzCIjKW8fTI="
                }
            ]
        },
        {
            "id": 5750501782061056,
            "name": "product_3",
            "description": "product_3",
            "authCallback": "",
            "apiRules": null,
            "apiMeta": "",
            "userRules": null,
            "userMeta": "",
            "apiKeys": [
                {
                    "name": "default",
                    "value": "aIsKmHDTaSvYJ7JBzc5_QsnJZ4UWJFwMgt5AIA4Oyvs="
                }
            ]
        }
    ]
}
```

Retrieves the detailed list of all products.

### HTTPS Request

`GET https://[GOODCOP_URL]/v1/product`

### Returns

Returns a list of product objects. If any other backend failures an appropriate error message will be returned with an error code associated with it.

### Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide correct API key`
2.  <code style="background:#FFC107;"> 400 </code> `Name is required field`



## Get Product By ID

> Definition

```
GET  https://[GOODCOP_URL]/v1/product/{productID}

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5735995932672000"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "id": 5735995932672000,
    "name": "product_1",
    "description": "123",
    "authCallback": "https://requestb.in/1f4y9ho1",
    "apiRules": [
        {
            "verb": "POST",
            "path": "/product_1/billing",
            "effect": false
        },
        {
            "verb": "POST",
            "path": "/product_1/billin",
            "effect": true
        },
        {
            "verb": "POST",
            "path": "/dkd",
            "effect": false
        }
    ],
    "apiMeta": "123",
    "userRules": null,
    "userMeta": "",
    "apiKeys": [
        {
            "name": "default",
            "value": "test_3MjPNgo2tFvZOXvWbNAdlAWWaAZnb9fg="
        }
    ]
}

```

Retrieves the details of an existing product. You need only supply the unique product identifier that was returned upon product creation.

### HTTPS Request

`GET https://[GOODCOP_URL]/v1/product/{productID}`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns a product object if a valid identifier was provided. If invalid product ID was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`


## Update Product By ID

Provide the product details and Goodcop will return the updated product information.

> Definition

```
PUT  https://[GOODCOP_URL]/v1/product/{productID}

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/6308443803615232"
  -X PUT
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
  -d '{
	"name":"test_product",
	"description":"This is test description",
	"apiMeta": "test meta",
	"authCallback":"/callback",
	"apiRules":[{
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
		
	}],
	"userRules":[{
            "verb": "GET",
            "path": "/new/5687539843203072",
            "effect": true
		
	}],
	"userMeta":"user meta"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
	"name":"test_product",
	"description":"This is test description",
	"apiMeta": "test meta",
	"authCallback":"/callback",
	"apiRules":[{
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
		
	}],
	"userRules":[{
            "verb": "GET",
            "path": "/new/5687539843203072",
            "effect": true
		
	}],
	"userMeta":"user meta"
}

```

Updates the product information by setting the value of the body parameter passed.

### HTTPS Request

`PUT https://[GOODCOP_URL]/v1/product/{productID}`

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
name | optional | string | name of the product
description | optional | string |  description of the product 
authCallback | optional | string | define a callback for federated auth 
apiMeta | optional | string | meta information of the api 
apiRules | optional | array | rules of api
userMeta | optional | string | meta information of the user 
userRules | optional | array | rules of user  

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid user identifier 

### Returns

Returns updated product object. If invalid product ID or any other backend failures an appropriate error message will be returned with an error code associated with it.


## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`

## Delete Product By ID

> Definition

```
DELETE  https://[GOODCOP_URL]/v1/product/{productID}

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5178306911535104"
  -X DELETE
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "message": "Product Deleted Successfully"
}
```

Deletes a product permanently.

### HTTPS Request

`DELETE https://[GOODCOP_URL]/v1/product/{productID}`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns a message on success. If the product ID does not exist or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`

## Update Product Meta By ID

> Definition

```
PUT  https://[GOODCOP_URL]/v1/product/{productID}/meta

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5178306911535104/meta"
  -X PUT
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "category: user" \
  -H "Content-Type: application/json"
  -d '{
	    "meta":"meta updated successfully"
    }'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "meta": "meta updated successfully"
}
```

Updates the meta by setting the value of the body parameter passed.

<aside style="background:#5bc0de;">
The category header can be provided with two options either api or user depending on which type meta you want to change 
</aside>


### HTTPS Request

`PUT https://[GOODCOP_URL]/v1/product/{productID}/meta`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns updated meta string. If invalid product ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`

## Get Product Meta By ID

> Definition

```
GET  https://[GOODCOP_URL]/v1/product/{productID}/meta

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5178306911535104/meta"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "category: api" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "apiMeta": "test meta"
}
```
Retrieves the meta details provided the product ID.

<aside style="background:#5bc0de;">
The category header can be provided with two options either api or user depending on which type meta you want to change 
</aside>

### HTTPS Request

`GET https://[GOODCOP_URL]/v1/product/{productID}/meta`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns meta string. If invalid product ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`

## Delete Product Meta By ID

> Definition

```
DELETE  https://[GOODCOP_URL]/v1/product/{productID}/meta

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5178306911535104/meta"
  -X DELETE
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "category: api" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "message": "meta deleted successfully"
}
```

Replaces the meta with empty string.

<aside style="background:#5bc0de;">
The category header can be provided with two options either api or user depending on which type meta you want to change 
</aside>

### HTTPS Request

`DELETE https://[GOODCOP_URL]/v1/product/{productID}/meta`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns success message on succesfull deletion of meta. If invalid product ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`


## Get Product Rules By ID

> Definition

```
GET  https://[GOODCOP_URL]/v1/product/{productID}/rule

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5178306911535104/rule"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "category: api" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "apiRules": [
        {
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
}
```
Retrieves the details of all rules for a product.

<aside style="background:#5bc0de;">
The category header can be provided with two options either api or user depending on which type meta you want to change 
</aside>

### HTTPS Request

`GET https://[GOODCOP_URL]/v1/product/{productID}/rule`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns the list of product rules. If invalid product ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`


## Update Product Rules By ID

> Definition

```
PUT  https://[GOODCOP_URL]/v1/product/{productID}/rule

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5178306911535104/rule"
  -X PUT
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "category: api" \
  -H "Content-Type: application/json"
  -d ' [
        {
            "verb": "PUT",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "apiRules": [
        {
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
        },
        {
            "verb": "PUT",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
}
```

Updates the rules by setting the value of the body parameter passed.

<aside style="background:#5bc0de;">
The category header can be provided with two options either api or user depending on which type meta you want to change 
</aside>

### HTTPS Request

`PUT https://[GOODCOP_URL]/v1/product/{productID}/rule`

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
rules | required | array | rules to be updated 

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns updated rules for the product. If invalid product ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`
3.  <code style="background:#FFC107;"> 400 </code> `Not Acceptable - You requested a wrong rule format`

## Delete Product Rules By ID

> Definition

```
DELETE  https://[GOODCOP_URL]/v1/product/{productID}/rule

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/5178306911535104/rule"
  -X DELETE
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "category: api" \
  -H "Content-Type: application/json"
  -d ' [
        {
            "verb": "PUT",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
'
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "apiRules": [
        {
            "verb": "GET",
            "path": "/credentials/5687539843203072",
            "effect": true
        }
    ]
}
```

Deletes the rules from the product.

### HTTPS Request

`DELETE https://[GOODCOP_URL]/v1/product/{productID}/rule`

### Request Body

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
rules | required | array | rules to be deleted 

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier 

### Returns

Returns updated rules for the product. If invalid product ID or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`
3.  <code style="background:#FFC107;"> 400 </code> `Not Acceptable - You requested a wrong rule format`

## Create Product APIKey By ID

> Definition

```
PUT  https://[GOODCOP_URL]/v1/product/{productID}/apikey/{apikeyname}

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/6308443803615232/apikey/testKey"
  -X PUT
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "ApiKeys": [
        {
            "name": "default",
            "value": "test_y2va8vfZ4j1Ci1qvGreQ-u8OwD3LjYQ9ksegxEp0="
        },
        {
            "name": "testKey",
            "value": "test_Gc11rS8g0sTh6Iz1QFz-nvnK6Ou3j5VxZ9z_6JU="
        }
    ]
}

```

Creates a new product api key.

### HTTPS Request

`PUT https://[GOODCOP_URL]/v1/product/{productID}/apikey/{apikeyname}`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier
apikeyname | required | string | Name of the api key to be generated
 

### Returns

Returns a list of all api keys. The returned object will have information of the new key and can be used to access goodcop modules. If no api name was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`
3.  <code style="background:#FFC107;"> 400 </code> `APIKEY name already exits. Try with another name`


## Get Product APIKey By ID

> Definition

```
GET  https://[GOODCOP_URL]/v1/product/{productID}/apikey/{apikeyname}

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/6308443803615232/apikey/testKey"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "name": "testKey",
    "value": "yIaoGc11rS8g0sTh6Iz1QFz-nvnK6Ou3j5VxZ9z_6JU="
}

```

Retrieves the details of an existing api key. You need to supply the unique product Id and key name identifier that was returned upon key creation.

### HTTPS Request

`GET https://[GOODCOP_URL]/v1/product/{productID}/apikey/{apikeyname}`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier
apikeyname | required | string | Name of the api key to be generated
 

### Returns

Returns a key details. If invalid product ID, invalid key name was provided or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`
3.  <code style="background:#FFC107;"> 400 </code> `Invalid Key Name`


## Get All Product APIKeys By ID

> Definition

```
GET  https://[GOODCOP_URL]/v1/product/{productID}/apikey

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/6308443803615232/apikey"
  -X GET
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "ApiKeys": [
        {
            "name": "default",
            "value": "1y4y2va8vfZ4j1Ci1qvGreQ-u8OwD3LjYQ9ksegxEp0="
        },
        {
            "name": "testKey",
            "value": "yIaoGc11rS8g0sTh6Iz1QFz-nvnK6Ou3j5VxZ9z_6JU="
        }
    ]
}

```

Retrieves the detailed list of all api keys for the product.

### HTTPS Request

`GET https://[GOODCOP_URL]/v1/product/{productID}/apikey/`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier

### Returns

Returns a list of api keys. If any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`


## Delete Product APIKey By ID

> Definition

```
DELETE  https://[GOODCOP_URL]/v1/product/{productID}/apikey/{apikeyname}

```
> Example Request

```shell
curl "https://[GOODCOP_URL]/v1/product/6308443803615232/apikey/testKey"
  -X DELETE
  -H "Authorization: test_aIsKmHDTaSvYJGHGHJ5_QsnJZ4UWJFwMgt5AIA4Oyvs=" \
  -H "Content-Type: application/json"
```

> Example Response <code style="background:#4CAF50;"> 200</code>

```json
{
    "message": "Key deleted successfuly."
}

```

Deletes a api key from the product permanently.

### HTTPS Request

`DELETE https://[GOODCOP_URL]/v1/product/{productID}/apikey/{apikeyname}`

### URL Params

Parameter | Value | Type | Description
--------- | ------- | --------------- | -----------
productID | required | string | Valid product identifier
apikeyname | required | string | Name of the api key to be generated
 

### Returns

Returns a message on success. If the product ID does not exist, api key name does not exists or any other backend failures an appropriate error message will be returned with an error code associated with it.

## Error Messages

1.  <code style="background:#FF7043;"> 401 </code> `Authorization Error. Kindly provide product API key`
2.  <code style="background:#FFC107;"> 400 </code> `Product API key and Product id doesnt match`
3.  <code style="background:#FFC107;"> 400 </code> `Invalid Key Name`
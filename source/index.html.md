---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Sales Tracker API! You can use this API to access the Sales Tracker API endpoints, which can get information on various users, their products, and categories they track about their products in the database.

# Authentication

## Generate a user's token

```shell
curl -d '{ "user": {"email":"testing@testmail.org", "password":"password"}}' 
     -H "Content-Type: application/json" https://trekab-tracker-api.herokuapp.com/api/v1/tokens
```

> The above command returns JSON structured like this:

```json
{
  "token":"eyJhbGciOiJIUzI1NiJ9.eyJ1c2VyX2lkIjo0LCJleHAiOjE2MDAzMjUwODN9.UL_0mix7S1lipNR_EkYQIBW_z-a6ZCWjZ-DpUCNPUkw",
  "email":"testing@testmail.org"
}
```

This endpoint creates a new token for the user.

### HTTP Request

`POST https://trekab-tracker-api.herokuapp.com/api/v1/tokens`

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: auth_token"
```

> Make sure to replace `auth_token` with your created token.

This API expects for the token to be included in all API requests (that require authenticated users) to the server in a header that looks like the following:

`Authorization: auth_token`

<aside class="notice">
You must replace <code>auth_token</code> with your generated token.
</aside>

# Users

## Get a Specific User

```shell
curl "https://trekab-tracker-api.herokuapp.com/api/v1/users/<ID>"
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"4",
      "type":"user",
      "attributes":{"email":"test@testmail.org"},
      "relationships":{"products":{"data":[]}}
    },
    "included":[]
}
```

This endpoint retrieves a specific user.

### HTTP Request

`GET https://trekab-tracker-api.herokuapp.com/api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to retrieve


## Create a new user(sign up)

```shell
curl -d '{ "user": {"email":"test@testmail.org", "password":"password"}}' 
     -H "Content-Type: application/json" https://trekab-tracker-api.herokuapp.com/api/v1/users
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"5",
      "type":"user",
      "attributes":{"email":"test1@testmail.org"},
      "relationships":{"products":{"data":[]}}
    }
}
```

This endpoint creates a new user.

### HTTP Request

`POST https://trekab-tracker-api.herokuapp.com/api/v1/users`

## Update a specific user

```shell
curl -d '{ "user": {"email":"testing@testmail.org", "password":"password"}}' 
     -H "Authorization: auth_token" 
     -H "Content-Type: application/json" 
     -X PUT https://trekab-tracker-api.herokuapp.com/api/v1/users/<ID>
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"4",
      "type":"user",
      "attributes":{"email":"testing@testmail.org"},
      "relationships":{"products":{"data":[]}}
    }
}
```
This endpoint updates a specific user.

### HTTP Request

`PUT https://trekab-tracker-api.herokuapp.com/api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to update


## Delete a specific user

```shell
curl "https://trekab-tracker-api.herokuapp.com/api/v1/users/5"
  -X DELETE
  -H "Authorization: auth_token"
```

This endpoint deletes a specific user.

### HTTP Request

`DELETE https://trekab-tracker-api.herokuapp.com/api/v1/users/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the user to delete

# Products

## Get All Products

```shell
curl https://trekab-tracker-api.herokuapp.com/api/v1/products
```

> The above command returns JSON structured like this:

```json
{
  "data":
    [
      {
        "id":"1","type":"product","attributes":{"title":"Heavy Duty Wool Keyboard","price":"70.4230117790916","published":true},"relationships":{"user":{"data":{"id":"1","type":"user"}}}
      },
      {
        "id":"2","type":"product","attributes":{"title":"Fantastic Wooden Wallet","price":"42.700356212483","published":true},"relationships":{"user":{"data":{"id":"1","type":"user"}}}
      },
      {
        "id":"3","type":"product","attributes":{"title":"Ergonomic Concrete Clock","price":"55.5778962259204","published":true},"relationships":{"user":{"data":{"id":"2","type":"user"}}}
      },
      {
        "id":"4","type":"product","attributes":{"title":"Ergonomic Cotton Chair","price":"19.4047560422438","published":true},"relationships":{"user":{"data":{"id":"2","type":"user"}}}
      },
      {
        "id":"5","type":"product","attributes":{"title":"Synergistic Plastic Bag","price":"27.4820485341494","published":true},"relationships":{"user":{"data":{"id":"3","type":"user"}}}
      },
      {
        "id":"6","type":"product","attributes":{"title":"Heavy Duty Wool Gloves","price":"76.8466326275144","published":true},"relationships":{"user":{"data":{"id":"3","type":"user"}}}
      }
    ]
}
```
This endpoint retrieves all products.

### HTTP Request

`GET https://trekab-tracker-api.herokuapp.com/api/v1/products`

## Get a Specific Product

```shell
curl https://trekab-tracker-api.herokuapp.com/api/v1/products/1
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"1",
      "type":"product",
      "attributes": {"title":"Heavy Duty Wool Keyboard","price":"70.4230117790916","published":true},
      "relationships":{"user":{"data":{"id":"1","type":"user"}}}
    },
    "included":
      [
        {"id":"1","type":"user","attributes":{"email":"don.hessel@ullrich.biz"},"relationships":{"products":{"data":[{"id":"1","type":"product"},{"id":"2","type":"product"}]}}}
      ]
}
```
This endpoint retrieves a specific product.

### HTTP Request

`GET https://trekab-tracker-api.herokuapp.com/api/v1/products/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the product to retrieve

## Create a Product

```shell
curl -d '{"product": {"title":"testing product", "price":"50.5", "published":true}}' 
     -H "Authorization: auth_token" -H "Content-Type: application/json" https://trekab-tracker-api.herokuapp.com/api/v1/products
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"7",
      "type":"product",
      "attributes":{"title":"testing product","price":"50.5","published":true},
      "relationships":{"user":{"data":{"id":"4","type":"user"}}}
    }
}
```

This endpoint creates a new product for the user.

### HTTP Request

`POST https://trekab-tracker-api.herokuapp.com/api/v1/products`

## Update a Product

```shell
curl -d '{"product": {"title":"testing product", "price":"50.5", "published":true}}' 
     -H "Authorization: auth_token" -H "Content-Type: application/json" 
     -X PUT https://trekab-tracker-api.herokuapp.com/api/v1/products/7
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"7",
      "type":"product",
      "attributes":{"title":"testing product","price":"50.5","published":true},
      "relationships":{"user":{"data":{"id":"4","type":"user"}}}
    }
}
```

This endpoint updates a product for a specified user.

### HTTP Request

`PUT https://trekab-tracker-api.herokuapp.com/api/v1/products/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the product to update

## Delete a specific product

```shell
curl "https://trekab-tracker-api.herokuapp.com/api/v1/products/7"
  -X DELETE
  -H "Authorization: auth_token"
```

This endpoint deletes a specific product.

### HTTP Request

`DELETE https://trekab-tracker-api.herokuapp.com/api/v1/products/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the product to delete

# Categories
Category endpoints require admin user rights. Please generate the admin user's `auth_token` using the following created admin user's details:

* "email":"admin-testing@testmail.org"
* "password":"password"

## Get All Categories

```shell
curl https://trekab-tracker-api.herokuapp.com/api/v1/categories
```

> The above command returns JSON structured like this:

```json
{
  "data":
    [
      {"id":"1","type":"category","attributes":{"name":"orders"}},
      {"id":"2","type":"category","attributes":{"name":"sales"}},
      {"id":"3","type":"category","attributes":{"name":"Inventory"}}
    ]
}
```
This endpoint retrieves all the categories.

### HTTP Request

`GET https://trekab-tracker-api.herokuapp.com/api/v1/categories`

## Create a new Category

```shell
curl -d '{"category": {"name":"orders"}}' 
     -H "Authorization: auth_token" -H "Content-Type: application/json" https://trekab-tracker-api.herokuapp.com/api/v1/categories
```

> The above command returns JSON structured like this:

```json
{
  "data":
  {
    "id":"1",
    "type":"category",
    "attributes":{"name":"orders"}
  }
}
```

This endpoint creates a new category using the admin user credentials.

### HTTP Request

`POST https://trekab-tracker-api.herokuapp.com/api/v1/categories`

## Update a Specific Category

```shell
curl -d '{"category": {"name":"Orders"}}' 
     -H "Authorization: auth_token" -H "Content-Type: application/json" 
     -X PUT https://trekab-tracker-api.herokuapp.com/api/v1/categories/1
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"1",
      "type":"category",
      "attributes":{"name":"Orders"}
    }
}
```

This endpoint updates a category using the admin user's credentials.

### HTTP Request

`PUT https://trekab-tracker-api.herokuapp.com/api/v1/categories/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the category to update

## Delete a Specific Category

```shell
curl "https://trekab-tracker-api.herokuapp.com/api/v1/categories/4"
  -X DELETE
  -H "Authorization: auth_token"
```

This endpoint deletes a specific category using the admin user's credentials.

### HTTP Request

`DELETE https://trekab-tracker-api.herokuapp.com/api/v1/categories/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the category to delete

<aside class="notice">
You must replace <code>auth_token</code> with the Admin's generated token for all `category` endpoints.
</aside>

# Measurements

## Get All Measurements
```shell
curl https://trekab-tracker-api.herokuapp.com/api/v1/measurements
```

> The above command returns JSON structured like this:

```json
{
  "data":
    [
      {"id":"1","type":"measurement","attributes":{"product_id":8,"category_id":1,"total":50}},
      {"id":"2","type":"measurement","attributes":{"product_id":8,"category_id":2,"total":50}}
    ]
}
```
This endpoint retrieves all measurements.

### HTTP Request

`GET https://trekab-tracker-api.herokuapp.com/api/v1/measurements`

## Get a Specific Measurement

```shell
curl https://trekab-tracker-api.herokuapp.com/api/v1/measurements/1
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"1",
      "type":"measurement",
      "attributes":{"product_id":8,"category_id":1,"total":50}
    }
}
```
This endpoint retrieves a specific measurement.

### HTTP Request

`GET https://trekab-tracker-api.herokuapp.com/api/v1/measurements/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the measurement to retrieve

## Create a new Measurement

```shell
curl -d '{ "measurement": {"total":"50", "product_id":"8", "category_id":"1"}}' 
     -H "Content-Type: application/json" 
     -H "Authorization: auth_token" https://trekab-tracker-api.herokuapp.com/api/v1/measurements
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"1",
      "type":"measurement",
      "attributes":{"product_id":8,"category_id":1,"total":50}
    }
}
```

This endpoint creates a new measurement.

### HTTP Request

`POST https://trekab-tracker-api.herokuapp.com/api/v1/measurements`

## Update a Specific Measurement

```shell
curl -d '{"measurement": {"total":"55", "product_id":"8", "category_id":"1"}}' 
     -H "Authorization: auth_token" -H "Content-Type: application/json" 
     -X PUT https://trekab-tracker-api.herokuapp.com/api/v1/measurements/1
```

> The above command returns JSON structured like this:

```json
{
  "data":
    {
      "id":"1",
      "type":"measurement",
      "attributes":{"product_id":8,"category_id":1,"total":55}
    }
}
```

This endpoint updates a specific measurement for a specified user.

### HTTP Request

`PUT https://trekab-tracker-api.herokuapp.com/api/v1/measurements/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the measurement to update

## Delete a Specific Measurement

```shell
curl "https://trekab-tracker-api.herokuapp.com/api/v1/measurements/2"
  -X DELETE
  -H "Authorization: auth_token"
```

This endpoint deletes a specific measurement.

### HTTP Request

`DELETE https://trekab-tracker-api.herokuapp.com/api/v1/measurements/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the measurement to delete

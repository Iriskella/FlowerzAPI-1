# FlowerZAPI Documentation

<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#introduction">Introduction</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
    </li>
    <li><a href="#base-URL">Base URL</a></li>
    <li><a href="#resources">Resources</a></li>
    <li><a href="#authentication">Authentication</a></li>
    <li><a href="#json-schema">JSON Schema</a></li>
    <li><a href="#encoding">Encoding</a></li>
  </ol>
</details>



<!-- Introduction -->
## Introduction

Welcome to the FlowerzAPI. Here you will learn about our available resources and how to use them with HTTP requests.

---

<!-- GETTING STARTED -->
## Getting Started

Here you can see an example GET request to the FlowerzAPI.

```bash
GET http://localHost:8080/api/flowerBouquet/5fd4b1476027c14028b0e5de
```

Here we are asking for a specific flowerbouquet with the id:5fd4b1476027c14028b0e5de.

The response:

```bash
[
  {
    "_id": "5fd4b1476027c14028b0e5de",
    "color": "WHITE",
    "price": 89.9,
    "size": "M",
    "productDescription": "test test test test test test",
    "productImage": "https://miro.medium.com/max/1200/1*mk1-6aYaf_Bes1E3Imhc0A.jpeg",
    "occasionStyle": "BIRTHDAY",
    "isMixed": true,
    "updatedAt": "2020-12-12T12:06:46.718Z",
    "createdAt": "2020-12-12T12:05:19.018Z"
  }
]
```

*Note: Response may be different due to possible changes in data.

---

<!-- Base URL -->
## Base URL

The base URL, which presents the root for the entire API:

```bash
http://localHost:8080/api
```
---

<!-- Resources -->
## Resources
### User
The Users resource manage user authentication and provides the registered users information.

#### EndPoints
- ``` /users ``` get all users
- ``` /users/:id ``` get, patch or delete specific user
- ``` /users/signup ``` register a user and get temoprety token as a response 
- ``` /users/signin ``` sign in and get temoprety token as a response 

#### Example request:
```bash
  GET http://localHost:8080/api/users/signup HTTP/1.1
```

#### Example response:
```bash
[
  {
    "_id": "5fd3d0bbccb74d3b1c307e64",
    "emailAddress": "test@gmail.com",
    "firstName": "Test",
    "surName": "Testush",
    "phoneNumber": "050-546-6646",
    "addresses": [
      {
        "_id": "5fd4a48331436b3a6cc59173",
        "name": "Home",
        "city": "testavile",
        "street": "testastreet",
        "houseNumber": "4/5",
        "floorNumber": 7,
        "aptNumber": 7
      }
    ],
    "cart": {
      "orders": []
    }
  }
]
```
##### Properties 
* id : *String*-- The User's id. This attribute is generated automatically. 
* emailAddress : *String*-- The User's email address.  Must be a valid email on input.
* firstName : *String* -- The first name of the user.
* surName : *String* -- The last name of the user.
* PhoneNumber : *Number* --The User's phone number. Must be a valid phone number on input.
* addresses : *object Array* -- 
   * id : *String* -- The addresses id. This attribute is generated automatically. 
   * name : *String* -- The type of the address. (Home, Work, etc...)
   * city : *String* - -The city of the user.
   * street : *String* -- The street of the user.
   * houseNumber : *Number* -- The user's house number.
   * floorNumber : *Number* -- The user's floor number.
   * aptNumber : *Number* -- The user's apartment number.

* cart : *Object* -- 
   * orders : *orders Array* -- The orders of the user.
   * totalSum : cart price

### Order
The Order resource provides users orders information.

#### EndPoints
- ``` /order ``` get all orders or add one
- ``` /order/:id ``` get, patch or delete specific order

#### Example request:
```
http://localhost:8080/api/orders/5fd4a82fd0069c37bc46b183
```

#### Example response:
```bash
{
  "_id": "5fd4a82fd0069c37bc46b183",
  "userID": "5fd3d0bbccb74d3b1c307e64",
  "frequencyWeeks": "1",
  "startDate": "11/3",
  "nextShippingDate": "19/3",
  "orderCategory": "BOUQUET",
  "totalSum": 200,
  "updatedAt": "2020-12-12T11:26:12.546Z",
  "createdAt": "2020-12-12T11:25:32.675Z"
}
```
##### Properties 
* id : *String*-- The Order's id. This attribute is generated automatically. 
* UserId: *String*-- The id of the user who registered the order.
* frequencyWeeks: *Number* -- The weekly frequency desired by the user.
* startDate: *Date* -- The First date for the order delivery.
* nextShippingDate: *Date* -- The next date for the order delivery.
* orderCategory: *String* --The order's type of category.
* totalSum: *Number* -- The order's price amount.

### Flower bouquet
The Flower bouquet resource provides information on the product.
Use and requests from this resource require specific authorizations.

#### EndPoints
- ``` /flowerBouquet ``` get all flower bouquets or add one
- ``` /flowerBouquet/:id ``` get, patch or delete specific flower bouquet

#### Example request:
```
http://localHost:8080/api/flowerBouquet
```

#### Example response:
```bash
  {
    "_id": "5fd4dccf95bab7401c0faea3",
    "color": "WHITE",
    "price": 99.9,
    "size": "M",
    "productDescription": "a very nice flower!",
    "productImage": "https://miro.medium.com/max/1200/1*mk1-6aYaf_Bes1E3Imhc0A.jpeg",
    "occasionStyle": "BIRTHDAY",
    "isMixed": true,
    "createdAt": "2020-12-12T15:07:59.111Z",
    "updatedAt": "2020-12-12T15:07:59.111Z",
    "__v": 0
  }
```

##### Properties 
* id : *String*-- The flowerBouquet's id. This attribute is generated automatically. 
* color: *String*-- The color of the flowerBouquet. 
* price: *Number* -- The price of the flowerBouquet.
* size: *String* -- The size of the bouquet (S,M,L,XL).
* productDescription: *String* -- A description of the flowerBouquet. 
* productImage: *String* -- An image of the flowerBouquet.
* occasionStyle: *String* -- The product style of occasion.
* isMixed: *Boolean* -- Flower bouquet diversity.

---

## Authentication

FlowerzAPI require authentication for some of its requests. However, some operations are open and does not require authentication to get data. 

---

## JSON Schema

FlowerzAPI resources support JSON Schema.

---

## Encoding
FlowerzAPI provides JSON as the data format.

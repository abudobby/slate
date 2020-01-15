---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to AirValet Internal API. This is the main api for both the mobile app and web app.


# Users

> Endpoints:


```javascript
     GET  /v1/users
    POST  /v1/users
     GET  /v1/users/:id
     PUT  /v1/users/:id
  DELETE  /v1/users/:id
```
The `User` object is the base object of the app. All requests will require a userId to compelete

## The user object

> A sample response for a user object:

```json
[
    {
        "_id": "5e1d0e574a8ba27f945a61e0",
        "email": "brittanyklepfer@gmail.com",
        "firstName": "Brittany",
        "lastName": "Klepfer",
        "customerId": "cus_GXivgijQFAU39g",
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
        "deviceToken": "29c49a0fd25ba30f24889b1a5857399b5a5be90d2f042e7d87ff8eda5bea319d"
    }
]
```
### Attributes

    field      | description
--------- | -----------
`_id` String | Unique identifier for the user object.
`customerId` String | Unique identifier for stripe object.
`first_name` String | user's first name.
`last_name` String | user's last name.
`email` String | user's email address.
`phone` String | user's phone number.
`deviceToken` String | unique identifier for the device the user is using.
`createdAt` Date | time user object was created
`updatedAt` Date | time user object was last updated

## Create a user

> `POST /v1/users`

```javascript
let userController = require('...controllers/user-controller')

 app.route('/api/v1/users/')
        .post(userController.createUser)
```

> response

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "customerId": "cus_GXivgijQFAU39g",
        "first_name": "Brittany",
        "last_name": "Klepfer",
        "email": "brittanyklepfer@gmail.com",
        "phone": "6518724630",
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

This endpoint creates a new user in the database.

### Arguments

  field      | description
--------- | -----------
`first_name` String | user's first name.
`last_name` String | user's last name.
`email` String | user's email address.
`phone` String | user's phone number.
`password` String | user's password.

## Retrieve a user

> `GET /v1/users/:id`

```javascript
let userController = require('...controllers/user-controller')

 app.route('/api/v1/users/:id')
        .get(userController.fetchUser)
})
```

> response:

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "customerId": "cus_GXivgijQFAU39g",
        "first_name": "Brittany",
        "last_name": "Klepfer",
        "email": "brittanyklepfer@gmail.com",
        "phone": "6518724630",
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

Retrieves the details of an existing user. You need only supply the unique user identifier that was returned upon user creation.

### Arguements

`no arguments`

### Returns

Returns a user object if a valid identifier was provided. When requesting the ID of a user that has been deleted, a subset of the users’s information will be returned, including a deleted property, which will be true.


## Update a user

> `PUT /v1/users/:id`

```javascript
let userController = require('...controllers/user-controller')

 app.route('/api/v1/users/:id')
        .put(userController.updateUser)
})
```

> response:

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "customerId": "cus_GXivgijQFAU39g",
        "first_name": "Brittany",
        "last_name": "Klepfer",
        "email": "brittanyklepfer@gmail.com",
        "phone": "6518724630",
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

Updates the specified user by setting the values of the parameters passed. Any parameters not provided will be left unchanged

### Arguements

`Any argument listed in the object definition`

### Returns

Returns the user object if the update succeeded. Throws an error if update parameters are invalid (e.g. specifying an invalid coupon or an invalid source).


## Delete a user

> `Delete /v1/users/:id`

```javascript
let userController = require('...controllers/user-controller')

 app.route('/api/v1/users/:id')
        .delete(userController.deleteUser)
})
```

> response:

```json
{
  "_id": "cus_GY90URwhYx9Oy5",
  "object": "user",
  "deleted": true
}
```

Permanently deletes a user. It cannot be undone. Also immediately cancels any active bookings on the customer.

### Arguements

`none`

### Returns

Returns an object with a deleted parameter on success. If the user ID does not exist, this call throws an error.
Unlike other objects, deleted users can still be retrieved through the API, in order to be able to track the history of users while still removing their credit card details and preventing any further operations to be performed (such as adding a new bookings).



## List all users

> `GET /v1/users/`

```javascript
let userController = require('...controllers/user-controller')

 app.route('/api/v1/users')
        .get(userController.fetchUsers)
})
```

> response:

```json
{
  "object": "list",
  "url": "/v1/users",
  "has_more": false,
  "data": [
    {
        "_id": "5e1d0e574a8ba27f945a61e0",
        "customerId": "cus_GXivgijQFAU39g",
        "first_name": "Brittany",
        "last_name": "Klepfer",
        "email": "brittanyklepfer@gmail.com",
        "phone": "6518724630",
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
  ]
```

Returns a list of your users. The users are returned sorted by creation date, with the most recent user appearing first.

### Arguements

`none`

### Returns

A object with a data property that contains an array of up to limit customers, starting after user starting_after. Passing an optional email will result in filtering to users with only that exact email address. Each entry in the array is a separate user object. If no more customers are available, the resulting array will be empty. This request should never throw an error.




# Valets

> Endpoints:


```javascript
     GET  /v1/valets
    POST  /v1/valets
     GET  /v1/valets/:id
     PUT  /v1/valets/:id
  DELETE  /v1/valets/:id
```
The `Valet` is used to update bookings and alert users

## The valet object

> A sample response for a valet object:

```json
[
    {
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": "7e1d0e574a8ba27f945a61eF",
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
]
```
### Attributes

    field      | description
--------- | -----------
`_id` String | Unique identifier for the user object.
`user` String | The user object associated with the Valet object
`createdAt` Date | Time valet object was created
`updatedAt` Date | Time valet object was last updated

## Create a valet

> `POST /v1/valets`

```javascript
let valetController = require('...controllers/valet-controller')

 app.route('/api/v1/valet/')
        .post(valetController.createValet)
```

> response

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

This endpoint creates a new valet in the database.

### Arguments

  field      | description
--------- | -----------
`user` String | The user object associated with the valet.

## Retrieve a valet

> `GET /v1/valets/:id`

```javascript
let valetController = require('...controllers/valet-controller')

 app.route('/api/v1/valets/:id')
        .get(valetController.fetchValet)
})
```

> response:

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

Retrieves the details of an existing valet. You need only supply the unique valet identifier that was returned upon valet creation.

### Arguements

`no arguments`

### Returns

Returns a valet object if a valid identifier was provided. When requesting the ID of a valet that has been deleted, a subset of the users’s information will be returned, including a deleted property, which will be true.


## Update a valet

> `PUT /v1/valets/:id`

```javascript
let valetController = require('...controllers/valet-controller')

 app.route('/api/v1/valets/:id')
        .put(valetController.updateValet)
})
```

> response:

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

Updates the specified valet by setting the values of the parameters passed. Any parameters not provided will be left unchanged

### Arguements

`Any argument listed in the object definition`

### Returns

Returns the valet object if the update succeeded. Throws an error if update parameters are invalid (e.g. specifying an invalid coupon or an invalid source).


## Delete a valet

> `Delete /v1/valets/:id`

```javascript
let valetController = require('...controllers/user-controller')

 app.route('/api/v1/users/:id')
        .delete(valetController.deleteValet)
})
```

> response:

```json
{
  "_id": "cus_GY90URwhYx9Oy5",
  "object": "valet",
  "deleted": true
}
```

Permanently deletes a valet. It cannot be undone. Also immediately cancels any active bookings on the valet.

### Arguements

`none`

### Returns

Returns an object with a deleted parameter on success. If the valet ID does not exist, this call throws an error.
Unlike other objects, deleted valets can still be retrieved through the API, in order to be able to track the history of valet while still removing their credit card details and preventing any further operations to be performed (such as adding a new bookings).



## List all valets

> `GET /v1/valets/`

```javascript
let valetController = require('...controllers/valet-controller')

 app.route('/api/v1/valets')
        .get(valetController.fetchValets)
})
```

> response:

```json
{
  "object": "list",
  "url": "/v1/valets",
  "has_more": false,
  "data": [
   {
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
  ]
```

Returns a list of your valets. The valets are returned sorted by creation date, with the most recent user appearing first.

### Arguements

`none`

### Returns

A object with a data property that contains an array of up to limit valats, starting after valet starting_after. Passing an optional email will result in filtering to users with only that exact email address. Each entry in the array is a separate valet object. If no more customers are available, the resulting array will be empty. This request should never throw an error.



















# Bookings

> Endpoints:


```javascript
     GET  /v1/bookings
    POST  /v1/bookings
     GET  /v1/bookings/:id
     PUT  /v1/bookings/:id
  DELETE  /v1/bookings/:id
```
The `Booking` is the object that both users and valets will interact with

## The booking object

> A sample response for a booking object:

```json
[
    {
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": "7e1d0e574a8ba27f945a61eF",
        "valet": "7e1d0e574a8ba27f945a61eF",
        "status": 0,
        "airport": "MSP",
        "flight": "DL5899",
        "car": {"make": "Toyota", "model":"Camry", "plate":"txp120", "color":"black"},
        "dropOffAt": "2020-01-14T00:42:16.240Z",
        "pickUpAt": "2020-01-14T00:42:16.240Z",
        "droppedOffAt": "2020-01-14T00:42:16.240Z",
        "pickedUpAt": "2020-01-14T00:42:16.240Z",
        "total": 40.00,
        "__v": 0,
    }
]
```
### Attributes

    field      | description
--------- | -----------
`_id` String | Unique identifier for the booking object.
`user` String | The user object that creates the booking
`valet` String | The valet object that is assigned to the booking
`status` Int | The status of the booking (pending, confirmed, cancelled)
`airport` String | The departure airport
`flight` String | The airline departure flight number
`car` {String: String} | The car the user listed under booking
`dropOffAt` Date | The time the user expects to dropp off the vehicle with the valet
`pickupAt` Date | The time the user expects to pick up his/her car from the valet 
`droppedOffAt` Date | The actual time the user drops off vehicle with valet
`pickedUpAt` Date | The actuall time the user picked up his/her vehicle from the valet
`total` Int | The total cost of the booking


 






## Create a booking

> `POST /v1/bookings`

```javascript
let bookingController = require('...controllers/booking-controller')

 app.route('/api/v1/bookings/')
        .post(bookingController.createBooking)
```

> response

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "status": 0,
        "airport": "MSP",
        "flight": "DL5899",
        "car": {"make": "Toyota", "model":"Camry", "plate":"txp120", "color":"black"},
        "dropOffAt": "2020-01-14T00:42:16.240Z",
        "pickUpAt": "2020-01-14T00:42:16.240Z",
        "droppedOffAt": "2020-01-14T00:42:16.240Z",
        "pickedUpAt": "2020-01-14T00:42:16.240Z",
        "total": 40.00,
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

This endpoint creates a new booking in the database.

### Arguments

  field      | description
--------- | -----------
`user` String | The user object that created the booking.
`airport` String | The departure airport
`flight` String | The departure flight number
`car` {String: String} | The vehicle under the booking
`dropOffAt` String | The anicipated drop off time
`pickUpAt` String | The anicipated pickup time
`total` Int | The total charge for the service










## Retrieve a booking

> `GET /v1/bookings/:id`

```javascript
let bookingController = require('...controllers/booking-controller')

 app.route('/api/v1/bookings/:id')
        .get(bookingController.fetchBooking)
})
```

> response:

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "status": 0,
        "airport": "MSP",
        "flight": "DL5899",
        "car": {"make": "Toyota", "model":"Camry", "plate":"txp120", "color":"black"},
        "dropOffAt": "2020-01-14T00:42:16.240Z",
        "pickUpAt": "2020-01-14T00:42:16.240Z",
        "droppedOffAt": "2020-01-14T00:42:16.240Z",
        "pickedUpAt": "2020-01-14T00:42:16.240Z",
        "total": 40.00,
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

Retrieves the details of an existing booking. You need only supply the unique booking identifier that was returned upon valet creation.

### Arguements

`no arguments`

### Returns

Returns a booking object if a valid identifier was provided. When requesting the ID of a valet that has been deleted, a subset of the booking information will be returned, including a deleted property, which will be true.


## Update a booking

> `PUT /v1/bookings/:id`

```javascript
let bookingController = require('...controllers/booking-controller')

 app.route('/api/v1/valets/:id')
        .put(bookingController.updateBooking)
})
```

> response:

```json
{
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "status": 0,
        "airport": "MSP",
        "flight": "DL5899",
        "car": {"make": "Toyota", "model":"Camry", "plate":"txp120", "color":"black"},
        "dropOffAt": "2020-01-14T00:42:16.240Z",
        "pickUpAt": "2020-01-14T00:42:16.240Z",
        "droppedOffAt": "2020-01-14T00:42:16.240Z",
        "pickedUpAt": "2020-01-14T00:42:16.240Z",
        "total": 40.00,
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
```

Updates the specified booking by setting the values of the parameters passed. Any parameters not provided will be left unchanged

### Arguements

`Any argument listed in the object definition with an action argument` 

  field      | description
--------- | -----------
`claim`  | A valet claims a booking.
`cancel`  | The user cancels a booking.
`dropOff` | The user exchanges key to valet, valet drives off and parks the car
`pickup` String | The user grabs car from valet and drives off

### Returns

Returns the booking object if the update succeeded. Throws an error if update parameters are invalid (e.g. specifying an invalid coupon or an invalid source).


## Delete a booking

> `Delete /v1/bookings/:id`

```javascript
let bookingController = require('...controllers/booking-controller')

 app.route('/api/v1/bookings/:id')
        .delete(bookingController.deleteBooking)
})
```

> response:

```json
{
  "_id": "cus_GY90URwhYx9Oy5",
  "object": "booking",
  "deleted": true
}
```

Permanently deletes a booking. It cannot be undone. Also immediately cancels any active bookings on the booking.

### Arguements

`none`

### Returns

Returns an object with a deleted parameter on success. If the valet ID does not exist, this call throws an error.
Unlike other objects, deleted valets can still be retrieved through the API, in order to be able to track the history of valet while still removing their credit card details and preventing any further operations to be performed (such as adding a new bookings).



## List all bookings

> `GET /v1/bookings/`

```javascript
let BookingController = require('...controllers/booking-controller')

 app.route('/api/v1/bookings')
        .get(bookingController.fetchBookings)
})
```

> response:

```json
{
  "object": "list",
  "url": "/v1/bookings",
  "has_more": false,
  "data": [
   {
        "_id": "5e1d0e574a8ba27f945a61e0",
        "user": {
                "first_name": "Brittany",
                "last_name": "Klepfer",
                "phone": "6518724630",
                "deviceToken": "sdojfd0e574a8ba27f945a61e0",
        },
        "status": 0,
        "airport": "MSP",
        "flight": "DL5899",
        "car": {"make": "Toyota", "model":"Camry", "plate":"txp120", "color":"black"},
        "dropOffAt": "2020-01-14T00:42:16.240Z",
        "pickUpAt": "2020-01-14T00:42:16.240Z",
        "droppedOffAt": "2020-01-14T00:42:16.240Z",
        "pickedUpAt": "2020-01-14T00:42:16.240Z",
        "total": 40.00,
        "createdAt": "2020-01-14T00:41:59.740Z",
        "updatedAt": "2020-01-14T00:42:16.240Z",
        "__v": 0,
    }
  ]
```

Returns a list of your bookings. The valets are returned sorted by creation date, with the most recent user appearing first.

### Query Parameters

  field      | description
--------- | -----------
`userId` String | Filter bookings by userId
`valetId` String | Filter bookings by valetId
`date` Date | Filter bookings by date
`status` String| Filter bookings by status

### Returns

A object with a data property that contains an array of up to limit bookings, starting after booking starting_after. Passing an optional email will result in filtering to users with only that exact email address. Each entry in the array is a separate valet object. If no more customers are available, the resulting array will be empty. This request should never throw an error.



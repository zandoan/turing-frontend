# Turing Front-end


## Welcome
Welcome to the Turing Challenge. Here you'll find some examples to reach your goal. 

## Root Endpoint 
[https://backendapi.turing.com/docs](https://backendapi.turing.com/docs)

## Authentication
Just some endpoint required Authentication, you can check it in the documentation. 
The Customer login provide the Token to use in the other endpoints that required it.

Token's example: ```Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjdXN0b21lcl9pZCI6MTIsIm5hbWUiOiJFZGVyIFRhdmVpcmEiLCJyb2xlIjoiY3VzdG9tZXIiLCJpYXQiOjE1NTA3ODYyMjAsImV4cCI6MTU1MDg3MjYyMH0.QEGdry367EQNxBqzuUDCGJscWkq8YQwJdGBgV3hztR0```
 
The Token need to be in the header param **"user-key"**. Let's see an example below.

Example Using login Authentication (jQuery):
```javascript
$.ajax({ 
         url: "https://backendapi.turing.com/customer/login",
         data: {email: "CUSTOMER EMAIL", passsword: "CUSTOMER PASSWORD"},
         type: "POST",
         success: function(resp) { console.log(resp.responseText); },
         error: function(error) { console.log(error.responseText); }
});		
```

Response example:
```json
{
  "user": {
    "customer_id": 12,
    "name": "Eder Taveira",
    "email": "challenge@turing.com",
    "address_1": "",
    "address_2": "",
    "city": "",
    "region": "",
    "postal_code": "",
    "shipping_region_id": null,
    "day_phone": null,
    "eve_phone": null,
    "mob_phone": null
  },
  "accessToken": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjdXN0b21lcl9pZCI6MTIsIm5hbWUiOiJFZGVyIFRhdmVpcmEiLCJyb2xlIjoiY3VzdG9tZXIiLCJpYXQiOjE1NTA3ODYyMjAsImV4cCI6MTU1MDg3MjYyMH0.QEGdry367EQNxBqzuUDCGJscWkq8YQwJdGBgV3hztR0",
  "expires_in": "24h"
}
```

Example with header and token:
```javascript
$.ajax({ 
         url: "https://backendapi.turing.com/customer",
         headers: { 'user-key': 'Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjdXN0b21lcl9pZCI6MTIsIm5hbWUiOiJFZGVyIFRhdmVpcmEiLCJyb2xlIjoiY3VzdG9tZXIiLCJpYXQiOjE1NTA3ODYyMjAsImV4cCI6MTU1MDg3MjYyMH0.QEGdry367EQNxBqzuUDCGJscWkq8YQwJdGBgV3hztR0' },
         type: "GET",
         success: function(resp) { console.log(resp.responseText); },
         error: function(error) { console.log(error.responseText); }
});		
```

## Pagination
All params of pagination are not required.

The pagination can to have the query params below:

* **page** - Number of page. Default is "1".
* **limit** - Number of limit por page. (Check [the documentation](https://backendapi.turing.com/docs) to see what the default for each endpoint).

Examples: 

* https://backendapi.turing.com/categories?page=1&limit=20
* https://backendapi.turing.com/products?page=1
* https://backendapi.turing.com/products?limit=30

Some endpoints (shoppingcart and products) have a  no required param **"description_length"**.

Return of list with pagination:
```json
{
  "count": 40,
  "rows": [
    {
      "category_id": 1,
      "name": "French",
      "description": "The French have always had an eye for beauty. One look at the T-shirts below and you'll see that same appreciation has been applied abundantly to their postage stamps. Below are some of our most beautiful and colorful T-shirts, so browse away! And don't forget to go all the way to the bottom - you don't want to miss any of them!",
      "department_id": 1
    }
  ]
}
```

## Order

To sort some lists use the no required param **"order"**.

The format of param is as this REGEX: '/^([^\s]+),(DESC|ASC)$/'

Example: 

* https://backendapi.turing.com/categories?order=name|DESC
 
## Stripe Itegration

Do as the example in this [link](https://stripe.com/docs/stripe-js/elements/quickstart) using this stripe public key **pk_test_NcwpaplBCuTL6I0THD44heRe**

After that use the TOKEN created in the endpoint **"https://backendapi.turing.com/stripe/charge"**. 

## Errors

The error response has the following structure:

* **code** - Error's Code.
* **message** - Error's Message.
* **field** - Error's Field.

Example of Error:
```json
{"error":{"status":400,"code":"USR_05","message":"The email don't exists.","field":"email"}}
```


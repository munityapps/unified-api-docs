For your Ecommerce integrations, you can create orders.

You can send the paylod to this endpoint:
```txt
https://api.munityapps.com/v1/customers/{CUTOMER_ID}/ecommerce-order/
```
Payload:
```json
{
    "integration_id":"The id of the integration",
    "products":[
        //
        {
            "id":"the product's id", 
            "quantity":"the quantity bought", 
            "variation":"Optional: the variation of the product"
        }
        //
    ],
    "customer":{
        "firstname":"The customer's first name",
        "lastname":"The customer's last name",
        "email":"The customer's email"
    },
    "address":{
        "address1":"customer's Address",
        "address2":"",
        "country":"",
        "city":"",
        "postcode":""
    }
}
```
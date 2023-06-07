# Get acces to your customer data

## API : Get data through our API

To communicate with API you need an API Key that you can manage on munity unified API website.

You can find your api keys in [your security page](https://app.munityapps.com/security).

![api_cert](./assets/api_cert.png)

This api key will be used on the Authorization header:

    Authorization: Api-Key <YOUR-API-KEY>

Exemple with CURL :

    curl -X GET 'https://api.munityapps.com/v1/customers/f87cc67d-b594-4407-a90d-b26cfdae8f14/pm-projects/' -H 'Authorization: Api-Key REM0aW39.NfO0123456789CNeHpF29wo'

You can access to our swagger to read all endpoint, how to implement it and what format are all responses :

[Munity Unified API Swagger](https://app.swaggerhub.com/apis-docs/dbyzero/munity-unified_api)

## WEBHOOK : Getting alert on your customer data

Munity can keep you updated for all your customer. Provide one endpoints and all your user data flow will be send to you.

You can add a webhook url here : [your security page](https://app.munityapps.com/security).

### integration_new_data_model

Payload :
```
payload={
    "id": self.id, // <- the integration id from where model is comming from
    "resource_id": id, // <- the new id for the resource
    "type": modal_name, // <- the kind of resource, it depends on your data mapping
},
```

### integration_updated_data_model

Payload :
```
payload={
    "id": self.id, // <- the integration id from where model is comming from
    "resource_id": id, // <- the new id for the resource
    "type": modal_name, // <- the kind of resource, it depends on your data mapping
    "diff": diff, // <- A json that show differences from old and new model
    "data": data, // <- Full data of the updated data model
},
```

### integration_deleted_data_model

Payload :
```
payload={
    "id": self.id, // <- the integration id from where model is deleted from
    "resource_id": id, // <- the id for the resource deleted
    "type": modal_name, // <- the kind of resource, it depends on your data mapping
},
```

## DATABASE : Get data directly inside database

You can also directly connect to your customer data here : [Customer page](https://app.munityapps.com/customers).

And click on `Show DB credentials`.

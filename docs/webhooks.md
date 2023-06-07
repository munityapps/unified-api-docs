You can add a webhook url here : [your security page](https://app.munityapps.com/security).

On your endpoint we will send following webhooks.

All webhook as following payload :

```
{
    workspace_id='XXX' // <- your workspace id 
    customer_id='XXX' // <- your customer id provided durring to connect function 
    event="event_type_name" // <- there few different kind of event all listed below
    state="integration_state", // <- your integration state provided durring to connect function, usefull to know which connection has been correctly made. Prevent creation collision. 
    payload={"id": self.id}, // <- a payload dedicated to this event
}
```

## integration_new_data_model

Payload :
```
payload={
    "id": self.id, // <- the integration id from where model is comming from
    "resource_id": id, // <- the new id for the resource
    "type": modal_name, // <- the kind of resource, it depends on your data mapping
},
```

## integration_updated_data_model

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

## integration_deleted_data_model

Payload :
```
payload={
    "id": self.id, // <- the integration id from where model is deleted from
    "resource_id": id, // <- the id for the resource deleted
    "type": modal_name, // <- the kind of resource, it depends on your data mapping
},
```

## integration_installed

Payload :
```
payload={
    "id": integration.id, // <- the integration id from where model is deleted from
    "connector_type": integration.connector_type, // <- connector type of the ingration, can be usefull
    "metadata": integration.metadata, // <- Some metadata of the ingration can be usefull to keep it saved on your side 
    "state": integration.external_state, <- State provided at integration creation
},
```

## integration_import_done

Payload :
```
payload={
    'id':integration.id, // <- the integration id of the integration that just finished
    'connector_type':integration.connector_type, // <- connector type of the ingration, can be usefull
},
```

## integration_cannot_refresh_oauth_token

Payload :
```
    payload={
        "id": self.id, // <- where id is the integration id fixed
        "error": err // <- error message trigged by oauth refresh
    },
```

## integration_oauth_token_fixed

Payload :
```
    payload={"id": self.id}, // <- where id is the integration id fixed
```

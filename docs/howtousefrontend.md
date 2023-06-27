# How to use on frontend : get your customer data access

Since you want you customer data, you need that your customer grant access.

We take care of the security so you don't have to store these credentials and we also manage the [Oauth2 dance](https://en.wikipedia.org/wiki/OAuth) for you.

## Install frontend library

```
npm install @munityapps/sdk-frontend
```

## Use frontend library to connect users

Javascript :
```javascript
import { connect } from @munityapps/sdk-frontend

const promise = connect( connector, secret, callback)
```

Typescript:
```javacript
import { connect } from @munityapps/sdk-frontend

const promise:Promise<boolean> = connect(
  connector: string,
  secret: string,
  cb: ((data: { status: string; message: any}):void),
  config: { [key: string]: string } = {}
)
```

### - `connector` :
It's a slug referring your connector (ex: `jira`).
### - `secret` : 

Here a snippet to generate your `secret` in python:

```python
import jwt

# Certificate provided by Munity
certificate = "-----BEGIN PRIVATE KEY-----[...]-----END PRIVATE KEY-----\n"

secret = jwt.encode({"customer_id": "customer_1234","workspace_id": "11111111-2222-3333-aaaa-eeeeeeeeeeee", "name": "optional name"}, certificate, algorithm="RS256")

```

You can find your certificate in [your security page](https://app.munityapps.com/security).

![api_cert](./assets/api_cert.png)

It's a JWT encoded with RS256 using your certificate provided by Munity. Your cetificate can be find here : [admin page](https://app.munityapps.com/admin). You need to provide `workspace_id` and `customer_id` and optionaly the name of the connector in a json format. 
    - `workspace_id` is the ID of your workspace on Munity, you can find it here : [admin page](https://app.munityapps.com/admin).
    - `customer_id` is your internal id that you will use to find back the customer. It can contains letter and numbers only.
    - *(optional)* `name`: a name to show the integration on your frontend for UI purpose.

### - `callback` *(optional)* 
The callback will be triggered when the connected integration sends a new event. The first parameter of the callback is a payload, and its value is:
```
    { 
        "type":  //<-- can be 'error', 'READY' or 'INSTALLED'.
        "message":  //<-- associated message if needed, useful for errors.
    }
``` 

### - `promise` return by connect function

The function will return a Promise<boolean>, indicating that it will resolve with a boolean value (true) when the integration is ready, or reject with an error object if any error occurs.

To handle the promise, you can use methods like .then() and .catch() or async/await syntax.

Here's an example using .then() and .catch():

```javascript
connect(connectorValue, secretValue, cbValue, configValue)
  .then((result) => {
    // Integration is ready, handle the success case
    console.log('Integration is ready:', result);
  })
  .catch((error) => {
    // Handle the error case
    console.error('Error occurred:', error);
  });
```

You can also use async/await syntax to handle the promise:

```javascript
async function handleConnect() {
  try {
    const result = await connect(connectorValue, secretValue, cbValue, configValue);
    // Integration is ready, handle the success case
    console.log('Integration is ready:', result);
  } catch (error) {
    // Handle the error case
    console.error('Error occurred:', error);
  }
}

handleConnect();
```

### How to restore a broken integration (renew credentials)

There is an other fields that you can add in secret generation to specify that you want to update an integration credentials.

```
secret = jwt.encode({"customer_id": "customer_1234","workspace_id": "11111111-2222-3333-aaaa-eeeeeeeeeeee", "integration_id": "old_uuid"}, certificate, algorithm="RS256")
```
# Use frontend SDK

Since you desire access to your customer's company data, it's necessary for your customer to grant permission.

We handle security measures, eliminating the need for you to store these credentials. Additionally, we manage the OAuth2 authentication process on your behalf.

## Install frontend library

```
npm install @munityapps/sdk-frontend
```

## Use frontend library to connect users

To request credentials from your users, you should call the connect function provided by the Munity SDK.

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

The parameters are detailed below.

### - `connector` :

> Please specify the connector's name (e.g., jira) to refer to your particular connector.

### - `secret` : 

> To generate your secret key, utilize the Python snippet provided below. This script uses the jwt library to encode a JSON Web Token (JWT) with the RS256 algorithm, leveraging a certificate provided by Munity.
> 
```python
import jwt

# Munity-provided certificate
certificate = "-----BEGIN PRIVATE KEY-----[...]-----END PRIVATE KEY-----\n"

# Generate the secret
secret = jwt.encode({
    "customer_id": "customer_1234",
    "workspace_id": "11111111-2222-3333-aaaa-eeeeeeeeeeee",
    "name": "optional name"  # This field is optional
}, certificate, algorithm="RS256")
```
> 
> You will find the necessary certificate within your workspace settings, as illustrated below:
> 
> ![api_cert](./assets/api_cert.png)
> 
> This secret key is a JWT, encoded using the RS256 algorithm and your Munity-provided certificate. You can retrieve your certificate from the admin page. When encoding your JWT, you need to include the workspace_id and customer_id. Optionally, you can also specify a name for the connector. The details for these parameters are as follows:
> 
> - workspace_id: This is the unique identifier for your workspace on Munity. You can locate this ID on the admin page.
> - customer_id: This identifier is used internally to reference the customer. It should only contain letters and numbers.
> - name (optional): This parameter allows you to specify a name for the integration, which can be useful for display purposes on your frontend UI.
















### - `callback` *(optional)* 
> The callback function is optionally invoked when the connected integration emits a new event. The function receives a payload as its first parameter, structured as follows:
```
    { 
        "type":  //<-- can be 'error', 'READY' or 'IMPORT_DONE'.
        "message":  //<-- associated message if needed, useful for errors.
    }
``` 

### - `promise` return by connect function

> The connect function returns a Promise<boolean>. This promise resolves with a boolean value (true) once the integration is successfully ready, or it rejects with an error object in case of failure.
> 
> To manage the promise, you can employ .then() and .catch() methods or the async/await syntax.
> 
> Using .then() and .catch():

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

> Handling with async/await Syntax:

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

### Renewing Credentials for a Broken Integration

To update the credentials of an existing integration, you can include an additional field in your secret generation process. This field, integration_id, should contain the UUID of the integration you wish to update:

````js
secret = jwt.encode({
    "customer_id": "customer_1234",
    "workspace_id": "11111111-2222-3333-aaaa-eeeeeeeeeeee",
    "integration_id": "old_uuid"  // Specify the integration to update
}, certificate, algorithm="RS256")
````

This approach allows for seamless updating of integration credentials, ensuring continuous operation without manual intervention.
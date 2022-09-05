# How to use on frontend : get your customer data access

Since you want you customer data, you need that your customer grant access.

We take care of the security so you don't have to store these credentials and we also manage the [Oauth2 dance](https://en.wikipedia.org/wiki/OAuth) for you.

## Install frontend library

```
npm install @munityapps/frontend
```

## Use frontend library to connect users


```javascript
import { connect } from @munityapps/frontend

connect('connectorType', secret)
```

- `connectorType` : is a slug referring your connector (ex: `jira`).
- `secret` : a JWT encoded with RS256 using your certificate provided by Munity. Your cetificate can be find here : [admin page](https://app.munityapps.com/admin). You need to provide `workspace_id` and `customer_id` and optionaly the name of the connector in a json format. 
    - `workspace_id` is the ID of your workspace on Munity, you can find it here : [admin page](https://app.munityapps.com/admin).
    - `customer_id` is your internal id that you will use to find back the customer. It can contains letter and numbers only.
    - *(optional)* `name`: a name to show the integration on your frontend for UI purpose.

Here a snippet to generate your `secret` in python:

```python
import jwt

# Certificate provided by Munity
certificate = "-----BEGIN PRIVATE KEY-----[...]-----END PRIVATE KEY-----\n"

secret = jwt.encode({"customer_id": "customer_1234","workspace_id": "11111111-2222-3333-aaaa-eeeeeeeeeeee", "name": "optional name"}, certificate, algorithm="RS256")

```

You can find your certificate in [your user admin page](https://app.munityapps.com/admin).

![api_cert](./assets/api_cert.png)


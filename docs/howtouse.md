# How to use

## Connect customer

Since you want you customer data, you need your customer authorization.

We take care of the security so you don't have to store these credentials and we also manage the [Oauth2 dance](https://en.wikipedia.org/wiki/OAuth) for you.

The unique endpoint used to provide your customer authorization is `https://api.munityapps.com/v1/credentials/jira/register?secret={SECRET}` (for JIRA).

All you have to do is open in the browser our user manager to get credentials. For exemple, you can create an HTML button with the secret generate as bellow :

```
<button onclick="window.open('https://api.munityapps.com/v1/credentials/jira/register?secret={SECRET}','_blank')"> Connect JIRA </button>

```

Your **`SECRET`** is a **JWT payload encoded in RS256** using your certificate provided by munity Unified API.

For exemple you can get credentials of your customer `customer_1234` with this following snippet in python :

```python
import jwt

# Certificate provided by Munity
certificate = "-----BEGIN PRIVATE KEY-----[...]-----END PRIVATE KEY-----\n"

SECRET = jwt.encode({"customer_id": "customer_1234","workspace_id": "11111111-2222-3333-aaaa-eeeeeeeeeeee"}, certificate, algorithm="RS256")

```

You can find your certificate in [your user admin page](https://app.munityapps.com/admin).

![api_cert](./assets/api_cert.png)


## Unified API Endpoints

To communicate with API you need an API Key that you can manage on munity unified API website.

This api key will be used on the Authorization header:

    Authorization: X-Api-Key <YOUR-API-KEY>

Exemple with CURL :

    curl -X GET 'https://api.munityapps.com/v1/customers/f87cc67d-b594-4407-a90d-b26cfdae8f14/pm-projects/' -H 'Authorization: X-Api-Key REM0aW39.NfO0123456789CNeHpF29wo'

You can access to our swagger to read all endpoint, how to implement it and what format are all responses :

[Munity Unified API Swagger](https://app.swaggerhub.com/apis-docs/dbyzero/munity-unified_api/1.0.0)



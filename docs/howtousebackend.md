# Access your customer data

## API: Retrieve Data via Our API

To interact with our API, you'll need an API Key, which can be managed on the Munity Unified API website.

You can find your API keys on workspace settings.

[API Manage](./assets/api.png)

This API key should be included in the Authorization header:

```
Authorization: Api-Key <YOUR-API-KEY>
```

Example using CURL:

```
curl -X GET 'https://api.munityapps.com/v1/customers/f87cc67d-b594-4407-a90d-b26cfdae8f14/pm-projects/' -H 'Authorization: Api-Key YOUR_ACTUAL_API_KEY_HERE'
```

Access our Swagger documentation to view all endpoints, implementation methods, and response formats:

[Munity Unified API Swagger Documentation](https://app.swaggerhub.com/apis-docs/dbyzero/munity-unified_api)


## WEBHOOK : Getting alert on your customer data

Munity can keep you updated for all your customer. Provide one endpoints and all your user data flow will be send to you.

You can add a webhook url in your marketplace settings :

Webhook list are available here : [Webhook Reference](/webhooks)


## DATABASE : Get data directly inside database

You can also directly connect to your customer's company data here by connecting to there database. You can have access to there DB credential in your marketplace.
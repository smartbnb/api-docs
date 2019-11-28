# Authentication

Smartbnb protect our API endpoints using [OAuth 2.0](https://tools.ietf.org/html/rfc6749)'s Client Credentials flow. In order to use the Smartbnb API, you will need a Client ID and Secret. These should have been provided to you upon registering to use the API.


<!-- theme: warning -->
> #### 👀 Watch out!
> 
> Your Client ID and Secret are effectively credentials to access your Smartbnb account and connected Airbnb or HomeAway (VRBO) accounts, and therefore should be kept secure at all times - just like passwords.


## Token Exchange

Once you have your credentials, your application should request an access token from our authorization server, extract a JSON Web Token (JWT) from the response, and send that token in the headers of further API requests. The request to do so looks like the following:

```bash
curl --request POST \
  --url https://auth.smartbnb.io/oauth/token \
  --header 'Content-Type: application/json' \
  --data '{
	"client_id": "<YOUR CLIENT ID>",
	"client_secret": "<YOUR CLIENT SECRET>",
	"audience":"api.smartbnb.io",
	"grant_type":"client_credentials"
}'
```

The response to this request will be a JSON object containing an `access_token`. This should be sent in the `Authorization` header of subsequent requests as follows:

```http
Authorization: Bearer <YOUR ACCESS TOKEN>
```

Access tokens have limited lifetimes. Once an access token has expired, you will start to receive `401 Unauthenticated` responses from our API. At this point, a new access token must be requested.

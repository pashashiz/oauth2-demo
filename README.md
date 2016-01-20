### Grant AUTHORIZATION CODE (for any application)

Call OAuth2 Server (use user@password):
```
http://localhost:8000/oauth-server/oauth/authorize?response_type=code&client_id=acme&redirect_uri=http://example.com
```
The result is going to by like:
```
http://example.com/?code=ARx433
```

Get ticket by authorization code (ARx433) from redirected url:
```
curl acme:acmesecret@localhost:8000/oauth-server/oauth/token \
-d grant_type=authorization_code \
-d client_id=acme \
-d redirect_uri=http://example.com \
-d code=ARx433
```
The response should be the following:
```json
{
    "access_token":"de5e5996-917c-41dc-920d-94f1172fb8e3",
    "token_type":"bearer",
    "refresh_token":"ece025fb-3dd8-4f4d-b683-87902a18463b",
    "expires_in":43199,
    "scope":"openid"
}
```

### Grant IMPLICIT (For front-end, desktop and mobile application)

Call OAuth2 Server (use user@password):
```
http://localhost:8000/oauth-server/oauth/authorize?response_type=token&client_id=acme&redirect_uri=http://example.com
```
The result is going to by like:
```
http://example.com/#access_token=f263c3b9-32f2-4724-9f36-e25237bffd75&token_type=bearer&expires_in=43199&scope=openid
```

### Grant PASSWORD (for native applications with high level of trust)

Call OAuth2 Server:
```
curl acme:acmesecret@localhost:8000/oauth-server/oauth/token \
-d grant_type=password \
-d username=user \
-d password=password
```

### Example of using token

Call Resource Server directly with access token (1e944000-443e-4d53-bbc7-2c582eb20210"):
```
curl -H "Authorization: Bearer 1e944000-443e-4d53-bbc7-2c582eb20210" localhost:8010/resource-server
```
And the successful response:
```
{
    "id":"b6835c89-a23f-4d62-8569-74181333b3f2",
    "content":"Hello World"
}

```

Get resource through Gateway with access token (de5e5996-917c-41dc-920d-94f1172fb8e3):
```
curl -H "Authorization: Bearer de5e5996-917c-41dc-920d-94f1172fb8e3" localhost:8080/gateway/resource-server
```
And the successful response:
```
{
    "id":"b6835c89-a23f-4d62-8569-74181333b3f2",
    "content":"Hello World"
}

```

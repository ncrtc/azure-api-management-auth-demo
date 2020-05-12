# azure-api-management-auth-demo

## 1. Create App Registration for API


## 2. Create App Registration for Client


## 3. Get token for Client App

``` HTTP
POST /{tenant}/oauth2/v2.0/token HTTP/1.1           //Line breaks for clarity
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

client_id={clientAppID}
&scope=api://{apiAppID}/.default
&client_secret={clientAppSeceret}
&grant_type=client_credentials
```

## 4. Add JWT validation in API Management

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud" match="any">
            <value>api://{apiAppID}</value>
            <value>{apiAppID}</value>
        </claim>
        <claim name="appid" match="any">
            <value>{clientAppID}</value>
        </claim>
    </required-claims>
</validate-jwt>
```

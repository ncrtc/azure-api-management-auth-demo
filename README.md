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

Inspect the token with http://aka.ms/jwt:

``` JSON
JWT valid from 05-12-2020 17:14:28 to 05-12-2020 18:19:28

CLAIMS: 
[
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": null,
    "m_type": "aud",
    "m_value": "api://c8c86576-bffa-4db5-bf90-bba8ffa4b832",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": null,
    "m_type": "iss",
    "m_value": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": [
      {
        "Key": "http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/json_type",
        "Value": "System.Int32"
      }
    ],
    "m_type": "iat",
    "m_value": "1589303668",
    "m_valueType": "JSON"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": [
      {
        "Key": "http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/json_type",
        "Value": "System.Int32"
      }
    ],
    "m_type": "nbf",
    "m_value": "1589303668",
    "m_valueType": "JSON"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": [
      {
        "Key": "http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/json_type",
        "Value": "System.Int32"
      }
    ],
    "m_type": "exp",
    "m_value": "1589307568",
    "m_valueType": "JSON"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": null,
    "m_type": "aio",
    "m_value": "42dgYFjhs6riwK2a6YwZCSXMbzJ0AA==",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": null,
    "m_type": "appid",
    "m_value": "f3d44fcd-8d03-4940-810c-92c12f544138",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": null,
    "m_type": "appidacr",
    "m_value": "1",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": [
      {
        "Key": "http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/ShortTypeName",
        "Value": "idp"
      }
    ],
    "m_type": "http://schemas.microsoft.com/identity/claims/identityprovider",
    "m_value": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": [
      {
        "Key": "http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/ShortTypeName",
        "Value": "oid"
      }
    ],
    "m_type": "http://schemas.microsoft.com/identity/claims/objectidentifier",
    "m_value": "abc63196-7699-450a-bcae-a229db5d5e27",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": [
      {
        "Key": "http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/ShortTypeName",
        "Value": "sub"
      }
    ],
    "m_type": "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier",
    "m_value": "abc63196-7699-450a-bcae-a229db5d5e27",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": [
      {
        "Key": "http://schemas.xmlsoap.org/ws/2005/05/identity/claimproperties/ShortTypeName",
        "Value": "tid"
      }
    ],
    "m_type": "http://schemas.microsoft.com/identity/claims/tenantid",
    "m_value": "2e433799-9cb5-4258-956b-1253c4de44dc",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": null,
    "m_type": "uti",
    "m_value": "Nbuhsed840yjksE5PFHgAA",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  },
  {
    "m_issuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_originalIssuer": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
    "m_properties": null,
    "m_type": "ver",
    "m_value": "1.0",
    "m_valueType": "http://www.w3.org/2001/XMLSchema#string"
  }
]
```

## 4. Add JWT validation in API Management

Using the information from the client token add JWT validation rule to API Managment

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

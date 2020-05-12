# Azure API Management Authentication 

## Client Credential Flow for application to application scenarios

### 1. Create App Registration for API

An app registrations is needed to representing the API. The default settings can be used with no need for a redirect URI:

https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app

Additionally, set the App ID URI:

1. On the API Proxy app registration, navigate to Expose an API 
2. Then, click on Application ID URI - Set, and leave the default value, which should be **api://{clientId}**
3. Click on **Save**

### 2. Create App Registration for Client

An app registrations is needed to representing the API. The default settings can be used with no need for a redirect URI:

https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app

Now, we need to create a secret for the app registration representing the API client:

1. Navigate to the API client app registration.
2. Navigate to Certificate & Secrets, and add a secret.
3. Take a note of the generated secret. 

### 3. Get token for Client App

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

**Content**
``` JSON
{
  "typ": "JWT",
  "alg": "RS256",
  "x5t": "CtTuhMJmD5M7DLdzD2v2x3QKSRY",
  "kid": "CtTuhMJmD5M7DLdzD2v2x3QKSRY"
} 
{
  "aud": "api://c8c86576-bffa-4db5-bf90-bba8ffa4b832",
  "iss": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
  "iat": 1589303668,
  "nbf": 1589303668,
  "exp": 1589307568,
  "aio": "42dgYFjhs6riwK2a6YwZCSXMbzJ0AA==",
  "appid": "f3d44fcd-8d03-4940-810c-92c12f544138",
  "appidacr": "1",
  "idp": "https://sts.windows.net/2e433799-9cb5-4258-956b-1253c4de44dc/",
  "oid": "abc63196-7699-450a-bcae-a229db5d5e27",
  "sub": "abc63196-7699-450a-bcae-a229db5d5e27",
  "tid": "2e433799-9cb5-4258-956b-1253c4de44dc",
  "uti": "Nbuhsed840yjksE5PFHgAA",
  "ver": "1.0"
} 
pN-ifuHaA5dMOaqEqk8i9orl4D_KdxTrKMbFOwYsg7MSz2zRmBqed_UJWGqr5RPuFEh-MRIsLkg_9GCSqKcxxIbJddHnU0NiPihnVIl3dup1q5BN03SL__N4kc6GCfWtjPusH2qoMyl_R8sqyUt-3zjnJfx5SoHNwDWkWvtKiLtFWPsTZVw3VQYxP5M2IqZJnk8XBaJxMv4h149gh273nTrM7Tuj2YrXY0DX9nd21v7HL9v3TRdY8DPKgtp_BWdVP9cDp8zb-PfDV6uwL4-9l6Nmz8JVXucDgbl2eFA_x3Hww_khxer_8WXhDwXwKVA4Vdx37gMmbWQxIpbnL-7ImQ
```
**Claims**
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

### 4. Add JWT validation in API Management

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

## References
- https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-protect-backend-with-aad
- https://pacodelacruz.io/2019/07/09/oauth2-client-credentials-flow-on-azure-api-management
- https://docs.microsoft.com/en-us/azure/api-management/api-management-access-restriction-policies#ValidateJWT

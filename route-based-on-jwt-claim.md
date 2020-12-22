
## Sample Policy for routing based on JWT claim.

Using the information from the client token add JWT validation rule to API Managment

```xml

<policies>
    <inbound>
        <base />
        <validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
            <openid-config url="https://login.microsoftonline.com/{tenant}/.well-known/openid-configuration" />
            <required-claims>
                <claim name="aud" match="any">
                    <value>api://{apiAppID}</value>
                    <value>{apiAppID}</value>
                </claim>
                <claim name="appid" match="any">
                    <value>{clientAppID1}</value>
                    <value>{clientAppID2}</value>
                </claim>
            </required-claims>
        </validate-jwt>
        <set-variable name="azureAppId" value="@(context.Request.Headers["Authorization"].First().Split(' ')[1].AsJwt()?.Claims["appid"].FirstOrDefault())" />
        <choose>
            <when condition="@(context.Variables.GetValueOrDefault<string>("azureAppId").Equals("{clientAppID1}"))">
                <set-backend-service base-url="https://rutzsco-demo-api-management-ingest-api2.azurewebsites.net/api/" />
                <set-header name="x-functions-key" exists-action="append">
                    <value>HroLSbFy2LU/44JxFPkXjC4yqQwpUqrEIty8R/HiLaKpDLq9GZa0DQ==</value>
                </set-header>
            </when>
            <otherwise>
                <set-backend-service base-url="https://rutzsco-demo-api-management-ingest-api.azurewebsites.net/api/" />
                <set-header name="x-functions-key" exists-action="append">
                    <value>CfmOdpmooPob19DO49Tb4E1PgjJ9nv0QMMdBxkR5Uyvxuc8qViN7sQ==</value>
                </set-header>
            </otherwise>
        </choose>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
    <on-error>
        <base />
    </on-error>
</policies>

```

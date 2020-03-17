# **Integrator Authentication:**

In order for Integrators to be able to use MobilePay APIs, first they'll have to obtain an access token from the Integrator Authentication service. 

## **Environments:**

 - SandBox: [https://api.sandbox.mobilepay.dk](https://api.sandbox.mobilepay.dk/)[/integrator-authentication](https://api.mobilepay.dk/integrator-authentication)
 - Production: [https://api.mobilepay.dk/integrator-authentication](https://api.mobilepay.dk/integrator-authentication)

### **Client Credentials:**
The Integrator Authentication solution is based on the OpenID/OAuth 2.0 specification. Currently, the only flow supported is the Client Credentials grant type:

[https://tools.ietf.org/html/rfc6749#section-4.4](https://tools.ietf.org/html/rfc6749#section-4.4)

The OpenID Connect protocol is a simple identity layer on top of the OAuth 2.0 protocol.

### **Endpoints:**

#### HTTP GET: **`/integrator-authentication/.well-known/openid-configuration:`**

The discovery endpoint, also known as the "well-known endpoint" is a set of OpenID Connect properties, used by clients integrating against a OpenID authentication provider. The documents describes which claims, scopes, grant types and endpoints are to be used upon authentication.

Headers:

X-IBM-Client-Id: Client_Id supplied upon certification.

Example of response body from SandProd environment:


```
{
    "issuer": "https://api.mobilepay.dk/integrator-authentication",
    "jwks_uri": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/.well-known/openid-configuration/jwks",
    "authorization_endpoint": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/authorize",
    "token_endpoint": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/token",
    "userinfo_endpoint": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/userinfo",
    "end_session_endpoint": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/endsession",
    "check_session_iframe": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/checksession",
    "revocation_endpoint": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/revocation",
    "introspection_endpoint": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/introspect",
    "device_authorization_endpoint": "http://sandprod-az3-front-ext-rest-integrator-auth.ext.mobilepay.dk/integrator-authentication-restapi/connect/deviceauthorization",
    "frontchannel_logout_supported": true,
    "frontchannel_logout_session_supported": true,
    "backchannel_logout_supported": true,
    "backchannel_logout_session_supported": true,
    "scopes_supported": [
        "integrator_scope",
        "offline_access"
    ],
    "claims_supported": [],
    "grant_types_supported": [
        "authorization_code",
        "client_credentials",
        "refresh_token",
        "implicit",
        "urn:ietf:params:oauth:grant-type:device_code"
    ],
    "response_types_supported": [
        "code",
        "token",
        "id_token",
        "id_token token",
        "code id_token",
        "code token",
        "code id_token token"
    ],
    "response_modes_supported": [
        "form_post",
        "query",
        "fragment"
    ],
    "token_endpoint_auth_methods_supported": [
        "client_secret_basic",
        "client_secret_post"
    ],
    "id_token_signing_alg_values_supported": [
        "RS256"
    ],
    "subject_types_supported": [
        "public"
    ],
    "code_challenge_methods_supported": [
        "plain",
        "S256"
    ],
    "request_parameter_supported": true
}
 
```


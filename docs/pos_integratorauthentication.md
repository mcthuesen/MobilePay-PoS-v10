# **Integrator Authentication:**

In order for Integrators to be able to use MobilePay APIs, first they'll have to obtain an access token from the Integrator Authentication service. 

## **Environments:**

 - SandBox: [https://api.sandbox.mobilepay.dk](https://api.sandbox.mobilepay.dk/)[/integrator-authentication](https://api.mobilepay.dk/integrator-authentication)
 - Production: [https://api.mobilepay.dk/integrator-authentication](https://api.mobilepay.dk/integrator-authentication)

### **Client Credentials:**
The Integrator Authentication solution is based on the OpenID/OAuth 2.0 specification. Currently, the only flow supported is the Client Credentials grant type:

[https://tools.ietf.org/html/rfc6749#section-4.4](https://tools.ietf.org/html/rfc6749#section-4.4)

The OpenID Connect protocol is a simple identity layer on top of the OAuth 2.0 protocol.

## **Endpoint description:**

When doing `POST`,  `Content-Type: application/json` HTTP header must be provided.


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

### <a name="statuscodes"></a>Expected status codes

You might encounter the following status codes :

1. `200 - OK`  
 

2. `401 - Unauthorized` , if the client is not authorized/authenticated through the API Gateway
 
 
cURL example:

```console 
curl --location --request GET 'https://api.sandbox.mobilepay.dk/integrator-authentication/.well-known/openid-configuration' \
--header 'X-IBM-Client-Id: {YOUR_CLIENT_ID}''
```


#### HTTP `GET`: _**`/integrator-authentication/.well-known/openid-configuration/jwks:`**_

A JSON Web Key (JWK) is a standard method for representing a cryptographic key using JSON. The spec can be found [here](https://tools.ietf.org/html/rfc7517)

The Integrator Authentication solutions signs all JWT access token with a private key. The public key can be obtained in the jwks endpoint to verify the authenticity of the access token.

Headers:

 - `X-Ibm-client-id` supplied upon certification.

Example of response body from SandProd environment:


```
{
    "keys": [
        {
            "kty": "RSA",
            "use": "sig",
            "kid": "A9A7ACCF1884D01D4AB0FFD1049124B74B1E8BAD",
            "x5t": "qaeszxiE0B1KsP_RBJEkt0sei60",
            "e": "AQAB",
            "n": "peYBOoky5YBl2O_SUCLUlzoc2rzoDqlYS8Tha9rmV0SaTlpRm41LK5dAOTFZSoZqQVcUKoSpGtyg2Kpjr5DdMhN59XzAALjVETeEuLbUjthDkzQWXCck3WytzHxiKrwP59MFFosP75k2xh-05WYaSTlrATesNXblj33DG7okv9wCZqidQUBVHyn7vscOk_mTigZMrsTxpclr5fdrtGVa-tHg_97k7YOdsyurjLCzT7IjX4ekyuOJnzNwoEc5I2cSpNSu0tpTlI_6SaTr8Y9hJvM8REUvruh0vJUSyyo2OfFlGQ5TKsGaaNYzJNwycxh5UIwY5v4reWRDxG8TZ-yRxQ",
            "x5c": [
                "MIIFIDCCAwigAwIBAgIFAMaFE1EwDQYJKoZIhvcNAQELBQAwgZgxEDAOBgNVBAMTB0RCR1JPT1QxCzAJBgNVBAYTAkRLMRMwEQYDVQQHEwpDb3BlbmhhZ2VuMRAwDgYDVQQIEwdEZW5tYXJrMRowGAYDVQQKExFEYW5za2UgQmFuayBHcm91cDEaMBgGA1UECxMRRGFuc2tlIEJhbmsgR3JvdXAxGDAWBgNVBAUTDzYxMTI2MjI4MTExMDAwMzAeFw0yMDAyMjQwMDAwMDBaFw0yMjAyMjQwMDAwMDBaMIG1MSwwKgYDVQQDEyNNb2JpbGVQYXkgSW50ZWdyYXRvciBBdXRoZW50aWNhdGlvbjELMAkGA1UEBhMCREsxEzARBgNVBAcTCkNvcGVuaGFnZW4xEDAOBgNVBAgTB0Rlbm1hcmsxGjAYBgNVBAoTEURhbnNrZSBCYW5rIEdyb3VwMRowGAYDVQQLExFEYW5za2UgQmFuayBHcm91cDEZMBcGA1UEBRMQNjExMjYyMjgzMDYxMDAwMTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKXmATqJMuWAZdjv0lAi1Jc6HNq86A6pWEvE4Wva5ldEmk5aUZuNSyuXQDkxWUqGakFXFCqEqRrcoNiqY6+Q3TITefV8wAC41RE3hLi21I7YQ5M0FlwnJN1srcx8Yiq8D+fTBRaLD++ZNsYftOVmGkk5awE3rDV25Y99wxu6JL/cAmaonUFAVR8p+77HDpP5k4oGTK7E8aXJa+X3a7RlWvrR4P/e5O2DnbMrq4yws0+yI1+HpMrjiZ8zcKBHOSNnEqTUrtLaU5SP+kmk6/GPYSbzPERFL67odLyVEssqNjnxZRkOUyrBmmjWMyTcMnMYeVCMGOb+K3lkQ8RvE2fskcUCAwEAAaNSMFAwHwYDVR0jBBgwFoAU61V/xZhpcCaqEN34Mo9XCeNAPzowHQYDVR0OBBYEFIIFlKd9KiBOtaU4DdKrOWXIxYk3MA4GA1UdDwEB/wQEAwIGwDANBgkqhkiG9w0BAQsFAAOCAgEAdNd+N9b/He3X/vNCBv1gErfKGANCmWRWmDIJ8nxx/zOOEM6/699qdHobS0kq5I5N9LFalf2m+7HJml2x0K0zXtYQiyPIqXhNjmV+wA0xCJwoUZSg5zBcMTLPXGpA3tm6sit7VNIGUwaJO1AScfyXJnoFKARQjBAx4u/OCL6fiCY21UN/w6Kuw2MO7KX4ZaYSf4+zg84yWwtiw+PUvVr3Unh5AUtxABfs4IXa/kPwSY0B39BunhOl5vAUefPWFaF1xnhz/TMnlh8Eah2gGbI8Ylw5sf1S+zd2y7Td4xfldms74wP8zNv+2oUpqidqhs/vBBD9gz3wSp/AvDMqdd0LBK/U6cHFur0Jtpgd9wX8Git5VVTgMBi6oAbTNouqirxm28qteunaUZZmReToSV2HMD8LZO+V3UYstsGienLQVCpXz6cIOpM2mLAZrXfAgbo/GEbocp4M7qTHipcJkQLFNKEYAr1ijwVwi8jEgfTtWnus54dRImdzVo1YVX1oTNRmqlNGUOuZfZC0lckXJny4fcFookB+hUlk2HqPcZ00/ytVh1c4wfXdOdCokVlxW8GLzsB1iopV4B5a1tPs41ZpDTy936CmQa44Emd2Edclra8h0PwVaGI5p9WXxPyxdK0uk/xc+aSLQpvlJO8To9kUNpVH7uJMmbc3wWR2NE9Y9Ss="
            ],
            "alg": "RS256"
        }
    ]
}
 
```

### Expected status codes

You might encounter the following status codes :

1. `200 - OK`  
 

2. `401 - Unauthorized` , if the client is not authorized/authenticated through the API Gateway

    

cURL example:
Response body

```console 
curl --location --request GET 'https://api.sandbox.mobilepay.dk/integrator-authentication/.well-known/openid-configuration/jwks' \
--header 'X-IBM-Client-Id: {YOUR_CLIENT_ID}'
```


## `POST /connect/token`

Used when requesting an access token for an onboarded integrator client.

Headers:

 - **Content-Type**: x-www-urlencoded
 - **X-IBM-Client-Id**: Client_Id supplied upon certification.
 - **Authorization**: Basic 
 - **Client_Id**: 
 - **Client_Secret** as a base64 encoded string.

The Client_id and client_secret will be sent to the integrator in a closed zip file from developer@mobilepay.dk to integrators e-mail 

Parameter description:
|grant_type  | client_credentials |
|--|--|
| vat_number | VAT Number of the Merchant the integrator is integration on behalf. Will be applied to the JWT access token, if supplied. Can be left empty. (OPTIONAL). |


Example of response body from SandProd environment:

Response Body


```
{
    "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c",
    "expires_in": 3700,
    "token_type": "Bearer",
    "scope": "integrator_scope"
}
 
```

### Expected status codes

You might encounter the following status codes :

1. `200 - OK`  
 

2. `401 - Unauthorized` , if the client is not authorized/authenticated through the API Gateway
>    
    ```json
    {
        "error": "Unauthorized",
        "error_description": {
            "message": "xxxxxxxxxxxxxx",
            "error_type": "ClientError",
            "correlation_id": "f4b02597-32cc-420f-a468-942307e89a97"
        }
    }
    ```
 
 
    

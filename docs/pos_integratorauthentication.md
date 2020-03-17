# **Integrator Authentication:**

In order for Integrators to be able to use MobilePay APIs, first they'll have to obtain an access token from the Integrator Authentication service. 

## **Environments:**

SandBox: [https://api.sandbox.mobilepay.dk](https://api.sandbox.mobilepay.dk/)[/integrator-authentication](https://api.mobilepay.dk/integrator-authentication)

Production: [https://api.mobilepay.dk/integrator-authentication](https://api.mobilepay.dk/integrator-authentication)

### **Client Credentials:**

The Integrator Authentication solution is based on the OpenID/OAuth 2.0 specification. Currently, the only flow supported is the Client Credentials grant type:

[https://tools.ietf.org/html/rfc6749#section-4.4](https://tools.ietf.org/html/rfc6749#section-4.4)

The OpenID Connect protocol is a simple identity layer on top of the OAuth 2.0 protocol.

### **Endpoints:**

#### HTTP GET: **`/integrator-authentication/.well-known/openid-configuration:`**

The discovery endpoint, also known as the "well-known endpoint" is a set of OpenID Connect properties, used by clients integrating against a OpenID authentication provider. The documents describes which claims, scopes, grant types and endpoints are to be used upon authentication.

Headers:

X-IBM-Client-Id: Client_Id supplied upon certification.


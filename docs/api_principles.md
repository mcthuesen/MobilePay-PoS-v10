
# API Principles

This is a preliminary list of architectual principles.

**Backend has the truth**

An architectual principle in MobilePay PoS is that the Backend has the truth - that means in a situation where certainty is required, for instance is the payment approved, the app and clients will have to wait for confirmation from the backend.

**API versus Implementation**

The API does not describe the abstractions of the underlying backend OR client implementations - instead the API serves as the joint Interface for Backend and Frontend. The rammification for this is that BOTH frontend and backend can move independently from the API however they must always support the API specification and not only support perceived details of current implementations. ANY valid HTTP request must be handled appropiately by the backend and produce a useful informative HTTP response. Any valid HTTP response received in the client must be handled appropriately by the client.

**RESTful API**

The API is defined using the RESTful principles.

## <a name="security_model"></a> Security Model

**Communication security**

MobilePay PoS version 10 uses TLS for communication security and data integrity (secure channel between the client and the API 10 servers). The current TLS version used with the MobilePay PoS solution is 1.2 -  Version 1.3 is finalized and will be implemented within 1-2 years - therefore clients should be able to handle the switch to 1.3 on the fly or with minimal changes.

**Integrator Authorization**

The MobilePay API Gateway is ensuring the authentication of all PoS API request. 
In order to be granted access to the MobilePay PoS API each integrator/vendor will have to enroll their clients as a client (called App) in our API Gateway Developer Portal (see section below for more information about it).

Creating an app in MobilePay Developer portal will create a client Id that should be used in all calls the the MobilePay PoS API in the following way:


Example with a Curl request:

> --header 'X-IBM-Client-Id: 80e0075c-d0b5-4b74-a466-ecaca65234b0'

## <a name="client_identification"></a> Client Identification

# The Client Id is used by the MobilePay PoS backend to identify the client on the application level - the backend expects that different clients use different ClientId thereby requiring following the steps in the developer portal for each client.

Headers containing the Client Name and the Client Version are required. The Client Name is suitable name used for the client, preferable the name that the Integrator uses in their own communication, this way support communication between Merchant, Integrator and MobilePay uses the same name which should aid in removing confusion in the support sitiation. The Client version is a 3 dimensional number Major.Minor.Build - it is recommended to use the power of the Client Version Header, as this will be used by MobilePay to block versions of clients that are not certified and/or are misbehaving. An example of misbehavior would be spamming irrelevant HTTP calls that endanger fast response times for other clients.

* Major version represents major changes to the client version, perhaps representing breaking changes on the clients other interfaces or representing major changes communicated to merchants - A major change requires re-certification.
* Minor version represents minor changes to the client version, changes that introduces new features or a change in the way internal logic is handled, minor version changes are perhaps not communicated to merchants - a minor change requires re-certification.
* Build version represents a new build of the client, the include minor bug-fixes and changes of the lowest magnitude. A new build version does not require a re-certification

Certification requirements in regard to changes to Client Name and Client Version

* Changes in Client Name, Major version or Minor version requires a new Certification
* Changes in Build version does not requires a new Certification

Example with a Curl request:

````
--header 'X-MP-Client-Name: MobilePay Pos Client Reference Implementation'
--header 'X-MP-Client-Version: 2.1.1'
````

## <a name="api_responses"></a> API Responses

The MobilePay PoS V10 API uses HTTP 2XX status codes for successful requests, HTTP 4XX
status codes for failed requests that failed due to a client error and HTTP 5XX status 
codes for failed requests that failed due to a server error. An overview of error codes
used in the V10 API is given below.

| Status code               | Description                                                                               |
|---------------------------|-------------------------------------------------------------------------------------------|
| 200 OK                    | The request succeeded                                                                     |
| 204 No Content            | The request succeeded but no response was returned                                        |
| 400 Bad Request           | The request is syntactically ill-formed or violates [validation rules](validation_rules)  |
| 401 Unauthorized          | [Authentication](security) of the caller failed                                           |
| 403 Forbidden             | The call was rejected due to insufficient permissions of the caller                       |
| 404 Not Found             | The specified resource does not exist                                                     |
| 409 Conflict              | The request was rejected due to the state of the underlying resource                      |
| 500 Internal Server Error | An unrecoverable internal server error occured                                            |

For most errors, V10 APIs returns an error response body that includes an error code and a error
description. The error responses has the following structure:

```javascript
{
  "code": "19999",
  "message": "Tiny elves have invaded V10; we surrender",
  "CorrelationId": "197b2e31-787d-423f-ba00-0bd1f19291df"
}
```

## <a name="error_handling"></a> Error Handling

Clients integrating against the MobilePay PoS V10 API should expect intermittent errors and **must** implement suitable
error handling. Errors can generally be classified into three categories: *network errors*, *server errors* and
*client errors*. Network and server errors should be handled by retrying requests, while client errors should be
handled by fixing the client request. 

#### Network and server errors

Network errors typically present themselves as timeouts or connections that are closed prematurely. 
Network errors and server errors (HTTP 5XX responses) should be handled by retrying requests. All POST, PUT and
DELETE endpoints in the
V10 API are *idempotent* (in the sense that performing the same call multiple times will not cause additional state
changes beyond those caused by the first call) and are therefore safe to retry. All GET endpoints are pure (i.e.,
have no side-effects) and are therefore also safe to retry.

For instance, if a client calls to initiate a payment and the initiate call is successful but the client never
receives the response due to an intermittent network issue, then it is safe to retry the initiate payment call.
The second call will not initiate a new payment, but rather return the *PaymentId* of the already initiated
payment. This is achieved using an *idempotency key*, which is an id generated by the client that must
be included as part of the initiate payment request to identify retried requests. The idempotency key for
initiate payment requests must be unique for each payment on a given PoS. We recommend using a client-generated
*GUID* as the idempotency key. 

We recommend retrying failed requests due to network and server errors using one of these strategies:
* Retrying requests up to a fixed number of times with a constant delay between each call. 
* Retrying requests until a proper response is received, using an exponential backoff with jitter strategy.

#### Client errors

Client errors (HTTP 4XX) indicate a problem with the client request and can typically not be resolved by retrying
the request. HTTP 409 errors typically indicate that the client and the PoS backend is out-of-sync about
the state of a given resource (e.g., trying to capture a reservation that is not yet reserved or initiating
a payment on a PoS that already has an active payment). If possible, the client should try to query the given
resource to fix any inconsistencies between the client and the PoS backend.

### Examples

TODO

## <a name="throttling"></a> Throttling calls

## <a name="self_certification"></a> Self Certification

The certification process changes with API v10 - for the new API all minor and major versions of clients 
must be certified, MobilePay will provide an automatic certification process - where it will be possible 
for most integrators to create a fully automated self-certification. The certification will be concluded 
with an automated report on how the certification went.

Further details on self certification will follow in December 2019.

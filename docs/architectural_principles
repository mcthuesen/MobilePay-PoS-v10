
# Architectual Principles

This is a preliminary list of architectual principles.

**Backend has the truth**

An architectual principle in MobilePay PoS is that the Backend has the truth - that means in a situation where certainty is required, for instance is the payment approved, the app and clients will have to wait for confirmation from the backend.

**API versus Implementation**

The API does not describe the abstractions of the underlying backend OR client implementations - instead the API serves as the joint Interface for Backend and Frontend. The rammification for this is that BOTH frontend and backend can move independently from the API however they must always support the API specification and not only support perceived details of current implementations. ANY valid HTTP request must be handled appropiately by the backend and produce a useful informative HTTP response. Any valid HTTP response received in the client must be handled appropriately by the client.

**RESTful API**

The API is defined using the RESTful principles.

## <a href="api_responses"></a> API responses

Calls to the MobilePay PoS V10 API return HTTP status codes. For successful requests, 
V10 APIs return HTTP 2XX status codes. For failed requests, V10 APIs return HTTP 
4XX or 5XX status codes.

Titanium APIs return these HTTP status codes:

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

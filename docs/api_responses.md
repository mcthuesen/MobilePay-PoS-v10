## <a name="api_responses"></a>API responses

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


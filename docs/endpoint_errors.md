# <a name="endpoint_errors"></a> API Status-Codes and Errors

## Errors that needs handling for all endpoints
<details>
  <summary>
    ALL Endpoints
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1150 <br> 1151 <br> 1152 <br> 1153 <br> 1154 <br> 1155 <br> 1156 <br> 1157 <br> 1158 <br> 1159 <br> 1160 <br> 1161 | Missing ``IntegratorId`` header <br> Missing ``MerchantVatNumber`` header <br> Missing ``Client-System-Name`` header <br> Missing ``Client-System-Version`` header <br> Duplicated ``IntegratorId`` header <br> Duplicated ``MerchantVatNumber`` header <br> Duplicated ``Client-System-Name`` header <br> Duplicated ``Client-System-Version`` header <br> Invalid ``IntegratorId`` <br> Invalid ``MerchantVatNumber`` <br> Invalid ``Client-System-Name`` <br> Invalid ``Client-System-Version`` |
| 401 | - | Unauthorized |
| 500 | 2000 - 2999 | Internal server error - Please attach error code when communicating with MobilePay for quicker support |

</details>

## Payments
<details>
  <summary>
    GET /api/v10/payments/{paymentid} - Query a Payment
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1401 | Cannot query payments created by a different integrator |
| 404 | - | Payment not found |

</details>

<details>
  <summary>
    GET /api/v10/payments - Query Payments by a filter
  </summary> 

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1109 | An input parameter has invalid syntax <br> Payment filter not specific enough |

</details>

<details>
  <summary>
    POST /api/v10/payments - Initiate a Payment
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1102 <br> 1105 <br> 1113 <br> 1117 <br> 1162 <br> 1163 <br> 1164 | An input parameter has invalid syntax <br> Invalid ``Amount`` <br> Invalid ``UserMinimumAge`` <br> Invalid ``OrderId`` <br> Invalid ``MerchantPaymentLabel`` <br> Invalid ``Idempotency-Key`` <br> Duplicated ``Idempotency-Key`` header <br> Missing ``Idempotency-Key`` header |
| 403 | 1400 | Cannot initiate payments on a point of sale created by a different integrator |
| 409 | 1000 <br> 1301 <br> 1306 | Point of Sale not found <br> A payment is already active. Cancel it before starting a new one <br> ``Idempotency-Key`` has to be unique per request unless the request is a retry of a previous request <br>  |

</details>

<details>
  <summary>
    POST /api/v10/payments/prepare - Prepare a Payment
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1113 <br> 1162 <br> 1163 <br> 1164 | An input parameter has invalid syntax <br> Invalid ``OrderId`` <br> Invalid ``Idempotency-Key`` <br> Duplicated ``Idempotency-Key`` header <br> Missing ``Idempotency-Key`` header |
| 403 | 1400 | Cannot prepare payments on a point of sale created by a different integrator |
| 409 | 1000 <br> 1301 <br> 1306 | Point of sale not found <br> A payment is already active. Cancel it before starting a new one <br> ``Idempotency-Key`` has to be unique per request unless the request is a retry of a previous request |

</details>

<details>
  <summary>
    POST /api/v10/payments/{paymentid}/ready - Ready a Payment
  </summary>  

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1102 <br> 1105 <br> 1117 | An input parameter has invalid syntax <br> Invalid ``Amount`` <br> Invalid ``UserMinimumAge`` <br> Invalid ``MerchantPaymentLabel`` |
| 403 | 1401 | Cannot ready payments prepared by a different integrator |
| 404 | - | Payment not found |
| 409 | 1303 | Payment needs to be prepared before it can be marked as ready |

</details>

<details>
  <summary>
    POST /api/v10/payments/{paymentid}/capture - Capture a Payment
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1102 | An input parameter has invalid syntax <br> Invalid ``Amount`` |
| 403 | 1401 | Cannot capture payments created by a different integrator |
| 404 | - | Payment not found |
| 409 | 1304 <br> 1305 | Cannot capture payment when payment is not reserved <br> Capture ``Amount`` cannot exceed the reserved amount |

</details>

<details>
  <summary>
    POST /api/v10/payments/{paymentid}/cancel - Cancel a Payment
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1401 | Cannot cancel payments created by a different integrator |
| 404 | - | Payment not found |
| 409 | 1300 | The payment cannot be cancelled in the current state |

</details>

## Point of Sales
<details>
  <summary>
    GET /api/v10/pointofsales/{posid} - Query a Point of Sale
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1400 | Cannot query point of sales created by a different integrator |
| 404 | - | Point of sale not found |

</details>

<details>
  <summary>
    GET /api/v10/pointofsales - Query Point of Sales by a filter
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1121 | An input parameter has invalid syntax <br> Point of sale filter not specific enough |

</details>

<details>
  <summary>
    GET /api/v10/pointofsales/{posid}/checkin - Query a checkin on a Point of Sale
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1400 | Cannot query checkin on a point of sale created by a different integrator |
| 404 | - | Point of sale not found |

</details>

<details>
  <summary>
    POST /api/v10/pointofsales - Create a Point of Sale
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1100 <br> 1111 <br> 1112 <br> 1116 <br> 1118 <br> 1162 <br> 1163 <br> 1164 | An input parameter has invalid syntax <br> Invalid ``BeaconId`` <br> Invalid ``MerchantPosId`` <br> Invalid ``PosName`` <br> Invalid ``CallbackAlias`` <br> Invalid ``CalibrationType`` <br> Invalid ``Idempotency-Key`` <br> Duplicated ``Idempotency-Key`` header <br> Missing ``Idempotency-Key`` header |
| 409 | 1002 <br> 1200 <br> 1202 <br> 1306 | Store not found <br> A point of sale with that ``MerchantPosId`` already exist <br> A point of sale with that ``BeaconId`` already exist <br> ``Idempotency-Key`` has to be unique per request unless the request is a retry of a previous request |

</details>

<details>
  <summary>
    DELETE /api/v10/pointofsales/{posid} - Delete a Point of Sale
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1400 | Cannot delete point of sales created by a different integrator |
| 404 | - | Point of sale not found |

</details>

## Refunds
<details>
  <summary>
    GET /api/v10/refunds/{refundid} - Query a Refund
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1402 | Cannot query refunds created by a different integrator |
| 404 | - | Refund not found |

</details>

<details>
  <summary>
    GET /api/v10/refunds - Query Refunds by a filter
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1110 | An input parameter has invalid syntax <br> Refund filter not specific enough |

</details>

<details>
  <summary>
    POST /api/v10/refunds - Create a Refund
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1102 <br> 1114 <br> 1162 <br> 1163 <br> 1164 | An input parameter has invalid syntax <br> Invalid ``Amount`` <br> Invalid ``RefundOrderId`` <br> Invalid ``Idempotency-Key`` <br> Duplicated ``Idempotency-Key`` header <br> Missing ``Idempotency-Key`` header |
| 403 | 1401 | Cannot refund payments created by a different integrator |
| 409 | 1001 <br> 1306 <br> 1350 | Payment not found <br> ``Idempotency-Key`` has to be unique per request unless the request is a retry of a previous request <br> Refund ``amount`` cannot be higher than remaining amount on the payment to refund |

</details>

<details>
  <summary>
    POST /api/v10/refunds/{refundid}/capture - Capture a reserved Refund
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1402 | Cannot capture refunds created by a different integrator |
| 404 | 1004 | Refund not found |
| 409 | 1351 | Cannot capture refund when refund is not reserved |

</details>

<details>
  <summary>
    POST /api/v10/refunds/{refundid}/cancel - Cancel a reserved Refund
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 403 | 1402 | Cannot cancel refunds created by a different integrator |
| 404 | - | Payment not found |
| 409 | 1352 | The refund cannot be cancelled in the current state |

</details>

## Stores
<details>
  <summary>
    GET /api/v10/stores/{storeid} - Query a Store
  </summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 | An input parameter has invalid syntax |
| 404 | - | Store not found |

</details>

<details><summary>GET /api/v10/stores - Query a Store by MerchantBrandId and MerchantLocationId</summary>

| StatusCode | ErrorCodes  | Description |
|------------|-------------|-------------|
| 400 | 1099 <br> 1122 <br> 1119 <br> 1120 | An input parameter has invalid syntax <br> Store filter not specific enough <br> Invalid ``MerchantBrandId`` <br> Invalid ``MerchantLocationId`` |

</details>

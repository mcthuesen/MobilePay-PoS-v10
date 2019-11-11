## <a name="validation"></a>Validation Rules

#### Headers

| Name | Type | Length | Validations | Uniqueness requirements | Description |
| X-IBM-ClientId | Guid | 36 | | Globally unique | MobilePay Integrator Application Id. This identifies an application created through MobilePay Developer Portal. |



|Entity              | Type    | Validation rules     |
|--------------------|---------|----------------------|
|PoS ID              | string  |                      |
|Beacon ID           | string  |                     |
|Order ID            | string  |                    |
|Refund order ID     | string  |                   |
|Currency code       | string  |                  |                      
|Payment amount      | decimal |                 |
|Reservation length  | integer |                |
|User minimum age    | integer |               |
|Call back URL       | string  |              |
|PoS name            | string  |             |

## <a name="validation"></a>Validation Rules

#### Headers

| Name | Type | Length | Validations | Uniqueness requirements | Description |
|------|------|--------|-------------|-------------------------|-------------|
| X-IBM-ClientId | Guid | 36 | | Globally unique | MobilePay Integrator Application Id.<br><br> Identifies an application created through MobilePay Developer Portal. |
| X-MP-IntegratorId | Guid | 36 | | Globally unique | MobilePay Integrator Id.<br><br> Will be provided to Integrators by MobilePay. |
| X-MP-Client-System-Name | String | <= 36 | Charset | - | Integrators System Name.<br><br>Will be used to identify what Integrator System that is making the call to MobilePay Point of Sale API's. |



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

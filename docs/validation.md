## <a name="validation"></a>Validation Rules

#### Headers

| Name | Type | Length | Validations | Uniqueness requirements | Description |
|------|------|--------|-------------|-------------------------|-------------|
| X-IBM-ClientId | Guid | 36 | Guid | Globally unique | MobilePay Integrator Application Id.<br><br> Identifies an application created through MobilePay Developer Portal. |
| X-MP-IntegratorId | Guid | 36 | Guid | Globally unique | MobilePay Integrator Id.<br><br> Will be provided to Integrators by MobilePay. |
| X-MP-Client-System-Name | String | ≤ 36 | Charset | - | Integrators System Name.<br><br>Will be used to identify what Integrator System that is making the call to MobilePay Point of Sale API's. |
| X-MP-Client-System-Version | String | ≤ 36 | Valid Client-Version | - | Integrators System Version.<br><br>Will be used to identify what Version of the Integrator System that is making the call to MobilePay Point of Sale API's. |

#### Brands

| Name | Type | Length | Validations | Uniqueness requirements | Description |
|------|------|--------|-------------|-------------------------|-------------|
| MerchantBrandId | String | 10	| MPPOSXXXXX<br>POSDKXXXXX<br>POSFIXXXXX | Globally unique | MobilePay Brand Id<br><br>This identifies a Brand in MobilePay. |

#### Stores

| Name | Type | Length | Validations | Uniqueness requirements | Description |
|------|------|--------|-------------|-------------------------|-------------|
| StoreId | Guid | 36 | Guid | Globally unique | MobilePay Store Id.<br><br>This identifies a Store in MobilePay. |
| MerchantLocationId | String | 5 | Charset | /Merchant | MobilePay Location Id.<br><br>Together with a MerchantBrandId, this identifies a Store in MobilePay. |



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

## <a name="validation"></a>Validation Rules

#### Headers

| Name | Validations | Description |
|------|-------------|-------------|
| X-IBM-ClientId | Guid | MobilePay Integrator Application Id.<br><br> Identifies an application created through MobilePay Developer Portal. |
| X-MP-IntegratorId | Guid | MobilePay Integrator Id.<br><br> Will be provided to Integrators by MobilePay. |
| X-MP-Client-System-Name | String with up to 36 valid characters | Integrators System Name.<br><br>Will be used to identify what Integrator System that is making the call to MobilePay Point of Sale API's. |
| X-MP-Client-System-Version | Valid Client-Version:<br>Major.Minor.Build<br>Example: 1.2.231 | Integrators System Version.<br><br>Will be used to identify what Version of the Integrator System that is making the call to MobilePay Point of Sale API's. |

#### Brands

| Name | Validations | Uniqueness requirements | Description |
|------|-------------|-------------------------|-------------|
| MerchantBrandId | MPPOSXXXXX / POSDKXXXXX / POSFIXXXXX | Globally unique | MobilePay Brand Id<br><br>This identifies a Brand in MobilePay. |

#### Stores

| Name | Type | Length | Validations | Uniqueness requirements | Description |
|------|------|--------|-------------|-------------------------|-------------|
| StoreId | Guid | 36 | Guid | Globally unique | MobilePay Store Id.<br><br>This identifies a Store in MobilePay. |
| MerchantLocationId | String | 5 | Charset | /Merchant | MobilePay Location Id.<br><br>Together with a MerchantBrandId, this identifies a Store in MobilePay. |

#### Point of Sales

| Name | Type | Length | Validations | Uniqueness requirements | Description |
|------|------|--------|-------------|-------------------------|-------------|
| PosId | String | ≤ 36 | Charset | /Merchant | Merchant defined Point of Sale Id.<br><br>Together with a MerchantId, this identifies a Point of Sale. |
| PosName | String | ≤ 36 | Charset | - | Merchant defined Point of Sale Name.<br><br>The name is visible to a MobilePay User, after the User has checked in on the Point of Sale. |
| CallbackUrl | String | ≤ 2048 | Valid URI OR Charset | N/A |In case of the Integrator System not being able to detect User CheckIn's, they can have the MobilePay Notification Service call this URL when a User has checked in.<br><br>To use the Notification Service the Callback URL needs to be manually approved by MobilePay before use.<br><br>The CallbackUrl can be either a valid URL or it can contain an Alias predefined by an agreement between MobilePay and the Integrator.<br><br>It can be relevant to use an Alias in case it is hard for the Integrator to update the CallbackUrl on hardware units such as Terminals. |
| BeaconId | String | 15 OR 36 | Digits OR Guid | Globally unique | Id of the Beacon.<br><br>In case of psysical device such as the MobilePay WhiteBox or a Terminal: The BeaconId is a 15 digit string.<br><br>If no psysical device (QR): BeaconId is not provided during Point of Sale creation and MobilePay will generate a String containing a random GUID as the BeaconId. |
| BeaconType | Enum | N/A | QR / NFC / BluetoothOther / BluetoothMP1 / BluetoothMP2 / BluetoothMP3 / BluetoothMP4 | N/A	| Beacon broadcast type.<br><br>Identifies an option for how a MobilePay User can CheckIn on a Point of Sale.<br><br>During creation of a Point of Sale, a list of Beacon Types are provided that defines how MobilePay Users can CheckIn on the Point of Sale. |
| CalibrationType | Integer |	≤ 5 | 0-65535 | N/A	| Calibration Type of a psysical Beacon.<br><br>This is used by the MobilePay app to know the distance between the Mobile Phone and the psycical Beacon before the MobilePay User Checks In on the Point of Sale.<br><br>This is only applicable if the Point of Sale contains any of the bluetooth BeaconTypes. |

#### Payments

| Name | Type | Length | Validations | Uniqueness requirements | Description |
|------|------|--------|-------------|-------------------------|-------------|
| PaymentId | Guid | 36 | Guid | Globally unique | MobilePay defined Payment Id. |
| OrderId | String | ≤ 36 | Charset | No (Recommended: /Pos) | Merchant defined Payment Order Id. |
| Amount | Decimal | - | Valid Positive Amount | N/A | Total Amount of the Payment. |
| CurrencyCode | Enum	| - | DKK / EUR | N/A	 | Currency Code for the Currency of the Payment. |
| MerchantPaymentLabel | String | ≤ 36 | Charset | No	| Label for the Payment.<br><br>This is a way for the Merchant to tag a Payment with a Label.<br><br>This is visible in the transaction reporting section on the MobilePay Portal |
| ReservationDurationInDays | Int | N/A | 1 - 14 | N/A | The number of days to keep the Payment reserved on the MobilePay User's Card/Account.<br><br>It is recommended to use the shortest duration possible in regards to the use case.|

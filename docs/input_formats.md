# <a name="input_formats"></a> Input and Output Formats

This page gives an overview of the format and length restrictions for all input parameters used in the PoS V10 API. 

## HTTP Headers
For more information about the http headers, see [API principles](api_principles).

| Name | Format      | Description |
|------|-------------|-------------|
| `X-IBM-ClientId` | Guid | Identifies an application created through MobilePay Developer Portal. |
| `X-MobilePay-Client-System-Name` | String with at most 36 valid characters | Identifies the [integrator system](api_principles#client_identification) calling the API. |
| `X-MobilePay-Client-System-Version` | Valid Client-Version:<br>Major.Minor.Build<br>Example: 1.2.1 | Identifies the [version of the integrator system](api_principles#client_identification) calling the API. |
| `X-MobilePay-Idempotency-Key` | String with at most 36 valid characters | Used to allow calls to be [safely retried](api_principles#error_handling) in case of errors. |

## Brands
For more information about brands, see [PoS Management](pos_management).

| Name | Format      | Description |
|------|-------------|-------------|
| `MerchantBrandId` | MPPOSXXXXX <br> POSDKXXXXX <br> POSFIXXXXX | Identifies a Brand in MobilePay. |
| `BrandName` | String | The name of the brand. |

## Stores
For more information about stores, see [PoS Management](pos_management).

| Name | Format      | Description |
|------|-------------|-------------|
| `StoreId` | Guid | Identifies a Store in MobilePay. |
| `MerchantLocationId` | String with exactly 5 valid characters | MobilePay location ID.<br><br>Together with a MerchantBrandId, this identifies a Store in MobilePay. |

## <a name="poses"></a> Point-of-Sales
For more information about a PoS, see [PoS Management](pos_management).

| Name | Format      | Description |
|------|-------------|-------------|
| `PosId` | Guid | Identifies a PoS in MobilePay. |
| `MerchantPosId` | String with at most 36 valid characters | Merchant defined PoS ID.<br><br>There can be at most one active PoS with a given `MerchantPosId` for a given integrator and merchant. |
| `PosName` | String with at most 36 valid characters | Merchant defined PoS name.<br><br>The name is visible in the app, after the customer has checked in on the PoS. |
| `CallbackAlias` | String with at most 36 valid characters | Only for clients that use the [notification service](notification_service) to detect MobilePay payments. The CallbackAlias is a key that identifies which notification endpoint to call for the given PoS. |
| `BeaconId` | A GUID or 15 digits | ID of the Beacon.<br><br>In case of physical device such as the MobilePay WhiteBox or a terminal the `BeaconId` is a 15 digit string.<br><br>In case of no physical device (QR) the `BeaconId` is not provided during PoS creation. MobilePay will generate a string containing a random GUID as the `BeaconId`. |
| `SupportedBeaconTypes` | `QR` / `NFC` / `BluetoothOther` / `BluetoothMP1` / `BluetoothMP2` / `BluetoothMP3` / `BluetoothMP4`	| Beacon broadcast type.<br><br>Identifies an option for how a customer can check in on a PoS.<br><br>During the creation of a PoS, a list of Beacon Types has to be provided. |
| `CalibrationType` | Integer between 0 and 65535 | Calibration Type of a physical beacon.<br><br>This is used by the MobilePay app to know the distance between the mobile device and the phycical beacon before the customer checks in on the PoS.<br><br>This is only applicable if the PoS contains any of the bluetooth `BeaconTypes`. |

## Payments
For more information about payments, see [Payment Flows](payment_flows).

| Name | Format      | Description |
|------|-------------|-------------|
| `PaymentId` | GUID | MobilePay defined Payment ID. |
| `OrderId` | String with at most 36 valid characters | Merchant defined payment order ID.<br><br>There is no uniqueness requirement for the `OrderId`, but it is highly recommended to use unique order IDs. |
| `Amount` | Valid positive amount | Total amount of the payment. |
| `CurrencyCode` | `DKK` / `EUR` | Currency code for the currency of the payment. |
| `MerchantPaymentLabel` | String with at most 36 valid characters	| Label for the payment.<br><br>This is a way for the merchant to tag a payment with a label that will be visible in the transaction reporting section on the MobilePay Portal |
| `PlannedCaptureDelay` | `None` / `LessThan24Hours` / `LessThan14Days`	| How long time the client expects to wait after receiving a reservation before capturing.<br><br>See [Specify planned capture delay](best_practices#specify-planned-capture-delay). |
| `CustomerToken` | String with at most 40 valid characters	| An alphanumeric string, uniquely identifying the customer. |
| `CustomerReceiptToken` | String with at most 32 valid characters	| An alphanumeric string used for Storebox. |
| <a name="restrictions"></a>`Restrictions` | Json object with one or more parameters | A way to define restrictions on how a payment can be completed. See [Payment Restrictions](input_formats#payment_restrictions) for possible restriction parameters |

### <a name="payment_restrictions"></a>Payment Restrictions
| Name | Format      | Description |
|------|-------------|-------------|
| `DebitCardDisallowed` | Boolean | When DebitCardDisallowed is set to true, debit cards cannot be used for this payment |
| `CreditCardDisallowed` | Boolean | When CreditCardDisallowed is set to true, credit cards cannot be used for this payment |
| `UserMinimumAge` | Positive Integer | When UserMinimumAge is set, MobilePay will cancel the payment if attempted accepted by users younger than the UserMinimumAge |

## Valid characters

Valid characters for PoS V10 API request fields are:
* 0 - 9
* a-zA-Z
* æÆøØåÅ
* äÄöÖšŠžŽ
* !"#$%&'()*+,-./":;<=>?@[\]^_\`{\|}~
* (space)

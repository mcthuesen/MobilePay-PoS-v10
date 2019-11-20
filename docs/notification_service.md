# <a name="NotificationService"></a> Notification Service

Clients that are unable to detect whether a MobilePay user has checked-in by either [User Activation](detecting_mobilePay#user_activation) or [BLE 2-Way](detecting_mobilePay#ble) can use the notification service. To be able to use the notification service, you need to implement an endpoint that MobilePay will call, when a client should query the active check-in on a PoS.

When you have implemented the endpoint you need to let us know the URL for validation and whitelisting in our firewalls. You do this by sending an email to developer@mobilepay.com. When the URL is whitelisted we will send back a reference to the URL that we call a CallbackAlias. The client will use this alias when [creating PoSes](pos_management#pos_creation) to indicate which notification endpoint to call.

## <a name="NotificationEndpoint"></a> Notification endpoint

The requirements for a notification endpoint are as follows:

* It must be an HTTPS POST endpoint.
* It must accept a JSON body that has the following format:  

```javascript
{
  "MerchantId"          : "622d3369-f940-4921-93eb-c8fca0c081b4",
  "MerchantBrandId"     : "MPPOS12345",
  "MerchantLocationId"  : "12345",
  "MerchantPosId"       : "MobilePay Merchant Pos Id"
  "PosId"               : "7e6acbde-345e-4641-b2f4-d8df0f3a5147"
}
```
* The format of the fields can be found here: [Input Formats](validation)

* The notification endpoint should respond with a ````200 OK```` status code when the notification was processed successfully. The MobilePay notification service will retry notification calls in case of any other response than ````200 OK````.

## Migrating to a different notification endpoint

In case existing PoSes have to be migrated to use a different notification, you can write to us at developer@mobilepay.com and ask us to whitelist the new URL and change the mapping for an existing alias to a new URL. Close collaboration on the time of switching the URL is important to make sure your new endpoint is ready to receive notifications at the time we change the URL of the alias.

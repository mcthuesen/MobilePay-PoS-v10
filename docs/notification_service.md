# <a name="NotificationService"></a> Notification Service
If your client is unable to detect whether a MobilePay user has checked-in by either [User Activation](Detecting_MobilePay#UserActivation) or [BLE 2-Way](Detecting_MobilePay#BLE2way) you can use our notification service.

To be able to use the notification service, you need to implement an [endpoint](detecting_mobilePay#NotificationEndpoint) that MobilePay will send a notification to, when we want you to query the active check-in on a PoS.

When you have implemented the endpoint you need to let us know the URL. You do this by sending an email to developer@mobilepay.com to let us know the URL so our security team can validate and whitelist the URL.

## Callback URL Registration

When the URL is whitelisted, there is two ways of registering the URL on your Point of Sale. [URL Direct](detecting_mobilePay#URL_Direct) or [URL by Alias](detecting_mobilePay#URL_by_Alias)

### <a name="URL_Direct"></a> URL Direct
When creating your Point-of-Sales using the endpoint **/v10/pointofsales** you have to include a callback that will look like this:

```javascript
"callback": {
  "destination"         : "http://example.com",
  "type"                : "Url"
}
```

This way of providing the URL is the easiest way to get started using the notification service. On the contrary if you imagine that the URL will change in the future then [URL by Alias](detecting_mobilePay#URL_by_Alias) is the best way to go.

### <a name="URL_by_Alias"></a> URL by Alias
When you want the possibility of changing the URL, without having to re-configure all your clients with the new URL, you will have to use this method of providing the URL.

First you will need to send an email to developer@mobilepay.com and request to map your URL to an alias.
Then you can create your Point-of-Sales using the endpoint **/v10/pointofsales** with a callback looking like this:

```javascript
"callback": {
  "destination"         : "AliasForMyURl",
  "type"                : "Alias"
}
```

Now when you have to change the URL you can write to us at developer@mobilepay.com and ask us to whitelist the new URL and afterwards change the mapping from your alias to the new URL. Close collaboration on the time of switching the URL is important to make sure your new endpoint is ready to receive notifications at the time we change the URL of the alias. 

## <a name="NotificationEndpoint"></a> HTTP POST endpoint
The requirements for the endpoint you will have to develop is as follows:

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



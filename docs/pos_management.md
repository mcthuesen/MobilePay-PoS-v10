## <a name="pos_management"></a>PoS Management

All payments and check-ins are done on a PoS. This could represent a terminal, a QR code, etc. Our API contains a PoS Management section to handle creation, deletion and querying of a PoS. The PosId has to be unique per merchant but if the PoS is deleted the ID can be reused.

Note that a PoS is not editable. If you need to change something on the PoS (e.g. name, callback URL, ID) you have to delete the existing PoS and create a new one with the changes. Best practice for changing values on a PoS is to re-use the same PosId.

When creating a new PoS you have to specify supported beacon types. This list is used to keep track of which beacon types are used by your PoS, but it is also used by MobilePay to better detect errors and for better customer support.

The Point of Sales section also includes endpoints for getting the active payment and getting a payment by order id. The payment id received by these calls can be used to look up the payment by calling the endpoint (/v10/payments/{paymentId}) in the Payments section. The payment id (GUID) should be known at all times. In the rare case that this id is lost, it can be retrieved by using the order id set on creation of the payment.

The checkout endpoint is used to remove the checked in user, but can only be used when there is no active payment yet. If a payment is present use /v10/pointofsales/{posId}/payment/cancel. This will cancel the active payment and checkout the user. The rules for when a payment can be cancelled are the same as for cancelling a payment by paymentId as described in the Payment Flows section.

The check-in endpoint will tell you whether a user is checked-in and the potential loyalty ids of the user. If your system expects a check-in before starting a payment, this endpoint can be used to poll for that check-in information.


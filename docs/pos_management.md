## <a name="pos_management"></a>PoS Management

All payments and check-ins are done on a Point of Sale. This could represent a terminal, a QR code, etc. Our API contains a PoS Management section to handle creation, deletion and different queries of a PoS. The PosId has to be unique per merchant but if the PoS is deleted the ID can be reused.

Note that a PoS is not editable. In the case where you need to change something on the PoS (e.g. name, callback URL, ID) you will have to delete the existing PoS and create a new with the changes. Best practice for changing different values on a PoS is to use the same PosId.

When creating a new PoS you specify supported beacon types. These are used to keep track of which beacon types are used but it is also used by our team to better detect errors and for better customer support.

The Point of Sales section also includes endpoints for getting the active payment and getting a payment by order id. The payment id received by these calls can be used to look up the payment by calling the endpoint (/api/v10/payments/{paymentId}) in the Payments section. The payment id (GUID) should be known at all times but in the rare case that this id is lost, it can be retrieved if the order id set by the merchant is known.

The section includes endpoints for check-in and checkout. 

The checkout endpoint is used to remove the user but can only be used when there is no payment yet. This functionality is therefore to be understood as a clean-up. In the case where a payment is present the recommendation is to use /api/v10/pointofsales/{posId}/payment/cancel which will cancel the active payment and checkout the user. The rules for when a payment can be cancelled are the same as for cancelling a payment by the payment id as described in the Payment Flows section.

The check-in endpoint will tell you whether a user is checked-in and the potential loyalty ids of the user. In the case, your system expects a check-in before starting a payment this endpoint can be used to poll for that check-in information.


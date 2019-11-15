## <a name="best_practices"></a> Best Practices

This section is an overview over best practices when integrating to MobilePay PoS. The purpose of these best practices is to optimize the user and merchant experience, to reduce errors and keep the integration as simple as possible without reducing user and merchant experince. 

### Check-in before or after payment has been initiated?
While our system supports users checking in both before or after a payment has been initiated, we suggest urging users to check-in before.
As an example: In a supermarket a user can check-in and then start bagging his groceries. When all the groceries have been scanned the cash register will initiate the payment and allow the user to swipe. 
This is an advantage over both cash and card payments, as the user has no need to go back to the terminal/payment area again. which means a faster transaction for all involved parties.

### Payment and Loyalty-Payment flows
We have two main payment flows in the V10 API.
Initiate payment followed by a Capture, and a flow where initiate payment is split into two parts: Prepare-Ready and then followed by a capture.
We recommend to use the Initiate-Capture flow if you do not need to calculate discounted amounts based on a loyalty ID. Then you will save a call to our API and in the end improve the overall time it takes to complete a payment.

### Specify Expected Capture When
It is required to specify when the payment is expected to be captured. The values are either immediately, Within24Hours, and Within14Days. These are values that control how payments are handled by MobilePay Support and it is therefore beneficial that these values are set as accurately as possible.

### Order ids
Order ids are not required to be unique however we do recommend it.
In error cases where you lost the paymentId you can use the **/v10/payments** endpoint to lookup payments based on the posId and the orderId. If orderId is unique you can count on this endpoint returning only the one payment you are looking for. If the orderId is not unique you might experience getting a list of payments not knowing which one you were looking for.
That is why we recommend always to use unique orderIds.

### Capture or Cancel of old Reservations
All reservations should be captured or cancelled as soon as practically possible. It is the task of the PoS Client to determine whether or not a reservation should be captured or cancelled. Therefore it is bad practice to poll for outstanding payments that are in reserved state and either cancel or capture.

### Polling
It is possible to get information on a payment using **/v10/payments/{paymentId}**, and it is possible to get information about an active check-in using **/v10/pointofsales/{posId}/checkin**. 
For both of these endpoints, it is allowed to do polling at most once per second as the default. Polling times are controlled by the backend, whenever you receive a response - the response will always contain a time interval that specifies, when the endpoint should at the earliest be polled again. We recommend polling as fast as allowed by the backend to ensure maximal end user experience.

### Payment restrictions
It is possible to restrict which card types can be used for a payment. This restriction is available because some countries have restrictions on which cards can be used for certain products.
It is also possible to set a minimum age for the paying user. As an example, this can be set on payments involving alcohol or gambling products.
We recommend only setting restrictions on payments where you are required to do so by the law or in case there are some business related reasons for restricting which cards can be used. 



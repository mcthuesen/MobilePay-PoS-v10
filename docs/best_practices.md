## <a name="best_practices"></a> Best Practices

This section is an overview over best practices when integrating to MobilePay PoS. The purpose of these best practices is to optimize the user and merchant experience, to reduce errors and keep the integration as simple as possible without reducing user and merchant experince. 

### Check-in before or after payment has been initiated?
While our system supports users checking in both before or after a payment has been initiated, we suggest urging users to check-in before.
As an example: In a supermarket a user can check-in and then start bagging his groceries. When all the groceries have been scanned the cash register will initiate the payment and allow the user to swipe. 
This is an advantage over both cash and card payments, as the user has no need to go back to the terminal/payment area again. which means a faster transaction for all involved parties.

### Prepare-Ready
The intention of the Prepare-Ready flow is for the merchant to postpone sending the amount to MobilePay, until after they know whether a user has checked in. 
The primary use case this was designed for, is where the merchant wants to know whether the user has a Loyalty card registered with the merchant, before sending the amount to the user. If integrators and merchants find other use cases for this payment flow, we would be happy to hear about them :-)

### Order ids
Order ids are intended be unique within a single PoS. This requirement is in place, to make it possible to lookup a paymentId using an orderId. 
When a payment is created using an orderId already used on a specific PoS, the new paymentId will be returned when querying with the orderId.

### Polling
It is possible to get information on a payment using **/v10/payments/{paymentId}**, and it is possible to get information about an active check-in using **/v10/pointofsales/{posId}/checkin**. 
For both of these endpoints, it is allowed to do polling at most once per second.

### Reservation length
Currently, a reservation in MobilePay can have a maximum length of 14 days. The maximum reservation length is shorter for some card types, but this is not represented in the API. 
Due to this constraint, it is not recommended that reservations last multiple days, as we are not always in control of when they expire.

### Payment restrictions
It is possible to restrict which card types can be used for a payment. This restriction is available because some countries have restrictions on which cards can be used for certain products.
It is also possible to set a minimum age for the paying user. As an example, this can be set on payments involving alcohol or gambling products.

### Refunds
A payment can both be fully and partially refunded. It is possible to do multiple partial refunds, up to the full amount of the original payment. 


## <a name="best_practices"></a> Best Practices

This section is an overview over best practices when integrating to MobilePay PoS. The purpose of these best practices is to optimize the user and merchant experience, to reduce errors and keep the integration as simple as possible without reducing user and merchant experince. 

### Check-in before or after payment has been initiated?
While our system supports users checking in both before or after a payment has been initiated, we suggest urging users to check-in before.
As an example: In a supermarket a user can check-in and then start bagging his groceries. When all the groceries have been scanned the cash register will initiate the payment and allow the user to swipe. 
This is an advantage over both cash and card payments, as the user has no need to go back to the terminal/payment area again. which means a faster transaction for all involved parties.

### Payment Flows
We have two main payment flows in the V10 API.
Initiate payment followed by a Capture, and a flow where initiate payment is split into two parts: Prepare-Ready and then followed by a capture.
We recommend to use the Initiate-Capture flow if you do not have a use case for the latter. Then you will save a call to our API and in the end improve the overall time it takes to complete a payment.

### Reservation Duration? Capture
We allow the integrator to reserve the payment amount between one and fourteen days before it will expire. However it is rarely a good idea to reserve the money for more than one day. We recommend setting the Reservation Duration to one day unless there is a reason for it. A reason could be if you are runnning a rental shop where you will need to reserve the payment amount over time and capture the amount when the costumer returns the rented item.

### Order ids
Order ids are not required to be unique however we do recommend it.
In error cases where you lost the paymentId you can use the **/v10/payments** endpoint to lookup payments based on the posId and the orderId. If orderId is unique you can count on this endpoint returning only the one payment you are looking for. If the orderId is not unique you might experience getting a list of payments not knowing which one you were looking for.
That is why we recommend always to use unique orderIds.

### Polling
It is possible to get information on a payment using **/v10/payments/{paymentId}**, and it is possible to get information about an active check-in using **/v10/pointofsales/{posId}/checkin**. 
For both of these endpoints, it is allowed to do polling at most once per second as the default. Polling times are controlled by the backend, whenever you receive a response - the response will contain when a poll should at the earliest be called again.
That is also the frequency we recommend to use. If you poll once per second you will make sure that the payment flow runs as smoothly as possible for the MobilePay costumer. 
If you choose to poll the checkin slower than once per second, the MobilePay user will experience a longer time from checking-in until the payment amount shows op on their screen. 
If you choose to poll the payment status slower then once per second the user will experience longer time after they have accepted the payment to the MobilePay receipt shows up on their screen.

### Payment restrictions
It is possible to restrict which card types can be used for a payment. This restriction is available because some countries have restrictions on which cards can be used for certain products.
It is also possible to set a minimum age for the paying user. As an example, this can be set on payments involving alcohol or gambling products.
We recommend only setting restrictions on payments where you are required to do so by the law or in case there are some business related reasons for restricting which cards can be used. 

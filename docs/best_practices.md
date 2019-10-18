## <a name="best_practice"></a> Best Practices

This section is an overview over best practices when integrating to MobilePay PoS. The purpose of these best practices is to optimize the user and merchant experience, to reduce errors and keep the integration as simple as possible without reducing user and merchant experince. 

## Check-in before or after payment has been initiated?
While our system supports users checking in both before or after a payment has been initiated, we suggest urging users to check-in before.
As an example: In a supermarket a user can check-in and then start bagging his groceries. When all the groceries have been scanned the cash register will initiate the payment and allow the user to swipe. 
This is an advantage over both cash and card payments, as the user has no need to go back to the terminal/payment area again. which means a faster transaction for all involved parties.

## Prepare-Ready
The intention of the Prepare-Ready flow is for the merchant to postpone sending the amount to MobilePay, until after they know whether a user has checked in. 
The primary use case this was designed for, is where the merchant wants to know whether the user has a Loyalty card registered with the merchant, before sending the amount to the user. If integrators and merchants find other use cases for this payment flow, we would be happy to hear about them :-)

## Order ids
Order ids are intended be unique within a single PoS. This requirement is in place, to make it possible to lookup a paymentId using an orderId. 
When a payment is created using an orderId already used on a specific PoS, the new paymentId will be returned when querying with the orderId.

## Polling
It is possible to get information on a payment using **/v10/payments/{paymentId}**, and it is possible to get information about an active check-in using **/v10/pointofsales/{posId}/checkin**. 
For both of these endpoints, it is allowed to do polling at most once per second.

## Reservation length
Currently, a reservation in MobilePay can have a maximum length of 14 days. The maximum reservation length is shorter for some card types, but this is not represented in the API. 
Due to this constraint, it is not recommended that reservations last multiple days, as we are not always in control of when they expire.

## Payment restrictions
It is possible to restrict which card types can be used for a payment. This restriction is available because some countries have restrictions on which cards can be used for certain products.
It is also possible to set a minimum age for the paying user. As an example, this can be set on payments involving alcohol or gambling products.

## Refunds
A payment can both be fully and partially refunded. It is possible to do multiple partial refunds, up to the full amount of the original payment. 

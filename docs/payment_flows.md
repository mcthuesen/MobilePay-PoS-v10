## <a name="payment-flows"></a>Payment Flows

Our system supports two different types of payments: Instant and reservations. An instant payment does not require approval from merchant to complete payment, after the user has approved the payment. When the user has approved, the payment is done and no further action is needed. A reservation need approval from merchant in the sense that they will have to call the capture endpoint in order to finish the payment. The API supports both full and partial captures.

The sequence diagrams below show the two different flows.

Reaching the state where a payment is initiated can be done in two different ways:
1.	Directly using either /api/v10/payments/instant or /api/v10/payments/reservation
2.	In two steps using either /api/v10/payments/instant/prepare /api/v10/payments/reservation/prepare followed by the ready endpoint /api/v10/payments/{paymentId}/ready

For regular payments, best practice is to use option 1.

Option 2 is intended for cases where you do not want to specify the amount on the payment before the user is checked in and locked on the payment. This could be in the case of loyalty payments where the merchant might want to reduce the amount to be paid after knowing what type of loyalty card the user has. 

The API supports cancelling a payment but a payment can only be cancelled when it has not been captured yet either by us (instant payment) or by the merchant (reservation payment).

### <a name="order_of_events"></a>Order of events

The system supports check-in both before and after the payment has been initiated. This is also the case in Option 2 but the intended flow is to prepare the payment, let the user check in and then mark the payment as ready by calling our ready endpoint (as shown in the sequence diagram).


[![](assets/images/InstantFlow.png)](assets/images/InstantFlow.png)

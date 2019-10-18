## <a name="payment-flows"></a>Payment Flows

Our system supports two different types of payments: Instant and reservations. An instant payment does not require approval from the merchant to complete the payment, after the user has approved the payment. When the user has approved, the payment is done and no further action is needed. A reservation needs approval from the merchant in the sense that they will have to call the capture endpoint in order to finish the payment. The API supports both full and partial captures.

The sequence diagrams below show the two different flows. Reaching the state where a payment is initiated can be done in two different ways:
1.	Directly using either /v10/payments/instant or /v10/payments/reservation
2.	In two steps using either /v10/payments/instant/prepare /v10/payments/reservation/prepare followed by the ready endpoint /v10/payments/{paymentId}/ready

For regular payments, best practice is to use option 1.
Option 2 is intended for cases where you do not want to specify the amount on the payment before the user is checked in and locked on the payment. This could be in the case of loyalty payments where the merchant might want to reduce the amount to be paid after knowing what type of loyalty card the user has. 

The API supports cancelling of payments. A payment can only be cancelled before it has been captured. Either by Mobilepay (Instant payments) or by the merchant (Reservation payments).

The system supports checking in either before or after the payment has been initiated. This is also the case in Option 2 but the intended flow is to prepare the payment, let the user check in and then mark the payment as ready by calling our ready endpoint (as shown in the sequence diagram).



### <a name="instant"></a>Instant Payment Flow

[![](assets/images/InstantFlow.png)](assets/images/InstantFlow.png)


[![](assets/images/InstantFlow_CheckInAfterPaymentInitiated.png)](assets/images/InstantFlow_CheckInAfterPaymentInitiated.png)

### <a name="instant"></a>Instant Payment Flow Using Prepare-Ready

[![](assets/images/InstantPrepareFlow.png)](assets/images/InstantPrepareFlow.png)

### <a name="instant"></a>Reservation Payment Flow

[![](assets/images/ReservationFlow.png)](assets/images/ReservationFlow.png)

### <a name="instant"></a>Reservation Payment Flow Using Prepare-Ready

[![](assets/images/ReservationPrepareFlow.png)](assets/images/ReservationPrepareFlow.png)

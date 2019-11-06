# Payment Option Detection

There are three ways in MobilePay PoS for a terminal/client to become aware that MobilePay has been chosen by the customer as the payment option; User activation, Notification service and BLE 2-way communication.

**User activation**

This is the default way of detecting MobilePay presence. In a supermarket this can be a button on the ECR that sends the payment request to MobilePay. For example the cashier will ask the customer or infer from the customer's actions which payment option the customer wants to choose and then push the MobilePay button. Another example of user activation is when the customer can choose MobilePay herself on a keypad placed on a vending machine for instance. Some vending machines only allow MobilePay to be used and therefore any request for the vending machine product would be inferred as a payment request to MobilePay.

A last example of a user activation is in the case of a QR code being displayed in a terminal - in these cases the terminal calls a HTTP GET checkin endpoint in the MobilePay v10 API - this approach ensures that this endpoint is not overloaded with requests.

**Notification service**

Some interfaces do not naturally include a possibility for user activation - in these cases an endpoint can be exposed by the MobilePay PoS integrator. This endpoint will be called with a checkin Notification in the case a user has checked in. After receiving a notification the client can poll the HTTP GET checkin endpoint for that client.

**BLE 2-way communication**

It is possible to get information about check ins via Bluetooth Low Energy - To use this approach the Integrator will need to use one of the MobilePay defined Bluetooth communication protocols. TODO insert link to Bluetooth documentation.

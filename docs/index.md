
# <a name="index"></a> Introduction 

Our MobilePay Point of Sale (PoS) REST API is intended for integrators implementing MobilePay payments in a PoS system.

For information about the PoS product and details on Getting Started, Test and Certification please visit our
<a href="https://developer.mobilepay.dk/subscriptions-main">Developer Portal</a>. On the portal you will also find FAQ and support resources.

This document will explain in more detail how to implement the different payment flows, how to manage the PoS, how the Security model is built and what is needed from the integrator.

This document does not include detailed specification of the endpoints, responses and response codes. This information can be found in the <a href="https://developer.mobilepay.dk/product"> API section</a> of the portal.


[![](assets/images/Preview-MP-logo-and-type-horizontal-blue.png)](assets/images/Preview-MP-logo-and-type-horizontal-blue.png)

# General description
MobilePay PoS is an API for setting up Merchant's transaction requests on customers' MobilePay apps in a store. MobilePay PoS does not require the customer to manually enter any information in the MobilePay app pertaining to the transaction. A transaction request can typically be obtained by the customer by holding the phone near to a Merchant device(Terminal, BLE beacon, etc.) OR scanning a QR code.

There are two types of transactions in MobilePay PoS:
* a payment which is a near instantaneous transfer of funds following the approved payment request 
* a reservation where the transfer of funds happens sometime after the approval of the reservation request. 

Currently MobilePay PoS uses BLE one-way and two-way beacons and QR-codes to set up the transaction requests - the technology choices are not important for the API - however the concept of a beacon ID is central to allow matching of the Customer willing to pay and the Merchant's transaction request.

## The MobilePay Developer Portal
The MobilePay Developer Portal is a site where you will be able to find information about the products and available APIs and their documentations.
It exposes live documentation that can be used for development and error correction. Access to the portal can be requested by writing to the following email address developer@mobilepay.dk .

The MobilePay Developer Portal is available at the following addresses:

| Environment  | Endpoint |
|--------------|-------------|
| Sandbox/Test | [https://sandbox-developer.mobilepay.dk/](https://sandbox-developer.mobilepay.dk/) |
| Production   | [https://developer.mobilepay.dk](https://developer.mobilepay.dk) |

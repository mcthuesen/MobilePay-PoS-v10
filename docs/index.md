
# <a name="index"></a> Introduction 

Our MobilePay Point of Sale (PoS) REST API is intended for integrators implementing MobilePay payments in a PoS system.

For information about the PoS product and details on Getting Started, Test and Certification please visit our
<a href="https://developer.mobilepay.dk/subscriptions-main">Developer Portal</a>. On the portal you will also find FAQ and support resources.

This document will explain in more detail how to implement the different payment flows, how to manage the PoS and how the Security model is build and what is needed from your side.

This document does not include detailed specification of the endpoints, responses and response codes. This information can be found in the <a href="https://developer.mobilepay.dk/product"> API section</a> of the portal.


[![](assets/images/Preview-MP-logo-and-type-horizontal-blue.png)](assets/images/Preview-MP-logo-and-type-horizontal-blue.png)

# General description
MobilePay PoS is an API for setting up Merchant's transaction requests on customer's MobilePay apps Instore. The customer is in PoS not required to manually enter any information in the MobilePay app pertaining to the transaction. A transaction request can typically be obtained by the customer by holding the phone near to a Merchant device(Terminal, BLE beacon, etc.) OR scanning a QR code.

There are two types of transactions in MobilePay PoS:
* a payment which is a near instantaneous transfer of funds following the approved payment request 
* a reservation where the transfer of funds happens sometime after the approval of the reservation request. 
Currently MobilePay PoS uses BLE one-way and two-way beacons and QR-codes to set up the transaction requests - the technology choices are not important for the API - however the concept of a beacon ID is central to allow matching of the Customer willing to pay and the Merchant's transaction request.

## Overview of Version 10 changes from Version 8.6 of the MobilePay PoS API
Version 10 of the MobilePay PoS API introduces breaking changes from version 8.6 of the API. The following tables describe the changes in overview:

Notable changes from Version 8.6 to Version 10 of the MobilePay PoS API
* Clients need to implement HTTP 1.1 and JSON standards
* No API key and HMAC validation
* New security setup
* Vendor Identification and Version numbering
* API method naming has changed
* The Error messages are more informative
* There are changes to the payment flow
* There is a new ID-structure
* Documentation is live through a developer website (using OpenAPI standards) and GitHub
* Certification will be done automatically


## Payment option detection

There are three ways in MobilePay PoS for a terminal/client to become aware that MobilePay has be chosen as the payment option:

* User activation
* Notification service
* BLE 2-way communication

**User activation**

This is the default way of detecting MobilePay presence. In a supemarket this can be a button on the ECR that sends the payment request to MobilePay. That is the cashier will ask the customer or infer from the customer's actions which payment option the customer wants to choose and then push the MobilePay button. Another example of user activation is when the customer can choose it herself on a keypad placed on a vending machine for instance. Some vending machines only allow MobilePay to be used and therefore any request for the vending machine product would be inferred as a payment request to MobilePay.

A last example of a button push is in the case of a QR code being displayed in a terminal - in these cases the terminal calls a HTTP GET checkin endpoint in the MobilePay v10 API - this approach ensures that this endpoint is not overloaded with requests.

**Notification service**

Some interfaces do not naturally include a possibility for user activation - for these an endpoint can be exposed by the MobilePay PoS integrator. This endpoint will be called with a checkin Notification in the case a user has checked in. The Notification specification can be obtained following a discussion with MobilePay on the feasibility of this option for the Integrator.

**BLE 2-way communication**

It is possible to get information about check ins via Bluetooth Low Energy - To use this approach the Integrator will need to participate in a co-development with MobilePay.

## Architectual principles
This is a preliminary list of architectual principles.

**Backend has the truth**

An architectual principle in MobilePay PoS is that the Backend has the truth - that means in a situation where certainty is required, for instance is the payment approved, the app and clients will have to wait for confirmation from the backend.

**API versus Implementation**

The API does not describe the abstractions of the underlying backend OR client implementations - instead the API serves as the joint Interface for Backend and Frontend. The rammification for this is that BOTH frontend and backend can move independently from the API however they must always support the API specification and not only support perceived details of current implementations. ANY valid HTTP request must be handled appropiately by the backend and produce a useful informative HTTP response. Any valid HTTP response received in the client must be handled appropriately by the client.

**RESTful API**

The API is defined using the RESTful principles.

## ID-hierarchy

The following diagram shows the ID-Hierarchy of the Master data in MobilePay PoS.

[![](assets/images/Pos-v10-id-hierarchy.png)](assets/images/Pos-v10-id-hierarchy.png)


## Security solution

**Communication security**

MobilePay PoS version 10 uses TLS for communication security and data integrity (secure channel between the client and the API 10 servers). The current TLS version used with the MobilePay PoS solution is 1.2 -  Version 1.3 is finalized and will be implemented within 1-2 years - therefore clients should be able to handle the switch to 1.3 on the fly or with minimal changes.

**Integrator Authorization**

The MobilePay API Gateway is ensuring the authentication of all PoS API request. 
In order to be granted access to the MobilePay PoS API each integrator/vendor will have to enroll their clients as a client (called App) in our API Gateway Developer Portal (see section below for more information about it).

Creating an app in MobilePay Developer portal will create a client Id that should be used in all calls the the MobilePay PoS API in the following way:


Example with a Curl request:

> --header 'X-IBM-Client-Id: 80e0075c-d0b5-4b74-a466-ecaca65234b0'

## Vendor, Merchant and version Identification
The Client Id is used by the MobilePay PoS backend to identify the client on the application level - the backend expects that different clients use different ClientId thereby requiring following the steps in the developer portal for each client.

 A Header containing the Client version is also required, the Client version is a 3 dimensional number Major.Minor.Build.

* Major version represents major changes to the client version, perhaps representing breaking changes on the clients other interfaces or representing major changes communicated to merchants - A major change requires re-certification.
* Minor version represents minor changes to the client version, changes that introduces new features or a change in the way internal logic is handled, minor version changes are perhaps not communicated to merchants - a minor change requires re-certification.
* Build version represents a new build of the client, the include minor bug-fixes and changes of the lowest magnitude. A new build version does not require a re-certification

Certification requirements in regard to changes to Client Id or Client Version

* Changes in ClientId, Major version or Minor version requires a new Certification
* Changes in Build version does not requires a new Certification

Example with a Curl request:

> --header 'X-MP-Client-Version: 2.1.1'


## Automatic self Certification
The certification process changes with API v10 - for the new API all minor versions of clients must be certified, MobilePay will provide an automatic certification process - where it will be possible for most integrators to create a fully automated self-certification. The certification will be concluded with an automated report on how the certification went.

Further details on self certification will follow in December 2019.

## The MobilePay Developer Portal
The MobilePay Developer Portal is a site where you will be able to find information about the products and available APIs and their documentations.
It exposes live documentation that can be used for development and error correction. Access to the portal can be requested by writing to the following email address developer@mobilepay.dk .

The MobilePay Developer Portal is available at the following addresses:

| Environment  | Endpoint |
|--------------|-------------|
| Sandbox/Test | https://sandbox-developer.mobilepay.dk/ |
| Production   | https://developer.mobilepay.dk |

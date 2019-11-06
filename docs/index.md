
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

## Overview of Version 10 changes from Version 8.6 of the MobilePay PoS API
Version 10 of the MobilePay PoS API introduces breaking changes from version 8.6 of the API. The following list describes the changes in overview:

Notable changes from Version 8.6 to Version 10 of the MobilePay PoS API
* Clients need to implement HTTP 1.1 and JSON standards
* No API key and HMAC validation
* New security setup using access tokens
* Vendor Identification and Version numbering
* API method naming has changed
* The Error messages are more informative
* There are minor changes to the payment flow
* There is a new ID-structure
* Documentation is live through a developer website (using OpenAPI standards) and GitHub
* Certification will be done automatically


## ID-hierarchy

The following diagram shows the ID-Hierarchy of the Master data in MobilePay PoS.

[![](assets/images/Pos-v10-id-hierarchy.png)](assets/images/Pos-v10-id-hierarchy.png)


## Vendor, Merchant and version Identification
# The Client Id is used by the MobilePay PoS backend to identify the client on the application level - the backend expects that different clients use different ClientId thereby requiring following the steps in the developer portal for each client.

Headers containing the Client Name and the Client Version are required. The Client Name is suitable name used for the client, preferable the name that the Integrator uses in their own communication, this way support communication between Merchant, Integrator and MobilePay uses the same name which should aid in removing confusion in the support sitiation. The Client version is a 3 dimensional number Major.Minor.Build - it is recommended to use the power of the Client Version Header, as this will be used by MobilePay to block versions of clients that are not certified and/or are misbehaving. An example of misbehavior would be spamming irrelevant HTTP calls that endanger fast response times for other clients.

* Major version represents major changes to the client version, perhaps representing breaking changes on the clients other interfaces or representing major changes communicated to merchants - A major change requires re-certification.
* Minor version represents minor changes to the client version, changes that introduces new features or a change in the way internal logic is handled, minor version changes are perhaps not communicated to merchants - a minor change requires re-certification.
* Build version represents a new build of the client, the include minor bug-fixes and changes of the lowest magnitude. A new build version does not require a re-certification

Certification requirements in regard to changes to Client Name and Client Version

* Changes in Client Name, Major version or Minor version requires a new Certification
* Changes in Build version does not requires a new Certification

Example with a Curl request:

````
--header 'X-MP-Client-Name: MobilePay Pos Client Reference Implementation'
--header 'X-MP-Client-Version: 2.1.1'
````

## Automatic self Certification
The certification process changes with API v10 - for the new API all minor and major versions of clients must be certified, MobilePay will provide an automatic certification process - where it will be possible for most integrators to create a fully automated self-certification. The certification will be concluded with an automated report on how the certification went.

Further details on self certification will follow in December 2019.

## The MobilePay Developer Portal
The MobilePay Developer Portal is a site where you will be able to find information about the products and available APIs and their documentations.
It exposes live documentation that can be used for development and error correction. Access to the portal can be requested by writing to the following email address developer@mobilepay.dk .

The MobilePay Developer Portal is available at the following addresses:

| Environment  | Endpoint |
|--------------|-------------|
| Sandbox/Test | [https://sandbox-developer.mobilepay.dk/](https://sandbox-developer.mobilepay.dk/) |
| Production   | [https://developer.mobilepay.dk](https://developer.mobilepay.dk) |

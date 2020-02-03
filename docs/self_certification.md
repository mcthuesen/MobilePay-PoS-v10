# <a name="self_certification"></a> Self Certification

The certification process changes with MobilePay PoS API v10. For the new API all Major and Minor versions of clients 
must be certified. MobilePay provides an automatic certification process where it is possible 
for most integrators to create a fully automated self-certification. The certification concludes 
with an automated report on how the certification went.

The Self Certification process has four steps: Identification, Selection, Certification and Approval.

## Identification Step
In the first step the Integrator identifies themselves in the tool. The following information is needed:
* Integrator ID - ID received from MobilePay per mail, which identifies the Integrator organisation itself. Each Integrator should only have one Integrator ID.
* Client ID - ID created on the MobilePay Developer Portal which identifies the client to be certified. Each Integrator is allowed to create multiple Client IDs, however it is also acceptable to have just one Client ID.
* Version numbering - The three dimensional number that defines the version of the Client that needs to be certified. See [Client Identification](api_principles#client_identification)
* Access token - The token that grants access to the MobilePay PoS API v10. The token can be obtained through an HTTP endpoint (Link will follow).

[![](assets/images/identificationstep.PNG)](assets/images/identificationstep.PNG)

## Selection Step
In the second step the Integrator selects which major features to certify. There are six major features in MobilePay PoS API v10:
* Onboarding - The neccesary proces of creating a Point-of-Sale on the MobilePay backend
* Payment - Certification in sections of the API neccesary for doing a simple payment.
* Prepared Payment - Certification in sections of the API neccesary for doing a prepared payment.
* Refund - Certification in sections of the API neccesary for doing a refund.
* Loyalty - Certification in sections of the API neccesary for handling Loyalty programmes.
* Payment Restrictions - Certification in sections of the API neccesary for handling restrictions to payments.

[![](assets/images/selectionstep.PNG)](assets/images/selectionstep.PNG)

## Certification Step
In the third step the integrator goes through all the different certifiction cases neccesary using his client. In this step it might be neccesary to operate the client to go through the different steps of a certification case.

[![](assets/images/certificationstep.PNG)](assets/images/certificationstep.PNG)

## Approval step
In the Fourth and final step the Integrator gets a report informing them of the client performance. In the case the Certification is passed - it is now possible for the client to access production. In the case of a failure there will be information of which steps failed.

In general we urge all integrators to use this tool to do continuous testing - it is a requirement to certify when upgrading Major or Minor versions, it is recommended to use the tool when making new build versions as well. The tool will never retract a certification to a client version it has already certified. Retraction of a certification will only be done after a individual evaluation by MobilePay based on input from production. 



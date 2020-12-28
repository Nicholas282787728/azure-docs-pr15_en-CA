<properties 
   pageTitle="Create a Trading Partner Agreement in Azure App Service | Microsoft Azure" 
   description="Create Trading Partner Agreements" 
   services="logic-apps" 
   documentationCenter=".net,nodejs,java" 
   authors="rajram" 
   manager="erikre" 
   editor=""/>

<tags
   ms.service="logic-apps"
   ms.devlang="multiple"
    ms.topic="get-started-article"
   ms.tgt_pltfrm="na"
   ms.workload="integration" 
   ms.date="08/23/2016"
   ms.author="rajram"/>

# <a name="creating-a-trading-partner-agreement"></a>Creating a Trading Partner Agreement   

[AZURE.INCLUDE [app-service-logic-version-message](../../includes/app-service-logic-version-message.md)]

Trading partners are the entities involved in B2B (Business-to-Business) communications. When two partners establish a relationship, this is referred to as an *Agreement*. The agreement defined is based on the communication the two partners wish to achieve and is protocol or transport specific. The various B2B protocols and transports supported by Azure App Service include:

- AS2 (Applicability Statement 2)
- EDIFACT (United Nations/Electronic Data Interchange For Administration, Commerce and Transport (UN/EDIFACT))
- X12 (ASC X12)

### <a name="biztalk-api-apps-that-support-b2b-scenarios"></a>BizTalk API Apps that support B2B scenarios
The following API Apps enable these capabilities using a rich and intuitive experience in the Azure Portal:


## <a name="biztalk-trading-partner-management-tpm"></a>BizTalk Trading Partner Management (TPM)
- Creation and management of Partners, Profiles & Identities
- Storage and management of EDI Schemas
- Storage and management of certificates (used in AS2 protocol)
- Creation and management of AS2 Agreements
- Creation and management of EDIFACT Agreements (includes batching on the send side)
- Creation and management of X12 Agreements (includes batching on the send side)

![][1]


## <a name="as2-connector"></a>AS2 Connector
- Executes AS2 Agreements as defined in the related TPM API App instance
- Surfaces AS2 processing/tracking information for troubleshooting


## <a name="biztalk-edifact"></a>BizTalk EDIFACT
- Executes EDIFACT Agreements as defined in the related TPM API App instance
- Surfaces EDIFACT processing/tracking information for troubleshooting
- Provides state management of batches (start and stop) as defined in EDIFACT Agreement(s) in the related TPM API App instance


## <a name="biztalk-x12"></a>BizTalk X12
- Executes X12 Agreements as defined in the related TPM API App instance 
- Surfaces X12 processing/tracking information for troubleshooting
- Provides state management of batches (start and stop) as defined in X12 Agreement(s) in the related TPM API App instance

As previously stated, the AS2, X12, and EDIFACT API Apps require a TPM API App to function as expected.


## <a name="getting-started"></a>Getting Started
To create trading partner agreements:

1. Create an instance of the **BizTalk Trading Partner Management** connector. This requires a blank SQL Database to function. Before starting be sure to have a blank database available and ready for use.
2. Upload schemas and certificates as required by the agreements. Do this by browsing the TPM instance created and stepping into the ‘Schemas’ and/or ‘Certificates’ part
3. Browse to the TPM instance created and step into the **Partners** part
4. Create partners as desired. Also edit the profile(s) as appropriate and add the required identities
5. Now use the **Agreements** part to create agreements. When you create an Agreement, you must select the protocol that will be used. The remaining configuration options are based on the protocol that you selected.

![][2]

![][3]

<!--Image references-->
[1]: ./media/app-service-logic-create-a-trading-partner-agreement/TPMResourceView.png
[2]: ./media/app-service-logic-create-a-trading-partner-agreement/ProtocolSelection.png
[3]: ./media/app-service-logic-create-a-trading-partner-agreement/X12AgreementCreation.png
 
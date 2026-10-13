---
title: Connect to Azure Communication Services
description: Learn how to connect to Azure Communication Services by using a new or existing resource to configure the voice channel.
ms.date: 10/13/2026
ms.topic: concept-article
author: neeranelli
ms.author: nenellim
ms.reviewer: nenellim
ms.custom:
  - bap-template
  - ai-gen-docs-bap
  - ai-gen-desc
  - ai-seo-date:09/29/2023
---

# Connect to Azure Communication Services


[!INCLUDE[cc-feature-availability-embedded-yes](../../includes/cc-feature-availability-embedded-yes.md)]

> [!IMPORTANT]
> Microsoft retires certain standalone Azure Communication Services capabilities on September 30, 2028. This retirement affects voice channels that connect through Azure Communication Services (Direct Offer or Direct Routing). Existing configurations remain fully supported until that date, but we recommend that you start planning your migration to Microsoft Teams Phone extensibility now.
>
> Since September 30, 2026, organizations that don't already have an Azure Communication Services resource can't acquire phone numbers or port numbers into Azure Communication Services. For new deployments, we recommend that you [configure Teams Phone in the voice channel](https://learn.microsoft.com/en-us/dynamics365/contact-center/administer/configure-teams-phone-in-voice-channel).
>
> Learn more in [Plan migration from Azure Communication Services](https://learn.microsoft.com/en-us/dynamics365/contact-center/administer/migrate-from-azure-communication-services) and [Azure Communication Services retirement and breaking changes](https://learn.microsoft.com/en-us/azure/communication-services/acs-retirement-and-breaking-changes-guide).

The voice channel in Dynamics 365 is built over Azure Communication Services. This capability lets you provision phone numbers for your business by connecting to Azure Communication Services. However, to acquire phone numbers, you must first establish connection with Azure Communication Services. You can do this in the following ways:

- [Connect using a new Azure resource](voice-channel-connect-new-resource.md)
- [Connect using an existing Azure resource](voice-channel-connect-existing-resource.md)

You can also [import phone numbers](voice-channel-sync-from-acs.md) or [connect your existing telephony infrastructure with Azure](voice-channel-bring-your-own-number.md).

> [!IMPORTANT]
>
> - Avoid reusing [Azure Communication Services resources](/azure/communication-services/quickstarts/create-communication-resource) across multiple instances. For optimal performance and to avoid issues, map one application instance only with one Azure Communication Services resource.
> - After you connect to a resource in a Power Platform environment, the phone numbers purchased via the resource that are linked to the Power Platform environment can't be transferred or migrated to another environment.
> - We recommend that you [test your network](https://azurecommdiagnostics.net) before you connect to Azure Communication Services.


### Related information

[Overview of the voice channel](voice-channel.md)  
[Connect using a new Azure resource](voice-channel-connect-new-resource.md)  
[Connect using an existing Azure resource](voice-channel-connect-existing-resource.md)  
[Import phone numbers](voice-channel-sync-from-acs.md)   
[Disconnect from Azure Communication Services](voice-channel-disconnect-from-acs.md)  
[Manage phone numbers](voice-channel-manage-phone-numbers.md)  
[Set up outbound calling](voice-channel-outbound-calling.md)  
[Bring your own carrier](voice-channel-bring-your-own-number.md)  
[Integrate a third-party IVR system with voice channel](voice-channel-contextual-transfer-external-ivr.md)  
[Plan migration from Azure Communication Services](https://learn.microsoft.com/en-us/dynamics365/contact-center/administer/migrate-from-azure-communication-services)  

[!INCLUDE[footer-include](../../includes/footer-banner.md)]

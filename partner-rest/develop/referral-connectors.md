---
title: Referral-connectors.
description: Synchroniseer partner referrals met Dynamics 365 CRM-leads met behulp van Microsoft Flow.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a62023feb03114bb7ba1136b7700875f24c2e01
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770395"
---
# <a name="referral-connectors"></a>Referral-connectors

U kunt referentie connectors gebruiken voor het synchroniseren van partner verwijzingen met CRM-leads (Customer Relationship Management). U kunt een referentie connector maken met [Microsoft flow](https://flow.microsoft.com) als het HTTPS-eind punt om partner verwijzingen te ontvangen. U kunt vervolgens de verwijzing die door de stroom is ontvangen, naar een CRM-systeem schrijven als lead.

## <a name="prerequisites"></a>Vereisten

* Microsoft Flow-abonnement
  * Account met beheerders toegang tot dit abonnement
* Azure Active Directory (Azure AD) toepassings-id, gebruikers-id, wacht woord en Tenant-ID (gebruikt voor toegang tot de partner-API). Zie [partner verificatie](api-authentication.md)voor meer informatie over de installatie-instructies.
* [Azure function-app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) -abonnement.
* [Partner centrum webhook gebeurtenis](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) abonnement op [verwijzing gemaakt](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) en [bijgewerkte](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) gebeurtenissen door verwijzing.
* [Micro soft Dynamics 365](https://dynamics.microsoft.com) -abonnement
  * Module Sales ingeschakeld
  * Account met beheerders toegang tot dit abonnement

## <a name="flow-overview"></a>Stroom overzicht

Verwijzingen worden met de volgende stroom in het CRM geïmporteerd:

1. De partner stelt een webhook in voor het ontvangen van verwijzings meldingen.
2. De partner registreert de webhook met het partner centrum. De partner is ook geabonneerd op webhook-gebeurtenissen voor wanneer verwijzingen worden gemaakt of bijgewerkt.
3. Referral client maakt of update een verwijzing.
4. Partner Center-webhooksysteem controles voor de registratie van de partner en verzenden van een melding naar de webhook.
5. Webhook ontvangt de melding.
6. Flow-document in micro soft Flow gebruikt een token om een aanroep naar de Partner Center-Referral-API te maken.
7. Het eind punt van de stroom haalt de verwijzing op.
8. Met Flow-eind punt wordt de CRM-lead gemaakt.

![Stroom diagram met de stappen in deze sectie voor het importeren van partner referrals in CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a>Stroom document proces

Het stroom document voor een verwijzings Connector synchroniseert een partner referentie met een CRM-lead van Dynamics 365.

1. Connector haalt een token op waarmee verbinding moet worden gemaakt `https://api.partner.microsoft.com/v1.0/engagements/referrals` .
2. De connector verkrijgt de Referral die de connector heeft geactiveerd met behulp van `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .
3. Connector maakt verbinding met Dynamics 365.
4. Connector maakt een nieuwe lead of werkt een bestaande lead bij met de meest recente informatie over de verwijzing.
5. Connector updates Referral met de meest recente updates van de CRM-lead.

![Stroom diagram met de stappen in deze sectie voor het proces van het stroom document.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a>Voor beeld van referentie connector

De volgende voor *beeld-verwijzings connector* laat zien hoe u partner Center-verwijzingen naar CRM-leads in Dynamics 365 kunt synchroniseren.

> [!IMPORTANT]
> U kunt schrijven naar verschillende CRMs door de [flow-connectors](https://flow.microsoft.com/en-us/connectors/) in de voorbeeld code te vervangen.

### <a name="import-flow-synchronization-package"></a>Stroom synchronisatie pakket importeren

Down load en importeer het *voorbeeld code pakket* in Microsoft flow en maak verbinding met Dynamics 365:

1. Down load het [stroom synchronisatie pakket](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) van de [github opslag plaats](https://github.com/microsoft/Partner-Center-Referrals).
2. Meld u aan bij [Microsoft flow](https://flow.microsoft.com) met de juiste referenties.
3. Kies **mijn stromen** in het navigatie menu. Kies vervolgens **importeren**.
4. Selecteer op de pagina **pakket importeren** het stroom synchronisatie pakket dat u hebt gedownload. Kies vervolgens **uploaden**.

    ![Scherm pakket importeren voor pakket bestanden](../images/importPackage.png)

5. Nadat het uploaden van het pakket is voltooid, gaat u naar het pakket dat u hebt geüpload in de inhoud van het **beoordelings pakket** .

    ![Details van het scherm pakket importeren](../images/importPackageDetails.png)

6. Kies de **actie** knop (potlood pictogram) voor het geüploade pakket. Hiermee opent u de Blade **import instellingen** .
7. Kies uw **installatie** type.

    * Als u een nieuwe stroom wilt maken, selecteert u **maken als nieuw** en voert u een nieuwe **resource naam** in.
    * Als u een bestaande stroom met dezelfde naam wilt bijwerken, selecteert u **bijwerken**.

    ![Een nieuw pakket-scherm maken of bijwerken](../images/CreateNewConnection.png)

8. Zoek op de pagina **pakket importeren** uw Dynamics 365-verbinding in het gedeelte **pakket inhoud beoordelen** onder **gerelateerde resources**.
9. Kies de **actie** knop (potlood pictogram) voor uw Dynamics 365-verbinding. Hiermee opent u de Blade **import instellingen** voor deze gerelateerde resource.
10. Kies **Nieuw maken** om een nieuwe Dynamics 365-verbinding te maken of selecteer een bestaande verbinding.
11. Controleer of op de pagina **pakket importeren** nu het geselecteerde type stroom installatie en Dynamics 365-verbinding worden weer gegeven. Kies vervolgens **importeren**.

    ![Scherm pakket status importeren](../images/importStatus.png)

12. Controleer of de stroom resource nu is gemaakt of bijgewerkt.

### <a name="configure-flow-parameters"></a>Flow-para meters configureren

De para meters van uw stroom resource configureren:

1. In [Microsoft flow](https://flow.microsoft.com)kiest u **mijn stromen** in het navigatie menu.
2. Kies de stroom resource die u hebt gemaakt of bijgewerkt in de vorige sectie.
3. Op de pagina stroom kiest u **stroom bewerken**.
4. Kies de ID-variabele van de **Aad-toepassing (client)** en voer de id van uw Azure AD-toepassing in.
5. Kies de variabele **UserID** en voer uw gebruikers-id in.
6. Kies de variabele **userPassword** en voer uw gebruikers wachtwoord in.
7. Selecteer de ID-variabele voor **Aad-Directory (Tenant)** . Voer de Tenant-ID van uw Azure AD-toepassing in.
8. Kies **Opslaan** om uw stroom op te slaan.

    ![Scherm instellingen van stroom variabelen](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a>De call back verifiëren

De Terugbel gebeurtenis van het partner centrum verifiëren:

> [!TIP]
> Zie de [voorbeeld functie-app code](#sample-function-app-code) in de volgende sectie voor een voor beeld.

1. [Maak een Azure-functie-app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) die [de call back gebeurtenis verifieert vanuit het partner centrum](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).

    1. Controleer of de vereiste headers aanwezig zijn (**autorisatie**, **x-MS-Certificate-URL** en **x-MS-Signature-algoritme**).
    2. Down load het certificaat dat wordt gebruikt om de inhoud te ondertekenen (**x-MS-Certificate-URL**).
    3. Controleer de certificaat keten.
    4. Controleer de **organisatie** van het certificaat.
    5. Lees de inhoud met UTF-8-code ring in een buffer.
    6. Maak een RSA crypto-provider.
    7. [Controleer of de hand tekening overeenkomt](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) met wat is ondertekend met het opgegeven hash-algoritme (bijvoorbeeld sha256).
    8. Als de verificatie slaagt, wordt er een **OK** -bericht weer gegeven.

2. Noteer de gegenereerde call back-URI voor het HTTP-eind punt van uw functie-app. Deze URI wordt weer gegeven wanneer u de functie-app maakt. U kunt deze URI ook vinden op de Azure-resource pagina van de functie-app.
3. Bewerk in [Microsoft flow](https://flow.microsoft.com)de stroom ' partner referral to micro soft Dynamics CRM lead ' die u hebt geïmporteerd in het gedeelte *[import flow Synchronization package](#import-flow-synchronization-package)*.

    1. Voeg de waarde van de URI van de functie-app toe aan de stap ' validatie van webhook-certificaat '.
    2. Kopieer en plak de call back-URI van uw functie-app in het stroom document.
    3. Sla het stroom document op.

#### <a name="sample-function-app-code"></a>Code voor voorbeeld functie-app

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a>Stroom registreren met partner centrum

Registreer uw stroom resource bij het partner centrum om de stroom te activeren en de gebeurtenissen van de webhook te ontvangen:

1. In [Microsoft flow](https://flow.microsoft.com)kiest u **mijn stromen** in het navigatie menu.
2. Kies de stroom die u hebt gemaakt of bijgewerkt.
3. Op de pagina stroom kiest u **stroom bewerken**.
4. Kopieer de **http post-URL** van de stroom en sla deze op. U moet deze URL gebruiken om de stroom te activeren.
5. [Meld u aan om webhook-gebeurtenissen te ontvangen](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) wanneer verwijzingen worden gemaakt of bijgewerkt. Gebruik de volgende hoofd indeling:

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```

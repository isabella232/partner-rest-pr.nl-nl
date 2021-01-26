---
title: Een lijst met leads en kansen ophalen
description: Een lijst met leads en verkoop kansen ophalen met behulp van de partner-API.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 46243f8484a8068827e24e1d03f39ffddade1dbf
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770420"
---
# <a name="get-the-list-of-leads-and-opportunities"></a>De lijst met leads en verkoopkansen ophalen

Van toepassing op:

- Partner-API

 In dit onderwerp wordt uitgelegd hoe u de lijst met leads kunt ophalen die zijn ontvangen van de micro soft Solution Provider-pagina en verkoop kansen die zijn ontvangen van micro soft-verkopers of andere partners. Hiermee haalt u ook de lijst met verkoop kansen of pijplijn deals op die door uw organisatie zijn gemaakt.

> [!Note]
> Leads die zijn ontvangen van de micro soft Commercial Marketplace (Azure Marketplace en AppSource) worden niet ondersteund.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [partner API-verificatie](api-authentication.md). Dit scenario ondersteunt verificatie met app + gebruikers referenties.
- Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, referentie beheerder of verwijzings gebruiker.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Syntaxis van aanvraag

| Methode  | Aanvraag-URI                                                    |
|:--------|:---------------------------------------------------------------|
| **Toevoegen** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a>Ondersteunde OData-bewerkingen

| Naam     | Beschrijving     | Vereist    | Voorbeeld                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| $select  | Velden selecteren  | No          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| $filter  | Filtert resultaten | Aanbevolen | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| $orderby | Resultaten van orders  | Aanbevolen | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a>Ondersteunde OrderBy-para meters

Gebruik de volgende $orderby para meters om de lijst met leads en kansen te sorteren

| Naam            | Type     | Description                                       |
|:----------------|:---------|:--------------------------------------------------|
| createdDateTime | DateTime | Aanmaak datum en-tijd van de lead of kans |
| updatedDateTime | DateTime | De datum en tijd van de lead of de opportuniteit bijwerken   |

### <a name="request-headers"></a>Aanvraagheaders

Zie [partner rest headers](headers.md) voor meer informatie.

### <a name="request-body"></a>Aanvraagbody

Geen.

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a>REST-antwoord

Als dit lukt, bevat de antwoord tekst een verzameling [leads en/of verkoop kansen](referral-resources.md).

### <a name="response-success-and-error-codes"></a>Geslaagde en fout codes

Elk antwoord wordt geleverd met een [HTTP-status code](error-codes.md) die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing. Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.

### <a name="response-example"></a>Voorbeeld van antwoord

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
  "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
  "@odata.count": 1,
  "value": [
    {
      "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
      "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
      "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
      "organizationName": "Contoso Company",
      "createdDateTime": "2020-10-30T21:03:00.0000000Z",
      "updatedDateTime": "2020-10-30T21:03:00.0000000Z",
      "status": "New",
      "substatus": "Pending",
      "qualification": "Direct",
      "type": "Independent",
      "direction": "Incoming",
      "customerProfile": {
        "name": "Fabrikam Customer Inc",
        "address": {
          "addressLine1": "One Microsoft Way",
          "addressLine2": "",
          "city": "Redmond",
          "state": "WA",
          "postalCode": "98052",
          "country": "US"
        }
      },
      "details": {
        "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
        "dealValue": 10000,
        "currency": "USD",
        "closingDateTime": "2020-12-01T00:00:00Z",
        "requirements": {
            "industries": [ { "id": "Education" } ],
            "products": [ { "id": "Microsoft365" } ],
            "services": [ { "id": "LearningAndCertification" } ],
            "solutions": [ { "id": "SOL-Microsoft365", "name": "Microsoft365" }
          ]
        }
      },
      "links": {
        "relatedReferrals": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
          "method": "GET"
        },
        "self": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
          "method": "GET"
        }
      }
    }
  ],
  "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxX"
}
```

Gebruik de `@odata.nextLink` om de volgende pagina met resultaten op te halen.

> [!Note]
> De velden in het bovenstaande voor beeld illustratration zijn niet volledig. Het daad werkelijke API-antwoord bevat meer velden, zoals de klant en partner teams. Zie [Referral resources](referral-resources.md)voor een volledige lijst met ondersteunde velden.

## <a name="sample-requests"></a>Voorbeeld aanvragen

1. Hiermee worden de Top 10 van de meest recente inkomende mogelijkheden voor co-sell opgehaald. De aanvraag haalt verkoop kansen op die zijn geïnitieerd door een vertegenwoordiger van micro soft of een andere partner, waarbij uw organisatie wordt uitgenodigd om deel te nemen aan een mede-verkoop activiteit.
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. Haalt de meest recente inkomende leads en verkoop kansen op waarop niet is gereageerd.  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > Als u niet binnen de toegewezen tijd (momenteel 14 dagen) op een lead of verkoop kans reageert, worden deze gearchiveerd als verlopen en wordt micro soft of de partner die u deze mogelijkheid heeft gestuurd.

3. Hiermee worden de meest recente actieve verkoop kansen opgehaald die door uw organisatie zijn gestart en aan een specifieke verkoper worden door gegeven.
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```
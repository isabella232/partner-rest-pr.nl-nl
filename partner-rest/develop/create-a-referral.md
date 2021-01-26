---
title: Een verwijzing maken
description: Maak onafhankelijke of gedeelde verwijzingen in de partner-API.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770408"
---
# <a name="create-a-referral"></a>Een verwijzing maken

Van toepassing op:

- Partner-API

In dit onderwerp wordt uitgelegd hoe u een verwijzing maakt. Er zijn twee soorten [ReferralType](referral-resources.md#referraltype):

1. Onafhankelijk: een verwijzing is zichtbaar voor één partner.
2. Gedeeld: wanneer een verwijzing zichtbaar is voor twee partijen die samen werken. Als micro soft en een partner bijvoorbeeld samen werken in een mede-verkoop transactie, kan een verwijzing tussen beide partijen worden gedeeld. Zie de sectie [een gedeelde verwijzing maken](#create-a-shared-referral)voor meer informatie.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [partner API-verificatie](api-authentication.md). Dit scenario ondersteunt verificatie met app + gebruikers referenties.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Syntaxis van aanvraag

| Methode  | Aanvraag-URI                                                  |
|---------|--------------------------------------------------------------|
| **Verzenden** | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a>Aanvraagheaders

- Zie de REST-headers van de [partner-API](headers.md) voor meer informatie.

### <a name="request-body"></a>Aanvraagbody

In deze tabel worden de [verwijzings](referral-resources.md) eigenschappen in de hoofd tekst van de aanvraag voor een gloed nieuwe verwijzing beschreven.

| Eigenschap            | Type                                                                 | Beschrijving                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Name                | tekenreeks                                                               | De naam van de verwijzing.                                                                                            |
| ExternalReferenceId | tekenreeks                                                               | Een externe ID voor de verwijzing. Bijvoorbeeld uw eigen Dynamics 365-lead-of verkoop kans-ID.                   |
| Status              | [ReferralStatus](referral-resources.md#referralstatus)               | Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven.          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de substatus van de verwijzing aangeven.       |
| StatusReason        | tekenreeks                                                               | Een beschrijvende bericht over de status. Leg bijvoorbeeld uit waarom de Referral verloren is gegaan.                            |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Hiermee wordt het verwijzings type aangeduid. **Vereist.**                                                                                        |
| Kwalificatie       | [ReferralQualification](referral-resources.md#referralqualification) | Vertegenwoordigt de kwaliteit van de verwijzing.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Contact gegevens van de klant.  **Vereist.**                                                                                      |
| Toestemming             | [Toestemming](referral-resources.md#consent)                             | Markering van toestemming voor het delen van gegevens met andere organisaties, zodat ze contact kunnen opnemen met de gebruikers. **Vereist.**               |
| Details             | [ReferralDetails](referral-resources.md#referraldetails)             | Details van klant, notities, deal waarde, valuta afsluitings datum. **Vereist.**                                                           |
| Team                | [Lid](referral-resources.md#member)                               | Vertegenwoordigt gebruikers in de organisaties die betrokken zijn bij de partner engagement.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement. |
| Doel         | [ReferralTarget](referral-resources.md#target)        | Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.  |

#### <a name="status--substatus-transition-states"></a>Status & overgangs toestanden voor substatus

| Status | Status overgang toegestaan | Toegestane substatus            |
|--------|---------------------------|------------------------------|
| Nieuw    | Nieuw, actief, gesloten       | In behandeling, ontvangen            |
| Actief | Actief, gesloten            | Geaccepteerd                     |
| Gesloten | Gesloten                    | Gewonnen, verloren, afgewezen, verlopen |

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    }
}
```

## <a name="rest-response"></a>REST-antwoord

Als dit lukt, retourneert deze methode de gevulde [verwijzings](referral-resources.md) bron in de antwoord tekst.

### <a name="response-success-and-error-codes"></a>Geslaagde en fout codes

Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing. Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen. Zie [fout codes](error-codes.md)voor de volledige lijst.

### <a name="response-example"></a>Voorbeeld van antwoord

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```

## <a name="create-a-shared-referral"></a>Een gedeelde verwijzing maken

Er zijn twee stappen voor het maken van een verwijzing naar het **gedeelde** [verwijzings type](referral-resources.md#referraltype).

1. [Uw gedeelde Referral maken](#create-your-referral)
2. [Een verbonden verwijzing maken voor de tweede partij](#create-a-connected-referral)

In het volgende diagram ziet u deze twee stappen bij het maken van een gedeelde verwijzing.

![Stroom diagram met een gedeelde Referral met 2 referrals die zijn verbonden via de micro soft partner-API](../images/SharedReferral.png)

### <a name="create-your-referral"></a>Uw verwijzing maken

1. Een verwijzing maken waarbij [ReferralType](referral-resources.md#referraltype) is ingesteld op gedeeld.
2. Kopieer de **engagementId** van het retour antwoord.

Voor beeld van [ReferralTarget](referral-resources.md#target) voor verwijzing

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a>Een verbonden Referral maken

1. Maak een andere referral voor micro soft.
2. Neem de **enagementId** op uit uw referral, zodat deze aan elkaar zijn gekoppeld.

[ReferralTarget](referral-resources.md#target) -voor beeld voor micro soft Referral

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```
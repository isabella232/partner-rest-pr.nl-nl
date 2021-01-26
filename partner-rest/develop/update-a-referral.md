---
title: Een lead of verkoop kans bijwerken (verouderd)
description: Hiermee kunt u de details van de lead of de opportuniteit bijwerken. Deze methode voor het bijwerken van een lead of verkoop kans is verouderd en we recommmend in plaats daarvan de aanroep van de PATCH te gebruiken.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770425"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a>Een lead of verkoop kans bijwerken (verouderd)

Van toepassing op:

- Partner-API

In dit onderwerp wordt uitgelegd hoe u de lead-of verkoopkansgegevens, zoals de deal waarde, de geschatte Sluitings datum, of de verkoop stadia onder andere details bijwerkt. 


> [!IMPORTANT]
Deze methode voor het bijwerken van een lead of verkoop kans is verouderd en we recommmend in plaats daarvan de aanroep van de [patch](patch-a-referral.md) te gebruiken.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [partner API-verificatie](api-authentication.md). Dit scenario ondersteunt verificatie met app + gebruikers referenties.
- Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, referentie beheerder of verwijzings gebruiker.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Syntaxis van aanvraag

| Methode  | Aanvraag-URI                                                       |
|---------|-------------------------------------------------------------------|
| **PUT** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a>Aanvraagheaders

- Zie de REST-headers van de [partner-API](headers.md)voor meer informatie.

> [!IMPORTANT]
> Zorg ervoor dat u de header **if-match** instelt.

### <a name="request-body"></a>Aanvraagbody

In deze tabel worden de [verwijzings](referral-resources.md) eigenschappen in de hoofd tekst van de aanvraag beschreven.

| Eigenschap            | Type                                                                 | Description                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Id                  | tekenreeks                                                               | De ID voor deze verwijzing.                                                                                            |
| EngagementId        | tekenreeks                                                               | De EngagementID voor deze verwijzing. Meerdere verwijzingen kunnen worden gekoppeld aan één EngagementID                    |
| Name                | tekenreeks                                                               | De naam van de verwijzing.                                                                                            |
| ExternalReferenceId | tekenreeks                                                               | Een externe ID voor de verwijzing. Voor beeld: uw eigen Dynamics 365-ID voor potentiële klanten en verkoop kansen opslaan                    |
| CreatedDateTime     | teken reeks in UTC-datum tijd notatie                                       | De datum waarop de verwijzing is gemaakt.                                                                                   |
| UpdatedDateTime     | teken reeks in UTC-datum tijd notatie                                       | De datum waarop de verwijzing voor het laatst is bijgewerkt.                                                                              |
| ExpirationDateTime  | teken reeks in UTC-datum tijd notatie                                       | De datum waarop de verwijzing verloopt.                                                                                   |
| Status              | [ReferralStatus](referral-resources.md#referralstatus)               | Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven.          |
| Substatus           | [ReferralSubstatus](referral-resources.md#referralsubstatus)         | Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de verwijzings substatus aangeven.      |
| StatusReason        | tekenreeks                                                               | Een beschrijvende bericht over de status. Leg bijvoorbeeld uit waarom de Referral verloren is gegaan.                              |
| ReferralType        | [ReferralType](referral-resources.md#referraltype)                   | Hiermee wordt het verwijzings type aangeduid.                                                                                        |
| Kwalificatie       | [ReferralQualification](referral-resources.md#referralqualification) | Vertegenwoordigt de kwaliteit van de verwijzing.                                                                              |
| CustomerProfile     | [CustomerProfile](referral-resources.md#customerprofile)             | Contact gegevens van de klant.                                                                                        |
| Toestemming             | [Toestemming](referral-resources.md#consent)                             | Markering van toestemming voor het delen van gegevens met andere organisaties, zodat ze contact kunnen opnemen met de gebruikers.                |
| Details             | [ReferralDetails](referral-resources.md#referraldetails)             | Details van klant, notities, deal waarde, valuta afsluitings datum.                                                          |
| Team                | [Lid](referral-resources.md#member)                               | Vertegenwoordigt gebruikers in de organisaties die betrokken zijn bij de partner engagement.                                   |
| InviteContext       | [InviteContext](referral-resources.md#invitecontext)                 | Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement. |
| Doel         | [ReferralTarget](referral-resources.md#target)        | Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.  |

### <a name="status-and-substatus-transition-states"></a>Status en overgang van de substatus

| Status | Status overgang toegestaan | Toegestane substatus            |
|--------|---------------------------|------------------------------|
| Nieuw    | Nieuw, actief, gesloten       | In behandeling, ontvangen            |
| Actief | Actief, gesloten            | Geaccepteerd                     |
| Gesloten | Gesloten                    | Gewonnen, verloren, afgewezen, verlopen |

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> Verwijder het `"links": { }` object uit de put-resource.

## <a name="rest-response"></a>REST-antwoord

Als dit lukt, retourneert deze methode de gevulde [verwijzings](referral-resources.md) bron in de antwoord tekst.

### <a name="response-success-and-error-codes"></a>Geslaagde en fout codes

Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing. Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen. Zie [fout codes](error-codes.md)voor de volledige lijst.

### <a name="response-example"></a>Voorbeeld van antwoord

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
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
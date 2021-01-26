---
title: Een lead of verkoopkans bijwerken
description: Hiermee kunt u de details van de lead of de opportuniteit bijwerken.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770424"
---
# <a name="update-a-lead-or-opportunity"></a>Een lead of verkoopkans bijwerken

Van toepassing op:

- Partner-API

In dit onderwerp wordt uitgelegd hoe u de lead-of verkoopkansgegevens, zoals de deal waarde, de geschatte Sluitings datum, of de verkoop stadia onder andere details bijwerkt.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [partner API-verificatie](api-authentication.md). Dit scenario ondersteunt verificatie met app + gebruikers referenties.
- Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, referentie beheerder of verwijzings gebruiker.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Syntaxis van aanvraag

| Methode  | Aanvraag-URI                                                       |
|---------|-------------------------------------------------------------------|
| **VERZENDEN** | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a>URI-para meter


| Naam                   | Type     | Vereist | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Id                      | tekenreeks   | Yes       | De unieke id voor een lead of een verkoop kans op verkoop       |

### <a name="request-headers"></a>Aanvraagheaders

Zie [partner rest headers](headers.md) voor meer informatie.

### <a name="request-body"></a>Aanvraagbody

De aanvraag tekst volgt de indeling van de [JSON-patch](https://tools.ietf.org/html/rfc6902) . Een JSON-patch document heeft een matrix met bewerkingen. Elke bewerking identificeert een bepaald type wijziging. Voor beelden van dergelijke wijzigingen zijn het toevoegen van een matrix element of het vervangen van een eigenschaps waarde.

> [!Important]
> De API ondersteunt momenteel alleen de `replace` `add` bewerkingen en.

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> Als de **if-match-** header wordt door gegeven, wordt deze gebruikt voor gelijktijdigheids beheer.

## <a name="rest-response"></a>REST-antwoord

Als dit lukt, bevat de antwoord tekst de bijgewerkte [lead of verkoop kans](referral-resources.md).


### <a name="response-success-and-error-codes"></a>Geslaagde en fout codes

Elk antwoord wordt geleverd met een [HTTP-status code](error-codes.md) die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing. Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.

### <a name="response-example"></a>Voorbeeld van antwoord

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> De antwoord tekst is afhankelijk van de voor **Keurs** -header. Als de waarde van de header wordt wegge laten in de aanvraag, is de antwoord tekst leeg met de HTTP-status code 204. Voeg toe `Prefer: return=representation` aan de koptekst om de bijgewerkte lead of verkoop kans te verkrijgen.

## <a name="sample-requests"></a>Voorbeeld aanvragen

1. Hiermee wordt de deal waarde voor de verkoop kans bijgewerkt naar 10000 en worden de notities bijgewerkt. Er zijn geen gelijktijdigheids controles mogelijk vanwege de er zijn van de `If-Match` header.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. Hiermee wordt de status van een lead of verkoop kans bijgewerkt naar binnengehaald.
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > De `status` `substatus` velden en moeten overeenkomen met de toegestane set overgangs waarden, zoals [hier](referral-resources.md)wordt beschreven.

3. Voegt een nieuw lid van uw organisatie toe aan het team van lead of verkoop kansen. Het antwoord bevat de bijgewerkte lead of verkoop kans vanwege de aanwezigheid van de `Prefer: return=representation` header.

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```

---
title: Wisselkoersen ophalen
description: Wissel koersen voor een bepaalde maand te verkrijgen.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1e718624db54dcc2ed2b5d2d93dfd1cef0e6f96f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770417"
---
# <a name="get-foreign-exchange-rates"></a>Wisselkoersen ophalen

Van toepassing op:

- Partner-API

In dit onderwerp wordt uitgelegd hoe u wisselkoers tarieven voor een bepaalde maand kunt ophalen.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [partner API-verificatie](api-authentication.md). Dit scenario ondersteunt alleen toepassings gebruikers verificatie. Alleen-toepassing wordt nog niet ondersteund.
- Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, beheer agent of verkoop agent.


## <a name="details"></a>Details

- Wordt momenteel gebruikt met de [API voor prijzen overzichten ophalen](get-a-price-sheet.md) om verwachte kosten voor de lokale Valuta's van Azure plan CSP te berekenen.
- Valuta wisselkoersen blijven waar voor de hele maand.
- Meer informatie over de [prijzen](pricing.md) van Azure-abonnementen vindt u in de [Azure plan-prijs documentatie](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- De partner prijzen en deviezen-API-Api's maken geen deel uit van de [Partner Center-SDK](https://docs.microsoft.com/partner-center/develop/get-started).
- Deze methode retourneert resultaten als een bestands stroom. De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV. Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Syntaxis van aanvraag

| Methode   | Aanvraag-URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Toevoegen** | https://api.partner.microsoft.com/v1.0/sales/fxrates(Month={month})/$value                                  |

### <a name="uri-required-parameters"></a>Vereiste para meters voor URI

Gebruik de volgende Path-para meters om de gewenste maand aan te vragen.

| Naam                   | Type     | Vereist | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Maand                      | tekenreeks   | Yes       | Moet de YYYMM-indeling hebben. Als standaard de huidige maand wordt wegge laten.       |

### <a name="request-headers"></a>Aanvraagheaders

- Zie [partner rest headers](headers.md) voor meer informatie.

Naast de bovenstaande headers kunnen bestanden worden opgehaald als gecomprimeerde, verkleinde band breedte en download tijden. Standaard worden de bestanden niet gecomprimeerd. U kunt de onderstaande header waarde gebruiken om gecomprimeerde versies van de bestanden op te halen. Houd er rekening mee dat gecomprimeerde werk bladen alleen beschikbaar zijn vanaf 2020 april. alle aanvragen vóór april 2020 zijn alleen beschikbaar als niet-gecomprimeerd.

| Header                   | Waardetype     | Waarde | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| tekenreeks   | Deflate| Optioneel. Als er geen bestands stroom wordt wegge laten, wordt deze niet gecomprimeerd.       |

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-antwoord

Als dit lukt, retourneert deze methode wisselkoers tarieven als een bestands stroom. De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV.

### <a name="response-success-and-error-codes"></a>Geslaagde en fout codes

Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing. Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen. Zie [fout codes](error-codes.md)voor de volledige lijst.

### <a name="response-example"></a>Voorbeeld van antwoord

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 18548
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=fxrates
Request-ID: 65fb6e59-051b-42f7-8771-c8c139b3c901
Date: Wed, 02 Oct 2019 03:42:54 GMT

"CurrencyCode","USDPerUnit","Month"
"AED","0.27224589249009701","2019”
======= Truncated ==============

```

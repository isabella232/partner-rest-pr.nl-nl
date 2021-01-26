---
title: Een prijslijst ophalen
description: Verkrijg een prijzen overzicht voor een bepaalde markt en weer gave. Ondersteunt filters om geschiedenis per maand op te halen.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5195ebed6559bd71a7832a667e63ee801be1c82f
ms.sourcegitcommit: bb3f5f7ee0489bded86fe52e55018c1f4f5032e2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/07/2020
ms.locfileid: "97770416"
---
# <a name="get-a-price-sheet"></a>Een prijslijst ophalen

Van toepassing op:

- Partner-API

In dit onderwerp wordt uitgelegd hoe u een prijzen overzicht krijgt voor een bepaalde markt en weer gave. Deze methode ondersteunt filters om geschiedenis per maand op te halen.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [partner API-verificatie](api-authentication.md). Dit scenario ondersteunt alleen toepassings gebruikers verificatie. Application-alleen wordt nog niet ondersteund.
- Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, beheer agent of verkoop agent.

## <a name="details"></a>Details

- Huidige retourneert alleen gegevens voor verbruiks-en reserverings producten van Azure plan.
- De huidige [prijzen](pricing.md) omvatten alle meters en producten die beschikbaar zijn in de huidige maand tot de datum waarop de API wordt aangeroepen. Vorige maanden omvatten alle meters en producten die beschikbaar zijn voor de opgegeven maand.
- Prijzen voor verbruiks meter zijn alleen in USD. partners moeten gebruikmaken van de API voor buitenlandse wissel koersen om de lokale valuta kosten te berekenen.
- Prijzen voor verbruiks meter zijn geschatte verkoop prijzen. Partner kortingen zijn beschikbaar via het tegoed van de [partner](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).
- De prijs van de reserve ring meter omvat de CSP-partner kortingen. De geschatte verkoop prijzen voor reserve ringen vindt u in het Download bare bestand reserved services van de Partner Center-pagina prijzen en aanbiedingen.
- Meer informatie over de prijzen van Azure-abonnementen vindt u in de [Azure plan-prijs documentatie](https://docs.microsoft.com/partner-center/azure-plan-price-list).
- De partner prijzen en deviezen-API-Api's maken geen deel uit van de [Partner Center-SDK](https://docs.microsoft.com/partner-center/develop/get-started).
- Met deze methode wordt de prijs lijst als een bestands stroom geretourneerd. De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV. Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Syntaxis van aanvraag

| Methode   | Aanvraag-URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Toevoegen** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={Market}, PricesheetView = {View} ')/$value                                     |

### <a name="uri-required-parameters"></a>Vereiste para meters voor URI

Gebruik de volgende Path-para meters om te vragen welke markt en welk type prijs lijst u wilt gebruiken.

| Naam                   | Type     | Vereist | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Markt                      | tekenreeks   | Yes       | Land code van twee letters voor de markt die wordt aangevraagd       |
|PricesheetView | tekenreeks   | Yes       | Het aangevraagde type prijs lijst kan azure_consumption of azure_reservations       |

### <a name="uri-filter-parameters"></a>Para meters voor URI-filter

Gebruik de volgende filter parameters.

| Naam                   | Type     | Vereist | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Tijdlijn| tekenreeks   | No| De standaard waarde is actief als deze niet is door gegeven. Mogelijke waarden zijn geschiedenis, actueel en toekomstig.       |
|Maand| tekenreeks   | No| Alleen vereist als de geschiedenis is aangevraagd, moet voldoen aan de YYYYMM voor de aangevraagde prijs lijst.       |

### <a name="request-headers"></a>Aanvraagheaders

- Zie [partner rest headers](headers.md) voor meer informatie.

Naast de bovenstaande headers kunnen prijzen bestanden worden opgehaald als gecomprimeerde, verkleinde band breedte en download tijden. Standaard worden de bestanden niet gecomprimeerd. U kunt de onderstaande header waarde gebruiken om gecomprimeerde versies van de bestanden op te halen. Houd er rekening mee dat gecomprimeerde bladen alleen beschikbaar zijn vanaf 2020 april. alle bladen vóór april 2020 zijn alleen beschikbaar als niet-gecomprimeerd.

| Header                   | Waardetype     | Waarde | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| tekenreeks   | Deflate| Optioneel. Als er geen bestands stroom wordt wegge laten, wordt deze niet gecomprimeerd.       |

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-antwoord

Als deze methode is geslaagd, wordt de prijs lijst als een bestands stroom geretourneerd. De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV.

### <a name="response-success-and-error-codes"></a>Geslaagde en fout codes

Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing. Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen. Zie [fout codes](error-codes.md)voor de volledige lijst.

### <a name="response-example"></a>Voorbeeld van antwoord

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=pricesheet
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Oct 2019 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","MeterIds","MeterType","Tags“
"Advanced Data Security - SQL Database","DZH318Z0C16V","001J","Advanced Data Security - SQL Database - Standard - US East 2","Microsoft","Advanced Data Security - SQL Database - Standard - US East 2","1 Node/Month","payG-1","US","USD","15","","","3/1/2018 12:00:00 AM","11/30/9999 11:59:59 PM","cb0969aa-aaaa-4d6c-ab4b-7e182fa06aff","1 Node/Month","Azure“
======= Truncated ==============

```

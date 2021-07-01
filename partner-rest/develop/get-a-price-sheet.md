---
title: Een prijslijst ophalen
description: Verkrijg een prijzenblad voor een bepaalde markt en weergave. Ondersteunt filters om de geschiedenis per maand op te halen.
ms.date: 01/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 7571e8fce861dbfe463000a1ac4094115af08ffa
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2021
ms.locfileid: "113125513"
---
# <a name="get-a-price-sheet"></a>Een prijslijst ophalen

Van toepassing op:

- Partner-API

In dit onderwerp wordt uitgelegd hoe u een prijzenblad kunt krijgen voor een bepaalde markt en weergave. Deze methode ondersteunt filters om de geschiedenis per maand op te halen.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [Partner-API verificatie](api-authentication.md). Dit scenario ondersteunt alleen verificatie van toepassingsgebruikers. Alleen-toepassing wordt nog niet ondersteund. Partners die **http-fout 400** ervaren, moeten de documentatie Partner-API [verificatie](api-authentication.md) raadplegen.
- Deze API ondersteunt momenteel alleen gebruikerstoegang waarbij partners een van de volgende rollen moeten hebben: Globale beheerder, Beheerderagent of Verkoopagent.

## <a name="details"></a>Details

- Current retourneert alleen gegevens voor azure-planverbruik en reserveringsproducten.
- De [huidige prijzen](pricing.md) omvatten alle meters en producten die beschikbaar zijn in de huidige maand tot de datum waarop de API wordt aangeroepen. Vorige maanden bevatten alle meters en producten die beschikbaar zijn voor de opgegeven maand.
- Prijzen van verbruiksmeters zijn alleen in USD. Partners gebruiken de API voor wisselkoersen om de lokale valutakosten te berekenen.
- De prijzen van verbruiksmeters zijn geschatte detailhandelsprijzen. Partnerkortingen zijn beschikbaar via [partnertegoed](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).
- Reserveringsmeterprijzen zijn inclusief de CSP-partnerkortingen. Geschatte detailhandelsprijzen voor reserveringen vindt u in de gedeelde services voor reserveringen die kunnen worden gedownload op Partner Center pagina Prijzen en aanbiedingen.
- Meer informatie over prijzen voor Azure-plannen vindt u in de documentatie [over prijzen voor Azure-plannen.](https://docs.microsoft.com/partner-center/azure-plan-price-list)
- Partnerprijzen en API's voor wisselkoersen maken geen deel uit van [de Partnercentrum-SDK.](https://docs.microsoft.com/partner-center/develop/get-started)
- Deze methode retourneert de prijslijst als een bestandsstroom. Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv. Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Aanvraagsyntaxis

| Methode   | Aanvraag-URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Toevoegen** | https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={market},PricesheetView='{view}')/$value                                     |

### <a name="uri-required-parameters"></a>Vereiste URI-parameters

Gebruik de volgende padparameters om aan te vragen welke markt en welk type prijzenblad u wilt gebruiken.

| Naam                   | Type     | Vereist | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Markt                      | tekenreeks   | Ja       | Tweeletterig landnummer voor de markt die wordt aangevraagd       |
|PricesheetView | tekenreeks   | Ja       | Het type prijzenblad dat wordt aangevraagd. Dit kan worden azure_consumption, azure_reservations of bijgewerktgebaseerd.  |

> [!Note]
> updatedlicensebased PriceSheetView is momenteel alleen beschikbaar voor partners die deel uitmaken van de M365/D365 new commerce experience technical preview.

### <a name="uri-filter-parameters"></a>URI-filterparameters

Gebruik de volgende filterparameters.

| Naam                   | Type     | Vereist | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Tijdlijn| tekenreeks   | No| De standaardwaarde is current als deze niet wordt doorgegeven. Mogelijke waarden zijn geschiedenis, huidige en toekomstige waarden.       |
|Maand| tekenreeks   | No| Alleen vereist als de geschiedenis wordt aangevraagd, moet voldoen aan YYYYMM voor het prijzenblad dat wordt aangevraagd.       |

### <a name="request-headers"></a>Aanvraagheaders

- Zie [Partner REST-headers](headers.md) voor meer informatie.

Naast de bovenstaande headers kunnen prijsbestanden worden opgehaald als gecomprimeerde lagere bandbreedte en downloadtijden. Standaard worden de bestanden niet gecomprimeerd. Als u gecomprimeerde versies van de bestanden wilt downloaden, kunt u de onderstaande headerwaarde opnemen. U ziet dat gecomprimeerde bladen alleen beschikbaar zijn vanaf april 2020. Alle bladen vóór april 2020 zijn alleen beschikbaar als niet gecomprimeerd.

| Header                   | Waardetype     | Waarde | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| tekenreeks   | Deflate| Optioneel. Als de weggelaten bestandsstroom niet wordt gecomprimeerd.       |

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a>Voorbeeld aanvragen voor nieuwe handel

> [!Note]
> updatedlicensebased PriceSheetView is momenteel alleen beschikbaar voor partners die deel uitmaken van de M365/D365 new commerce experience technical preview.

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-antwoord

Als dit lukt, retourneert deze methode de prijslijst als een bestandsstroom. Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv.

### <a name="response-success-and-error-codes"></a>Antwoord geslaagd en foutcodes

Elk antwoord wordt geleverd met een HTTP-statuscode die aangeeft of het is gelukt of mislukt en aanvullende informatie over foutopsporing. Gebruik een hulpprogramma voor netwerk traceer om deze code, het fouttype en aanvullende parameters te lezen. Zie Foutcodes voor de [volledige lijst.](error-codes.md)

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

### <a name="response-example-for-new-commerce"></a>Voorbeeld van een reactie voor nieuwe handel

> [!Note]
> updatedlicensebased PriceSheetView is momenteel alleen beschikbaar voor partners die deel uitmaken van de M365/D365 new commerce experience technical preview.

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=sheets.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","Publisher","SkuDescription","UnitOfMeasure","TermDuration","BillingPlan","Market","Currency","UnitPrice","PricingTierRangeMin","PricingTierRangeMax","EffectiveStartDate","EffectiveEndDate","Tags","ERP Price“
"Advanced Communications","CFQ7TTC0HDK0","0001","Advanced Communications","Microsoft Corporation","Advanced meetings, calling, workflow integration, and management tools for IT.","","P1Y","Annual","US","USD","115.2","","","2/1/2019 12:00:00 AM","2/4/2021 8:35:31 PM","License","144"
======= Truncated ==============

```

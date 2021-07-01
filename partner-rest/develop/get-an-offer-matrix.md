---
title: Een aanbiedingsmatrix krijgen
description: Verkrijg een aanbiedingsmatrix voor een bepaalde datum. Ondersteunt filters om de geschiedenis per maand op te halen.
ms.date: 02/11/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e53276c1170febab002d35a42c88c1f96f7b7428
ms.sourcegitcommit: 9e64d6358ef4e1ac2d3e0d36cd63490a5f760b38
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/01/2021
ms.locfileid: "113131299"
---
# <a name="get-an-offer-matrix"></a>Een aanbiedingsmatrix krijgen

Van toepassing op:

- Partner-API
- De technical preview van de M365/D365 New Commerce-ervaring. De onderstaande new commerce-wijzigingen zijn momenteel alleen beschikbaar voor partners die deel uitmaken van de technical preview van de nieuwe commerce-ervaring M365/D365.

In dit onderwerp wordt uitgelegd hoe u een aanbiedingsmatrix voor een bepaalde maand kunt krijgen. De aanbiedingsmatrix bevat eigenschappen en aankoopregels voor de producten en SKU's. Deze methode ondersteunt filters om de geschiedenis per maand op te halen.

## <a name="prerequisites"></a>Vereisten

- Referenties zoals beschreven in [Partner-API verificatie](api-authentication.md). Dit scenario ondersteunt alleen verificatie van toepassingsgebruikers. Alleen-toepassing wordt nog niet ondersteund. Partners die **http-fout 400** ervaren, moeten de documentatie Partner-API [verificatie](api-authentication.md) raadplegen.
- Deze API ondersteunt momenteel alleen gebruikerstoegang waarbij partners een van de volgende rollen moeten hebben: Globale beheerder, Beheerderagent of Verkoopagent.

## <a name="details"></a>Details

- Current retourneert alleen gegevens voor bijgewerkte, op handelslicenties gebaseerde producten.
- De huidige prijzen omvatten producten die beschikbaar zijn in de huidige maand tot de datum waarop de API wordt aangeroepen. Vorige maanden bevatten de datum vanaf de laatste dag van de geselecteerde maand.
- Deze methode retourneert gegevens als een bestandsstroom. Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv. Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.

## <a name="rest-request"></a>REST-aanvraag

### <a name="request-syntax"></a>Aanvraagsyntaxis

| Methode   | Aanvraag-URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Toevoegen** | https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month={date})/$value |

### <a name="uri-filter-parameters"></a>URI-filterparameters

Gebruik de volgende filterparameters.

| Naam                   | Type     | Vereist | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Maand| tekenreeks   | No | Moet voldoen aan YYYYMM voor het prijzenblad dat wordt aangevraagd. |

### <a name="request-headers"></a>Aanvraagheaders

- Zie [Partner REST-headers](headers.md) voor meer informatie.

Naast de bovenstaande headers kunnen prijsbestanden worden opgehaald als gecomprimeerde lagere bandbreedte en downloadtijden. Standaard worden de bestanden niet gecomprimeerd. Als u gecomprimeerde versies van de bestanden wilt downloaden, kunt u de onderstaande headerwaarde opnemen. U ziet dat gecomprimeerde bladen alleen beschikbaar zijn vanaf april 2020. Alle bladen vóór april 2020 zijn alleen beschikbaar als niet gecomprimeerd.

| Header                   | Waardetype     | Waarde | Beschrijving                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|Accept-Encoding| tekenreeks   | Deflate| Optioneel. Als de weggelaten bestandsstroom niet wordt gecomprimeerd.       |

### <a name="request-example"></a>Voorbeeld van aanvraag

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a>REST-antwoord

Als dit lukt, retourneert deze methode een aanbiedingsmatrix als een bestandsstroom. Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv.

### <a name="response-success-and-error-codes"></a>Antwoord geslaagd en foutcodes

Elk antwoord wordt geleverd met een HTTP-statuscode die aangeeft of het is gelukt of mislukt en aanvullende informatie over foutopsporing. Gebruik een hulpprogramma voor netwerk traceer om deze code, het fouttype en aanvullende parameters te lezen. Zie Foutcodes voor de [volledige lijst.](error-codes.md)

### <a name="response-example"></a>Voorbeeld van antwoord

``` http
HTTP/1.1 200 OK
Cache-Control: private
Content-Length: 42180180
Content-Type: application/octet-stream
Content-Disposition: attachment; filename=updatedoffice.csv
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
Date: Wed, 02 Feb 2021 03:41:20 GMT

"ProductTitle","ProductId","SkuId","SkuTitle","ProvisioningId","ProvisioningString","MinLicenses","MaxLicenses","AssetOwnershipLimit","AssetOwnershipLimitType","ProductSkuPreRequisites","ProductSkuConversion","Description","AllowedCountries" 
"Microsoft 365 Business Basic","CFQ7TTC0LH18","0001","Microsoft 365 Business Basic","3b555118-da6a-4418-894f-7df1e2096870","O365_BUSINESS_ESSENTIALS","1","300","2","ConcurrentCount","","CFQ7TTC0LDPB/0001,CFQ7TTC0LF8Q/0001","Best for businesses that need professional...","AD;AE;AF;AG;AI;AL;AM;AO..."
======= Truncated ==============

```

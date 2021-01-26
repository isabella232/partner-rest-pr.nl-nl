---
title: REST-API van partner-headers
description: De volgende HTTP-aanvraag-en-antwoord headers worden ondersteund door de partner REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 955cab07da7f3a386690e18042165015906d864a
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770400"
---
# <a name="partner-rest-api-headers"></a>Partner REST API headers

De partner REST API ondersteunt de volgende HTTP-aanvraag-en-antwoord headers.

> [!NOTE]
> Niet alle API-aanroepen accepteren alle headers.

## <a name="request-headers"></a>Aanvraagheaders

De volgende HTTP-aanvraag headers worden ondersteund door de partner REST API.

| Header                       | Waardetype | Description                                                                            |
|------------------------------|------------|----------------------------------------------------------------------------------------|
| Autorisatie           | tekenreeks     | Vereist. Het autorisatie token in de vorm Bearer- &lt; token &gt; .                    |
| Accepteren                  | tekenreeks     | Hiermee geeft u de aanvraag en het antwoord type ' application/json ' op.                           |
| client-aanvraag-id         | GUID       | Vereist. Een unieke id voor de aanroep, die nuttig is in Logboeken en netwerk traceringen voor het oplossen van problemen. De waarde moet opnieuw worden ingesteld voor elke aanroep. Alle bewerkingen moeten deze header bevatten. |
| If-match:                    | tekenreeks     | Wordt gebruikt voor gelijktijdigheids beheer. Voor sommige API-aanroepen moet de ETag worden door gegeven via de If-Match-header. De ETag bevindt zich doorgaans op de bron en vereist dat u de meest recente versie krijgt. |

## <a name="response-headers"></a>Antwoordheaders

De volgende HTTP-antwoord headers kunnen worden geretourneerd door de partner REST API.

| Header                    | Waardetype | Description                                                                                                               |
|-------------------|------------|--------------------------------------------------------------------------------------------------|
| Accepteren                | tekenreeks     | Hiermee geeft u de aanvraag en het antwoord type ' application/json ' op.                                     |
| aanvraag-id        | GUID       | Een unieke id voor de oproep die wordt gebruikt om id-potentie te garanderen. In het geval van een time-out moet de aanroep voor opnieuw proberen dezelfde waarde bevatten. Wanneer er een reactie wordt ontvangen (geslaagd of mislukt), moet de waarde opnieuw worden ingesteld voor de volgende aanroep. |
| client-aanvraag-id| GUID| Een unieke id voor de aanroep, handig de logboeken en netwerk traceringen voor het oplossen van problemen. De waarde moet opnieuw worden ingesteld voor elke aanroep. Alle bewerkingen moeten deze header bevatten.                                                |
| x-MS-AGS-Diagnostic   | tekenreeks | Een teken reeks die diagnostische gegevens van de service bevat.
| tijdstempel|tekenreeks | Tijds tempel van de aanvraag bij het aanraken van de API.
|ETag |tekenreeks | ETag van de resource.

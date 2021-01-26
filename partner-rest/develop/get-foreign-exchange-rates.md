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
# <a name="get-foreign-exchange-rates"></a><span data-ttu-id="ec6b1-103">Wisselkoersen ophalen</span><span class="sxs-lookup"><span data-stu-id="ec6b1-103">Get foreign exchange rates</span></span>

<span data-ttu-id="ec6b1-104">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="ec6b1-104">Applies to:</span></span>

- <span data-ttu-id="ec6b1-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="ec6b1-105">Partner API</span></span>

<span data-ttu-id="ec6b1-106">In dit onderwerp wordt uitgelegd hoe u wisselkoers tarieven voor een bepaalde maand kunt ophalen.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-106">This topic explains how to get foreign exchange rates for a given month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec6b1-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec6b1-107">Prerequisites</span></span>

- <span data-ttu-id="ec6b1-108">Referenties zoals beschreven in [partner API-verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ec6b1-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="ec6b1-109">Dit scenario ondersteunt alleen toepassings gebruikers verificatie.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-109">This scenario only supports application user authentication.</span></span> <span data-ttu-id="ec6b1-110">Alleen-toepassing wordt nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-110">Application-only is not yet supported.</span></span>
- <span data-ttu-id="ec6b1-111">Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, beheer agent of verkoop agent.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>


## <a name="details"></a><span data-ttu-id="ec6b1-112">Details</span><span class="sxs-lookup"><span data-stu-id="ec6b1-112">Details</span></span>

- <span data-ttu-id="ec6b1-113">Wordt momenteel gebruikt met de [API voor prijzen overzichten ophalen](get-a-price-sheet.md) om verwachte kosten voor de lokale Valuta's van Azure plan CSP te berekenen.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-113">Currently used with [get price sheet API](get-a-price-sheet.md) to calculate expected charges for Azure plan CSP local currencies.</span></span>
- <span data-ttu-id="ec6b1-114">Valuta wisselkoersen blijven waar voor de hele maand.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-114">Foreign exchange rates hold true for the entire month they are posted.</span></span>
- <span data-ttu-id="ec6b1-115">Meer informatie over de [prijzen](pricing.md) van Azure-abonnementen vindt u in de [Azure plan-prijs documentatie](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="ec6b1-115">More information about Azure plan [pricing](pricing.md) can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="ec6b1-116">De partner prijzen en deviezen-API-Api's maken geen deel uit van de [Partner Center-SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="ec6b1-116">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="ec6b1-117">Deze methode retourneert resultaten als een bestands stroom.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-117">This method returns results as a file stream.</span></span> <span data-ttu-id="ec6b1-118">De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-118">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="ec6b1-119">Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-119">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="ec6b1-120">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="ec6b1-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ec6b1-121">Syntaxis van aanvraag</span><span class="sxs-lookup"><span data-stu-id="ec6b1-121">Request syntax</span></span>

| <span data-ttu-id="ec6b1-122">Methode</span><span class="sxs-lookup"><span data-stu-id="ec6b1-122">Method</span></span>   | <span data-ttu-id="ec6b1-123">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="ec6b1-123">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec6b1-124">**Toevoegen**</span><span class="sxs-lookup"><span data-stu-id="ec6b1-124">**GET**</span></span> | <span data-ttu-id="ec6b1-125"> https://api.partner.microsoft.com/v1.0/sales/fxrates(Month={month})/$value</span><span class="sxs-lookup"><span data-stu-id="ec6b1-125">https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='{month}')/$value</span></span>                                  |

### <a name="uri-required-parameters"></a><span data-ttu-id="ec6b1-126">Vereiste para meters voor URI</span><span class="sxs-lookup"><span data-stu-id="ec6b1-126">URI required parameters</span></span>

<span data-ttu-id="ec6b1-127">Gebruik de volgende Path-para meters om de gewenste maand aan te vragen.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-127">Use the following path parameters to request the month of foreign exchange rates you want.</span></span>

| <span data-ttu-id="ec6b1-128">Naam</span><span class="sxs-lookup"><span data-stu-id="ec6b1-128">Name</span></span>                   | <span data-ttu-id="ec6b1-129">Type</span><span class="sxs-lookup"><span data-stu-id="ec6b1-129">Type</span></span>     | <span data-ttu-id="ec6b1-130">Vereist</span><span class="sxs-lookup"><span data-stu-id="ec6b1-130">Required</span></span> | <span data-ttu-id="ec6b1-131">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ec6b1-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="ec6b1-132">Maand</span><span class="sxs-lookup"><span data-stu-id="ec6b1-132">Month</span></span>                      | <span data-ttu-id="ec6b1-133">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ec6b1-133">string</span></span>   | <span data-ttu-id="ec6b1-134">Yes</span><span class="sxs-lookup"><span data-stu-id="ec6b1-134">Yes</span></span>       | <span data-ttu-id="ec6b1-135">Moet de YYYMM-indeling hebben.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-135">Must be in YYYMM format.</span></span> <span data-ttu-id="ec6b1-136">Als standaard de huidige maand wordt wegge laten.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-136">If omitted defaults to current month.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="ec6b1-137">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="ec6b1-137">Request headers</span></span>

- <span data-ttu-id="ec6b1-138">Zie [partner rest headers](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-138">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="ec6b1-139">Naast de bovenstaande headers kunnen bestanden worden opgehaald als gecomprimeerde, verkleinde band breedte en download tijden.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-139">In addition to the above headers, files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="ec6b1-140">Standaard worden de bestanden niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-140">By default the files are not compressed.</span></span> <span data-ttu-id="ec6b1-141">U kunt de onderstaande header waarde gebruiken om gecomprimeerde versies van de bestanden op te halen.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-141">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="ec6b1-142">Houd er rekening mee dat gecomprimeerde werk bladen alleen beschikbaar zijn vanaf 2020 april. alle aanvragen vóór april 2020 zijn alleen beschikbaar als niet-gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-142">Realize that compressed sheets are only available from April 2020 onward, all requests prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="ec6b1-143">Header</span><span class="sxs-lookup"><span data-stu-id="ec6b1-143">Header</span></span>                   | <span data-ttu-id="ec6b1-144">Waardetype</span><span class="sxs-lookup"><span data-stu-id="ec6b1-144">Value Type</span></span>     | <span data-ttu-id="ec6b1-145">Waarde</span><span class="sxs-lookup"><span data-stu-id="ec6b1-145">Value</span></span> | <span data-ttu-id="ec6b1-146">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ec6b1-146">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="ec6b1-147">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="ec6b1-147">Accept-Encoding</span></span>| <span data-ttu-id="ec6b1-148">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ec6b1-148">string</span></span>   | <span data-ttu-id="ec6b1-149">Deflate</span><span class="sxs-lookup"><span data-stu-id="ec6b1-149">deflate</span></span>| <span data-ttu-id="ec6b1-150">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-150">Optional.</span></span> <span data-ttu-id="ec6b1-151">Als er geen bestands stroom wordt wegge laten, wordt deze niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-151">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="ec6b1-152">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="ec6b1-152">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/fxrates(Month='201909')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="ec6b1-153">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="ec6b1-153">REST response</span></span>

<span data-ttu-id="ec6b1-154">Als dit lukt, retourneert deze methode wisselkoers tarieven als een bestands stroom.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-154">If successful, this method returns foreign exchange rates as a file stream.</span></span> <span data-ttu-id="ec6b1-155">De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-155">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ec6b1-156">Geslaagde en fout codes</span><span class="sxs-lookup"><span data-stu-id="ec6b1-156">Response success and error codes</span></span>

<span data-ttu-id="ec6b1-157">Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ec6b1-158">Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ec6b1-159">Zie [fout codes](error-codes.md)voor de volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="ec6b1-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ec6b1-160">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="ec6b1-160">Response example</span></span>

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

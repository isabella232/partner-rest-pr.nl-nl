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
# <a name="get-a-price-sheet"></a><span data-ttu-id="44356-104">Een prijslijst ophalen</span><span class="sxs-lookup"><span data-stu-id="44356-104">Get a price sheet</span></span>

<span data-ttu-id="44356-105">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="44356-105">Applies to:</span></span>

- <span data-ttu-id="44356-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="44356-106">Partner API</span></span>

<span data-ttu-id="44356-107">In dit onderwerp wordt uitgelegd hoe u een prijzen overzicht krijgt voor een bepaalde markt en weer gave.</span><span class="sxs-lookup"><span data-stu-id="44356-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="44356-108">Deze methode ondersteunt filters om geschiedenis per maand op te halen.</span><span class="sxs-lookup"><span data-stu-id="44356-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44356-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="44356-109">Prerequisites</span></span>

- <span data-ttu-id="44356-110">Referenties zoals beschreven in [partner API-verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="44356-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="44356-111">Dit scenario ondersteunt alleen toepassings gebruikers verificatie.</span><span class="sxs-lookup"><span data-stu-id="44356-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="44356-112">Application-alleen wordt nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="44356-112">Application-ony is not yet supported.</span></span>
- <span data-ttu-id="44356-113">Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, beheer agent of verkoop agent.</span><span class="sxs-lookup"><span data-stu-id="44356-113">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="44356-114">Details</span><span class="sxs-lookup"><span data-stu-id="44356-114">Details</span></span>

- <span data-ttu-id="44356-115">Huidige retourneert alleen gegevens voor verbruiks-en reserverings producten van Azure plan.</span><span class="sxs-lookup"><span data-stu-id="44356-115">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="44356-116">De huidige [prijzen](pricing.md) omvatten alle meters en producten die beschikbaar zijn in de huidige maand tot de datum waarop de API wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="44356-116">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="44356-117">Vorige maanden omvatten alle meters en producten die beschikbaar zijn voor de opgegeven maand.</span><span class="sxs-lookup"><span data-stu-id="44356-117">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="44356-118">Prijzen voor verbruiks meter zijn alleen in USD. partners moeten gebruikmaken van de API voor buitenlandse wissel koersen om de lokale valuta kosten te berekenen.</span><span class="sxs-lookup"><span data-stu-id="44356-118">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="44356-119">Prijzen voor verbruiks meter zijn geschatte verkoop prijzen.</span><span class="sxs-lookup"><span data-stu-id="44356-119">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="44356-120">Partner kortingen zijn beschikbaar via het tegoed van de [partner](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span><span class="sxs-lookup"><span data-stu-id="44356-120">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="44356-121">De prijs van de reserve ring meter omvat de CSP-partner kortingen.</span><span class="sxs-lookup"><span data-stu-id="44356-121">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="44356-122">De geschatte verkoop prijzen voor reserve ringen vindt u in het Download bare bestand reserved services van de Partner Center-pagina prijzen en aanbiedingen.</span><span class="sxs-lookup"><span data-stu-id="44356-122">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="44356-123">Meer informatie over de prijzen van Azure-abonnementen vindt u in de [Azure plan-prijs documentatie](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span><span class="sxs-lookup"><span data-stu-id="44356-123">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="44356-124">De partner prijzen en deviezen-API-Api's maken geen deel uit van de [Partner Center-SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span><span class="sxs-lookup"><span data-stu-id="44356-124">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="44356-125">Met deze methode wordt de prijs lijst als een bestands stroom geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="44356-125">This method returns the price list as a file stream.</span></span> <span data-ttu-id="44356-126">De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV.</span><span class="sxs-lookup"><span data-stu-id="44356-126">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="44356-127">Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.</span><span class="sxs-lookup"><span data-stu-id="44356-127">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="44356-128">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="44356-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44356-129">Syntaxis van aanvraag</span><span class="sxs-lookup"><span data-stu-id="44356-129">Request syntax</span></span>

| <span data-ttu-id="44356-130">Methode</span><span class="sxs-lookup"><span data-stu-id="44356-130">Method</span></span>   | <span data-ttu-id="44356-131">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="44356-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44356-132">**Toevoegen**</span><span class="sxs-lookup"><span data-stu-id="44356-132">**GET**</span></span> | <span data-ttu-id="44356-133"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={Market}, PricesheetView = {View} ')/$value</span><span class="sxs-lookup"><span data-stu-id="44356-133">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="44356-134">Vereiste para meters voor URI</span><span class="sxs-lookup"><span data-stu-id="44356-134">URI required parameters</span></span>

<span data-ttu-id="44356-135">Gebruik de volgende Path-para meters om te vragen welke markt en welk type prijs lijst u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44356-135">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="44356-136">Naam</span><span class="sxs-lookup"><span data-stu-id="44356-136">Name</span></span>                   | <span data-ttu-id="44356-137">Type</span><span class="sxs-lookup"><span data-stu-id="44356-137">Type</span></span>     | <span data-ttu-id="44356-138">Vereist</span><span class="sxs-lookup"><span data-stu-id="44356-138">Required</span></span> | <span data-ttu-id="44356-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44356-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="44356-140">Markt</span><span class="sxs-lookup"><span data-stu-id="44356-140">Market</span></span>                      | <span data-ttu-id="44356-141">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="44356-141">string</span></span>   | <span data-ttu-id="44356-142">Yes</span><span class="sxs-lookup"><span data-stu-id="44356-142">Yes</span></span>       | <span data-ttu-id="44356-143">Land code van twee letters voor de markt die wordt aangevraagd</span><span class="sxs-lookup"><span data-stu-id="44356-143">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="44356-144">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="44356-144">PricesheetView</span></span> | <span data-ttu-id="44356-145">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="44356-145">string</span></span>   | <span data-ttu-id="44356-146">Yes</span><span class="sxs-lookup"><span data-stu-id="44356-146">Yes</span></span>       | <span data-ttu-id="44356-147">Het aangevraagde type prijs lijst kan azure_consumption of azure_reservations</span><span class="sxs-lookup"><span data-stu-id="44356-147">The type of price sheet being requested, this can be azure_consumption or azure_reservations</span></span>       |

### <a name="uri-filter-parameters"></a><span data-ttu-id="44356-148">Para meters voor URI-filter</span><span class="sxs-lookup"><span data-stu-id="44356-148">URI filter parameters</span></span>

<span data-ttu-id="44356-149">Gebruik de volgende filter parameters.</span><span class="sxs-lookup"><span data-stu-id="44356-149">Use the following filter parameters.</span></span>

| <span data-ttu-id="44356-150">Naam</span><span class="sxs-lookup"><span data-stu-id="44356-150">Name</span></span>                   | <span data-ttu-id="44356-151">Type</span><span class="sxs-lookup"><span data-stu-id="44356-151">Type</span></span>     | <span data-ttu-id="44356-152">Vereist</span><span class="sxs-lookup"><span data-stu-id="44356-152">Required</span></span> | <span data-ttu-id="44356-153">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44356-153">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="44356-154">Tijdlijn</span><span class="sxs-lookup"><span data-stu-id="44356-154">Timeline</span></span>| <span data-ttu-id="44356-155">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="44356-155">string</span></span>   | <span data-ttu-id="44356-156">No</span><span class="sxs-lookup"><span data-stu-id="44356-156">No</span></span>| <span data-ttu-id="44356-157">De standaard waarde is actief als deze niet is door gegeven.</span><span class="sxs-lookup"><span data-stu-id="44356-157">Defaults to current if not passed.</span></span> <span data-ttu-id="44356-158">Mogelijke waarden zijn geschiedenis, actueel en toekomstig.</span><span class="sxs-lookup"><span data-stu-id="44356-158">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="44356-159">Maand</span><span class="sxs-lookup"><span data-stu-id="44356-159">Month</span></span>| <span data-ttu-id="44356-160">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="44356-160">string</span></span>   | <span data-ttu-id="44356-161">No</span><span class="sxs-lookup"><span data-stu-id="44356-161">No</span></span>| <span data-ttu-id="44356-162">Alleen vereist als de geschiedenis is aangevraagd, moet voldoen aan de YYYYMM voor de aangevraagde prijs lijst.</span><span class="sxs-lookup"><span data-stu-id="44356-162">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="44356-163">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="44356-163">Request headers</span></span>

- <span data-ttu-id="44356-164">Zie [partner rest headers](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44356-164">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="44356-165">Naast de bovenstaande headers kunnen prijzen bestanden worden opgehaald als gecomprimeerde, verkleinde band breedte en download tijden.</span><span class="sxs-lookup"><span data-stu-id="44356-165">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="44356-166">Standaard worden de bestanden niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="44356-166">By default the files are not compressed.</span></span> <span data-ttu-id="44356-167">U kunt de onderstaande header waarde gebruiken om gecomprimeerde versies van de bestanden op te halen.</span><span class="sxs-lookup"><span data-stu-id="44356-167">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="44356-168">Houd er rekening mee dat gecomprimeerde bladen alleen beschikbaar zijn vanaf 2020 april. alle bladen vóór april 2020 zijn alleen beschikbaar als niet-gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="44356-168">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="44356-169">Header</span><span class="sxs-lookup"><span data-stu-id="44356-169">Header</span></span>                   | <span data-ttu-id="44356-170">Waardetype</span><span class="sxs-lookup"><span data-stu-id="44356-170">Value Type</span></span>     | <span data-ttu-id="44356-171">Waarde</span><span class="sxs-lookup"><span data-stu-id="44356-171">Value</span></span> | <span data-ttu-id="44356-172">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44356-172">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="44356-173">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="44356-173">Accept-Encoding</span></span>| <span data-ttu-id="44356-174">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="44356-174">string</span></span>   | <span data-ttu-id="44356-175">Deflate</span><span class="sxs-lookup"><span data-stu-id="44356-175">deflate</span></span>| <span data-ttu-id="44356-176">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="44356-176">Optional.</span></span> <span data-ttu-id="44356-177">Als er geen bestands stroom wordt wegge laten, wordt deze niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="44356-177">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="44356-178">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="44356-178">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="44356-179">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="44356-179">REST response</span></span>

<span data-ttu-id="44356-180">Als deze methode is geslaagd, wordt de prijs lijst als een bestands stroom geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="44356-180">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="44356-181">De bestands stroom is een CSV-bestand of een gecomprimeerde ZIP-versie van het CSV.</span><span class="sxs-lookup"><span data-stu-id="44356-181">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44356-182">Geslaagde en fout codes</span><span class="sxs-lookup"><span data-stu-id="44356-182">Response success and error codes</span></span>

<span data-ttu-id="44356-183">Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing.</span><span class="sxs-lookup"><span data-stu-id="44356-183">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44356-184">Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.</span><span class="sxs-lookup"><span data-stu-id="44356-184">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44356-185">Zie [fout codes](error-codes.md)voor de volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="44356-185">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44356-186">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="44356-186">Response example</span></span>

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

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
# <a name="get-a-price-sheet"></a><span data-ttu-id="a0a85-104">Een prijslijst ophalen</span><span class="sxs-lookup"><span data-stu-id="a0a85-104">Get a price sheet</span></span>

<span data-ttu-id="a0a85-105">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="a0a85-105">Applies to:</span></span>

- <span data-ttu-id="a0a85-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="a0a85-106">Partner API</span></span>

<span data-ttu-id="a0a85-107">In dit onderwerp wordt uitgelegd hoe u een prijzenblad kunt krijgen voor een bepaalde markt en weergave.</span><span class="sxs-lookup"><span data-stu-id="a0a85-107">This topic explains how to get a price sheet for a given market and view.</span></span> <span data-ttu-id="a0a85-108">Deze methode ondersteunt filters om de geschiedenis per maand op te halen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-108">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0a85-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a0a85-109">Prerequisites</span></span>

- <span data-ttu-id="a0a85-110">Referenties zoals beschreven in [Partner-API verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a0a85-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="a0a85-111">Dit scenario ondersteunt alleen verificatie van toepassingsgebruikers.</span><span class="sxs-lookup"><span data-stu-id="a0a85-111">This scenario only supports application user authentication.</span></span> <span data-ttu-id="a0a85-112">Alleen-toepassing wordt nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a0a85-112">Application-only is not yet supported.</span></span> <span data-ttu-id="a0a85-113">Partners die **http-fout 400** ervaren, moeten de documentatie Partner-API [verificatie](api-authentication.md) raadplegen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-113">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="a0a85-114">Deze API ondersteunt momenteel alleen gebruikerstoegang waarbij partners een van de volgende rollen moeten hebben: Globale beheerder, Beheerderagent of Verkoopagent.</span><span class="sxs-lookup"><span data-stu-id="a0a85-114">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="a0a85-115">Details</span><span class="sxs-lookup"><span data-stu-id="a0a85-115">Details</span></span>

- <span data-ttu-id="a0a85-116">Current retourneert alleen gegevens voor azure-planverbruik en reserveringsproducten.</span><span class="sxs-lookup"><span data-stu-id="a0a85-116">Current returns data only for Azure plan consumption and reservation products.</span></span>
- <span data-ttu-id="a0a85-117">De [huidige prijzen](pricing.md) omvatten alle meters en producten die beschikbaar zijn in de huidige maand tot de datum waarop de API wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-117">Current [pricing](pricing.md) includes all meters and products available during the current month to the date the API is called.</span></span> <span data-ttu-id="a0a85-118">Vorige maanden bevatten alle meters en producten die beschikbaar zijn voor de opgegeven maand.</span><span class="sxs-lookup"><span data-stu-id="a0a85-118">Previous months include all meters and products available for the given month.</span></span>
- <span data-ttu-id="a0a85-119">Prijzen van verbruiksmeters zijn alleen in USD. Partners gebruiken de API voor wisselkoersen om de lokale valutakosten te berekenen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-119">Consumption meter prices are only in USD, partners are to use the foreign exchange rates API to calculate local currency costs.</span></span>
- <span data-ttu-id="a0a85-120">De prijzen van verbruiksmeters zijn geschatte detailhandelsprijzen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-120">Consumption meter prices are estimated retail prices.</span></span> <span data-ttu-id="a0a85-121">Partnerkortingen zijn beschikbaar via [partnertegoed](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span><span class="sxs-lookup"><span data-stu-id="a0a85-121">Partner discounts are available via [partner earned credit](https://docs.microsoft.com/partner-center/partner-earned-credit-explanation).</span></span>
- <span data-ttu-id="a0a85-122">Reserveringsmeterprijzen zijn inclusief de CSP-partnerkortingen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-122">Reservations meter prices include the CSP partner discounts.</span></span> <span data-ttu-id="a0a85-123">Geschatte detailhandelsprijzen voor reserveringen vindt u in de gedeelde services voor reserveringen die kunnen worden gedownload op Partner Center pagina Prijzen en aanbiedingen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-123">Estimated retail prices for reservations can be found in the reservations shared services downloadable from the Partner Center "Pricing and offers" page.</span></span>
- <span data-ttu-id="a0a85-124">Meer informatie over prijzen voor Azure-plannen vindt u in de documentatie [over prijzen voor Azure-plannen.](https://docs.microsoft.com/partner-center/azure-plan-price-list)</span><span class="sxs-lookup"><span data-stu-id="a0a85-124">More information about Azure plan pricing can be found in the [Azure plan pricing documentation](https://docs.microsoft.com/partner-center/azure-plan-price-list).</span></span>
- <span data-ttu-id="a0a85-125">Partnerprijzen en API's voor wisselkoersen maken geen deel uit van [de Partnercentrum-SDK.](https://docs.microsoft.com/partner-center/develop/get-started)</span><span class="sxs-lookup"><span data-stu-id="a0a85-125">Partner pricing and foreign exchange rate APIs are not part of the [Partner Center SDK](https://docs.microsoft.com/partner-center/develop/get-started).</span></span>
- <span data-ttu-id="a0a85-126">Deze methode retourneert de prijslijst als een bestandsstroom.</span><span class="sxs-lookup"><span data-stu-id="a0a85-126">This method returns the price list as a file stream.</span></span> <span data-ttu-id="a0a85-127">Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv.</span><span class="sxs-lookup"><span data-stu-id="a0a85-127">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="a0a85-128">Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.</span><span class="sxs-lookup"><span data-stu-id="a0a85-128">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a0a85-129">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="a0a85-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a0a85-130">Aanvraagsyntaxis</span><span class="sxs-lookup"><span data-stu-id="a0a85-130">Request syntax</span></span>

| <span data-ttu-id="a0a85-131">Methode</span><span class="sxs-lookup"><span data-stu-id="a0a85-131">Method</span></span>   | <span data-ttu-id="a0a85-132">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="a0a85-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a0a85-133">**Toevoegen**</span><span class="sxs-lookup"><span data-stu-id="a0a85-133">**GET**</span></span> | <span data-ttu-id="a0a85-134"> https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market={market},PricesheetView='{view}')/$value</span><span class="sxs-lookup"><span data-stu-id="a0a85-134">https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='{market}',PricesheetView='{view}')/$value</span></span>                                     |

### <a name="uri-required-parameters"></a><span data-ttu-id="a0a85-135">Vereiste URI-parameters</span><span class="sxs-lookup"><span data-stu-id="a0a85-135">URI required parameters</span></span>

<span data-ttu-id="a0a85-136">Gebruik de volgende padparameters om aan te vragen welke markt en welk type prijzenblad u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0a85-136">Use the following path parameters to request which market and type of price sheet you want.</span></span>

| <span data-ttu-id="a0a85-137">Naam</span><span class="sxs-lookup"><span data-stu-id="a0a85-137">Name</span></span>                   | <span data-ttu-id="a0a85-138">Type</span><span class="sxs-lookup"><span data-stu-id="a0a85-138">Type</span></span>     | <span data-ttu-id="a0a85-139">Vereist</span><span class="sxs-lookup"><span data-stu-id="a0a85-139">Required</span></span> | <span data-ttu-id="a0a85-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a0a85-140">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="a0a85-141">Markt</span><span class="sxs-lookup"><span data-stu-id="a0a85-141">Market</span></span>                      | <span data-ttu-id="a0a85-142">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a0a85-142">string</span></span>   | <span data-ttu-id="a0a85-143">Ja</span><span class="sxs-lookup"><span data-stu-id="a0a85-143">Yes</span></span>       | <span data-ttu-id="a0a85-144">Tweeletterig landnummer voor de markt die wordt aangevraagd</span><span class="sxs-lookup"><span data-stu-id="a0a85-144">Two letter country code for the market being requested</span></span>       |
|<span data-ttu-id="a0a85-145">PricesheetView</span><span class="sxs-lookup"><span data-stu-id="a0a85-145">PricesheetView</span></span> | <span data-ttu-id="a0a85-146">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a0a85-146">string</span></span>   | <span data-ttu-id="a0a85-147">Ja</span><span class="sxs-lookup"><span data-stu-id="a0a85-147">Yes</span></span>       | <span data-ttu-id="a0a85-148">Het type prijzenblad dat wordt aangevraagd. Dit kan worden azure_consumption, azure_reservations of bijgewerktgebaseerd.</span><span class="sxs-lookup"><span data-stu-id="a0a85-148">The type of price sheet being requested, this can be azure_consumption, azure_reservations or updatedlicensebased.</span></span>  |

> [!Note]
> <span data-ttu-id="a0a85-149">updatedlicensebased PriceSheetView is momenteel alleen beschikbaar voor partners die deel uitmaken van de M365/D365 new commerce experience technical preview.</span><span class="sxs-lookup"><span data-stu-id="a0a85-149">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

### <a name="uri-filter-parameters"></a><span data-ttu-id="a0a85-150">URI-filterparameters</span><span class="sxs-lookup"><span data-stu-id="a0a85-150">URI filter parameters</span></span>

<span data-ttu-id="a0a85-151">Gebruik de volgende filterparameters.</span><span class="sxs-lookup"><span data-stu-id="a0a85-151">Use the following filter parameters.</span></span>

| <span data-ttu-id="a0a85-152">Naam</span><span class="sxs-lookup"><span data-stu-id="a0a85-152">Name</span></span>                   | <span data-ttu-id="a0a85-153">Type</span><span class="sxs-lookup"><span data-stu-id="a0a85-153">Type</span></span>     | <span data-ttu-id="a0a85-154">Vereist</span><span class="sxs-lookup"><span data-stu-id="a0a85-154">Required</span></span> | <span data-ttu-id="a0a85-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a0a85-155">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="a0a85-156">Tijdlijn</span><span class="sxs-lookup"><span data-stu-id="a0a85-156">Timeline</span></span>| <span data-ttu-id="a0a85-157">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a0a85-157">string</span></span>   | <span data-ttu-id="a0a85-158">No</span><span class="sxs-lookup"><span data-stu-id="a0a85-158">No</span></span>| <span data-ttu-id="a0a85-159">De standaardwaarde is current als deze niet wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="a0a85-159">Defaults to current if not passed.</span></span> <span data-ttu-id="a0a85-160">Mogelijke waarden zijn geschiedenis, huidige en toekomstige waarden.</span><span class="sxs-lookup"><span data-stu-id="a0a85-160">Possible values are history, current and future.</span></span>       |
|<span data-ttu-id="a0a85-161">Maand</span><span class="sxs-lookup"><span data-stu-id="a0a85-161">Month</span></span>| <span data-ttu-id="a0a85-162">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a0a85-162">string</span></span>   | <span data-ttu-id="a0a85-163">No</span><span class="sxs-lookup"><span data-stu-id="a0a85-163">No</span></span>| <span data-ttu-id="a0a85-164">Alleen vereist als de geschiedenis wordt aangevraagd, moet voldoen aan YYYYMM voor het prijzenblad dat wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="a0a85-164">Only required if history is requested, must adhere to YYYYMM for the price sheet being requested.</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="a0a85-165">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="a0a85-165">Request headers</span></span>

- <span data-ttu-id="a0a85-166">Zie [Partner REST-headers](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a0a85-166">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="a0a85-167">Naast de bovenstaande headers kunnen prijsbestanden worden opgehaald als gecomprimeerde lagere bandbreedte en downloadtijden.</span><span class="sxs-lookup"><span data-stu-id="a0a85-167">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="a0a85-168">Standaard worden de bestanden niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="a0a85-168">By default the files are not compressed.</span></span> <span data-ttu-id="a0a85-169">Als u gecomprimeerde versies van de bestanden wilt downloaden, kunt u de onderstaande headerwaarde opnemen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-169">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="a0a85-170">U ziet dat gecomprimeerde bladen alleen beschikbaar zijn vanaf april 2020. Alle bladen vóór april 2020 zijn alleen beschikbaar als niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="a0a85-170">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="a0a85-171">Header</span><span class="sxs-lookup"><span data-stu-id="a0a85-171">Header</span></span>                   | <span data-ttu-id="a0a85-172">Waardetype</span><span class="sxs-lookup"><span data-stu-id="a0a85-172">Value Type</span></span>     | <span data-ttu-id="a0a85-173">Waarde</span><span class="sxs-lookup"><span data-stu-id="a0a85-173">Value</span></span> | <span data-ttu-id="a0a85-174">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a0a85-174">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="a0a85-175">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="a0a85-175">Accept-Encoding</span></span>| <span data-ttu-id="a0a85-176">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a0a85-176">string</span></span>   | <span data-ttu-id="a0a85-177">Deflate</span><span class="sxs-lookup"><span data-stu-id="a0a85-177">deflate</span></span>| <span data-ttu-id="a0a85-178">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="a0a85-178">Optional.</span></span> <span data-ttu-id="a0a85-179">Als de weggelaten bestandsstroom niet wordt gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="a0a85-179">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="a0a85-180">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="a0a85-180">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='ad',PricesheetView='azure_consumption')/$value?timeline=history&month=201909 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```
### <a name="request-example-for-new-commerce"></a><span data-ttu-id="a0a85-181">Voorbeeld aanvragen voor nieuwe handel</span><span class="sxs-lookup"><span data-stu-id="a0a85-181">Request example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="a0a85-182">updatedlicensebased PriceSheetView is momenteel alleen beschikbaar voor partners die deel uitmaken van de M365/D365 new commerce experience technical preview.</span><span class="sxs-lookup"><span data-stu-id="a0a85-182">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/pricesheets(Market='US',PricesheetView='updatedlicensebased')/$value?timeline=history&month=202101 HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="a0a85-183">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="a0a85-183">REST response</span></span>

<span data-ttu-id="a0a85-184">Als dit lukt, retourneert deze methode de prijslijst als een bestandsstroom.</span><span class="sxs-lookup"><span data-stu-id="a0a85-184">If successful, this method returns the price list as a file stream.</span></span> <span data-ttu-id="a0a85-185">Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv.</span><span class="sxs-lookup"><span data-stu-id="a0a85-185">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a0a85-186">Antwoord geslaagd en foutcodes</span><span class="sxs-lookup"><span data-stu-id="a0a85-186">Response success and error codes</span></span>

<span data-ttu-id="a0a85-187">Elk antwoord wordt geleverd met een HTTP-statuscode die aangeeft of het is gelukt of mislukt en aanvullende informatie over foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="a0a85-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a0a85-188">Gebruik een hulpprogramma voor netwerk traceer om deze code, het fouttype en aanvullende parameters te lezen.</span><span class="sxs-lookup"><span data-stu-id="a0a85-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a0a85-189">Zie Foutcodes voor de [volledige lijst.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a0a85-189">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a0a85-190">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="a0a85-190">Response example</span></span>

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

### <a name="response-example-for-new-commerce"></a><span data-ttu-id="a0a85-191">Voorbeeld van een reactie voor nieuwe handel</span><span class="sxs-lookup"><span data-stu-id="a0a85-191">Response example for new commerce</span></span>

> [!Note]
> <span data-ttu-id="a0a85-192">updatedlicensebased PriceSheetView is momenteel alleen beschikbaar voor partners die deel uitmaken van de M365/D365 new commerce experience technical preview.</span><span class="sxs-lookup"><span data-stu-id="a0a85-192">updatedlicensebased PriceSheetView is currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

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

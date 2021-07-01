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
# <a name="get-an-offer-matrix"></a><span data-ttu-id="1fbd0-104">Een aanbiedingsmatrix krijgen</span><span class="sxs-lookup"><span data-stu-id="1fbd0-104">Get an offer matrix</span></span>

<span data-ttu-id="1fbd0-105">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="1fbd0-105">Applies to:</span></span>

- <span data-ttu-id="1fbd0-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="1fbd0-106">Partner API</span></span>
- <span data-ttu-id="1fbd0-107">De technical preview van de M365/D365 New Commerce-ervaring.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-107">The M365/D365 New Commerce experience technical preview.</span></span> <span data-ttu-id="1fbd0-108">De onderstaande new commerce-wijzigingen zijn momenteel alleen beschikbaar voor partners die deel uitmaken van de technical preview van de nieuwe commerce-ervaring M365/D365.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-108">The below New Commerce changes are currently available only to partners who are part of the M365/D365 new commerce experience technical preview.</span></span>

<span data-ttu-id="1fbd0-109">In dit onderwerp wordt uitgelegd hoe u een aanbiedingsmatrix voor een bepaalde maand kunt krijgen.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-109">This topic explains how to get an offer matrix for a given month.</span></span> <span data-ttu-id="1fbd0-110">De aanbiedingsmatrix bevat eigenschappen en aankoopregels voor de producten en SKU's.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-110">The offer matrix includes properties and purchase rules for the products and skus.</span></span> <span data-ttu-id="1fbd0-111">Deze methode ondersteunt filters om de geschiedenis per maand op te halen.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-111">This method supports filters to get history by month.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1fbd0-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1fbd0-112">Prerequisites</span></span>

- <span data-ttu-id="1fbd0-113">Referenties zoals beschreven in [Partner-API verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1fbd0-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="1fbd0-114">Dit scenario ondersteunt alleen verificatie van toepassingsgebruikers.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-114">This scenario only supports application user authentication.</span></span> <span data-ttu-id="1fbd0-115">Alleen-toepassing wordt nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-115">Application-only is not yet supported.</span></span> <span data-ttu-id="1fbd0-116">Partners die **http-fout 400** ervaren, moeten de documentatie Partner-API [verificatie](api-authentication.md) raadplegen.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-116">Partners that experience **http error:400** should consult the [Partner API authentication](api-authentication.md) documentation.</span></span>
- <span data-ttu-id="1fbd0-117">Deze API ondersteunt momenteel alleen gebruikerstoegang waarbij partners een van de volgende rollen moeten hebben: Globale beheerder, Beheerderagent of Verkoopagent.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-117">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Admin Agent or Sales Agent.</span></span>

## <a name="details"></a><span data-ttu-id="1fbd0-118">Details</span><span class="sxs-lookup"><span data-stu-id="1fbd0-118">Details</span></span>

- <span data-ttu-id="1fbd0-119">Current retourneert alleen gegevens voor bijgewerkte, op handelslicenties gebaseerde producten.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-119">Current returns data only for updated new commerce license-based products.</span></span>
- <span data-ttu-id="1fbd0-120">De huidige prijzen omvatten producten die beschikbaar zijn in de huidige maand tot de datum waarop de API wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-120">Current pricing includes products available during the current month to the date the API is called.</span></span> <span data-ttu-id="1fbd0-121">Vorige maanden bevatten de datum vanaf de laatste dag van de geselecteerde maand.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-121">Previous months include date as of the last day of the selected month.</span></span>
- <span data-ttu-id="1fbd0-122">Deze methode retourneert gegevens als een bestandsstroom.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-122">This method returns data as a file stream.</span></span> <span data-ttu-id="1fbd0-123">Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-123">File stream is either a .csv file or a zip compressed version of the .csv.</span></span> <span data-ttu-id="1fbd0-124">Hieronder vindt u meer informatie over het aanvragen van gecomprimeerde bestanden.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-124">Details about how to request compressed files are included below.</span></span>

## <a name="rest-request"></a><span data-ttu-id="1fbd0-125">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="1fbd0-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1fbd0-126">Aanvraagsyntaxis</span><span class="sxs-lookup"><span data-stu-id="1fbd0-126">Request syntax</span></span>

| <span data-ttu-id="1fbd0-127">Methode</span><span class="sxs-lookup"><span data-stu-id="1fbd0-127">Method</span></span>   | <span data-ttu-id="1fbd0-128">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="1fbd0-128">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1fbd0-129">**Toevoegen**</span><span class="sxs-lookup"><span data-stu-id="1fbd0-129">**GET**</span></span> | <span data-ttu-id="1fbd0-130"> https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month={date})/$value</span><span class="sxs-lookup"><span data-stu-id="1fbd0-130">https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='{date}')/$value</span></span> |

### <a name="uri-filter-parameters"></a><span data-ttu-id="1fbd0-131">URI-filterparameters</span><span class="sxs-lookup"><span data-stu-id="1fbd0-131">URI filter parameters</span></span>

<span data-ttu-id="1fbd0-132">Gebruik de volgende filterparameters.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-132">Use the following filter parameters.</span></span>

| <span data-ttu-id="1fbd0-133">Naam</span><span class="sxs-lookup"><span data-stu-id="1fbd0-133">Name</span></span>                   | <span data-ttu-id="1fbd0-134">Type</span><span class="sxs-lookup"><span data-stu-id="1fbd0-134">Type</span></span>     | <span data-ttu-id="1fbd0-135">Vereist</span><span class="sxs-lookup"><span data-stu-id="1fbd0-135">Required</span></span> | <span data-ttu-id="1fbd0-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1fbd0-136">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="1fbd0-137">Maand</span><span class="sxs-lookup"><span data-stu-id="1fbd0-137">Month</span></span>| <span data-ttu-id="1fbd0-138">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1fbd0-138">string</span></span>   | <span data-ttu-id="1fbd0-139">No</span><span class="sxs-lookup"><span data-stu-id="1fbd0-139">No</span></span> | <span data-ttu-id="1fbd0-140">Moet voldoen aan YYYYMM voor het prijzenblad dat wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-140">Must adhere to YYYYMM for the price sheet being requested.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1fbd0-141">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="1fbd0-141">Request headers</span></span>

- <span data-ttu-id="1fbd0-142">Zie [Partner REST-headers](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-142">See [Partner REST headers](headers.md) for more information.</span></span>

<span data-ttu-id="1fbd0-143">Naast de bovenstaande headers kunnen prijsbestanden worden opgehaald als gecomprimeerde lagere bandbreedte en downloadtijden.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-143">In addition to the above headers, pricing files can be retrieved as compressed reducing bandwidth and download times.</span></span> <span data-ttu-id="1fbd0-144">Standaard worden de bestanden niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-144">By default the files are not compressed.</span></span> <span data-ttu-id="1fbd0-145">Als u gecomprimeerde versies van de bestanden wilt downloaden, kunt u de onderstaande headerwaarde opnemen.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-145">To get compressed versions of the files you can include the below header value.</span></span> <span data-ttu-id="1fbd0-146">U ziet dat gecomprimeerde bladen alleen beschikbaar zijn vanaf april 2020. Alle bladen vóór april 2020 zijn alleen beschikbaar als niet gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-146">Realize that compressed sheets are only available from April 2020 onward, all sheets prior to April 2020 are only available as not compressed.</span></span>

| <span data-ttu-id="1fbd0-147">Header</span><span class="sxs-lookup"><span data-stu-id="1fbd0-147">Header</span></span>                   | <span data-ttu-id="1fbd0-148">Waardetype</span><span class="sxs-lookup"><span data-stu-id="1fbd0-148">Value Type</span></span>     | <span data-ttu-id="1fbd0-149">Waarde</span><span class="sxs-lookup"><span data-stu-id="1fbd0-149">Value</span></span> | <span data-ttu-id="1fbd0-150">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1fbd0-150">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="1fbd0-151">Accept-Encoding</span><span class="sxs-lookup"><span data-stu-id="1fbd0-151">Accept-Encoding</span></span>| <span data-ttu-id="1fbd0-152">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1fbd0-152">string</span></span>   | <span data-ttu-id="1fbd0-153">Deflate</span><span class="sxs-lookup"><span data-stu-id="1fbd0-153">deflate</span></span>| <span data-ttu-id="1fbd0-154">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-154">Optional.</span></span> <span data-ttu-id="1fbd0-155">Als de weggelaten bestandsstroom niet wordt gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-155">If omitted file stream is not compressed.</span></span>       |

### <a name="request-example"></a><span data-ttu-id="1fbd0-156">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="1fbd0-156">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/sales/offermatrix(Month='202101')/$value HTTP/1.1
Authorization: Bearer
Accept-Encoding: deflate
Host: api.partner.microsoft.com

```

## <a name="rest-response"></a><span data-ttu-id="1fbd0-157">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="1fbd0-157">REST response</span></span>

<span data-ttu-id="1fbd0-158">Als dit lukt, retourneert deze methode een aanbiedingsmatrix als een bestandsstroom.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-158">If successful, this method returns an offer matrix as a file stream.</span></span> <span data-ttu-id="1fbd0-159">Bestandsstroom is een .csv of een gecomprimeerde ZIP-versie van de .csv.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-159">File stream is either a .csv file or a zip compressed version of the .csv.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1fbd0-160">Antwoord geslaagd en foutcodes</span><span class="sxs-lookup"><span data-stu-id="1fbd0-160">Response success and error codes</span></span>

<span data-ttu-id="1fbd0-161">Elk antwoord wordt geleverd met een HTTP-statuscode die aangeeft of het is gelukt of mislukt en aanvullende informatie over foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1fbd0-162">Gebruik een hulpprogramma voor netwerk traceer om deze code, het fouttype en aanvullende parameters te lezen.</span><span class="sxs-lookup"><span data-stu-id="1fbd0-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1fbd0-163">Zie Foutcodes voor de [volledige lijst.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1fbd0-163">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1fbd0-164">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="1fbd0-164">Response example</span></span>

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

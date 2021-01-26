---
title: Een lijst met leads en kansen ophalen
description: Een lijst met leads en verkoop kansen ophalen met behulp van de partner-API.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 46243f8484a8068827e24e1d03f39ffddade1dbf
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770420"
---
# <a name="get-the-list-of-leads-and-opportunities"></a><span data-ttu-id="dd4a4-103">De lijst met leads en verkoopkansen ophalen</span><span class="sxs-lookup"><span data-stu-id="dd4a4-103">Get the list of leads and opportunities</span></span>

<span data-ttu-id="dd4a4-104">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="dd4a4-104">Applies to:</span></span>

- <span data-ttu-id="dd4a4-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="dd4a4-105">Partner API</span></span>

 <span data-ttu-id="dd4a4-106">In dit onderwerp wordt uitgelegd hoe u de lijst met leads kunt ophalen die zijn ontvangen van de micro soft Solution Provider-pagina en verkoop kansen die zijn ontvangen van micro soft-verkopers of andere partners.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-106">This topic explains how to get the list of leads received from Microsoft solution provider page and co-sell opportunities received from Microsoft sellers or other partners.</span></span> <span data-ttu-id="dd4a4-107">Hiermee haalt u ook de lijst met verkoop kansen of pijplijn deals op die door uw organisatie zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-107">This will also fetch the list of co-sell opportunities or pipeline deals created by your organization.</span></span>

> [!Note]
> <span data-ttu-id="dd4a4-108">Leads die zijn ontvangen van de micro soft Commercial Marketplace (Azure Marketplace en AppSource) worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-108">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dd4a4-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dd4a4-109">Prerequisites</span></span>

- <span data-ttu-id="dd4a4-110">Referenties zoals beschreven in [partner API-verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="dd4a4-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="dd4a4-111">Dit scenario ondersteunt verificatie met app + gebruikers referenties.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="dd4a4-112">Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, referentie beheerder of verwijzings gebruiker.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="dd4a4-113">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="dd4a4-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dd4a4-114">Syntaxis van aanvraag</span><span class="sxs-lookup"><span data-stu-id="dd4a4-114">Request syntax</span></span>

| <span data-ttu-id="dd4a4-115">Methode</span><span class="sxs-lookup"><span data-stu-id="dd4a4-115">Method</span></span>  | <span data-ttu-id="dd4a4-116">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="dd4a4-116">Request URI</span></span>                                                    |
|:--------|:---------------------------------------------------------------|
| <span data-ttu-id="dd4a4-117">**Toevoegen**</span><span class="sxs-lookup"><span data-stu-id="dd4a4-117">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

#### <a name="supported-odata-operations"></a><span data-ttu-id="dd4a4-118">Ondersteunde OData-bewerkingen</span><span class="sxs-lookup"><span data-stu-id="dd4a4-118">Supported OData operations</span></span>

| <span data-ttu-id="dd4a4-119">Naam</span><span class="sxs-lookup"><span data-stu-id="dd4a4-119">Name</span></span>     | <span data-ttu-id="dd4a4-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dd4a4-120">Description</span></span>     | <span data-ttu-id="dd4a4-121">Vereist</span><span class="sxs-lookup"><span data-stu-id="dd4a4-121">Required</span></span>    | <span data-ttu-id="dd4a4-122">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="dd4a4-122">Example</span></span>                                                                                                                                                                                                                                                     |
|:---------|:----------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dd4a4-123">$select</span><span class="sxs-lookup"><span data-stu-id="dd4a4-123">$select</span></span>  | <span data-ttu-id="dd4a4-124">Velden selecteren</span><span class="sxs-lookup"><span data-stu-id="dd4a4-124">Selects fields</span></span>  | <span data-ttu-id="dd4a4-125">No</span><span class="sxs-lookup"><span data-stu-id="dd4a4-125">No</span></span>          | `/referrals?$select=id,status,customerProfile`                                                                                                                                                                                                              |
| <span data-ttu-id="dd4a4-126">$filter</span><span class="sxs-lookup"><span data-stu-id="dd4a4-126">$filter</span></span>  | <span data-ttu-id="dd4a4-127">Filtert resultaten</span><span class="sxs-lookup"><span data-stu-id="dd4a4-127">Filters results</span></span> | <span data-ttu-id="dd4a4-128">Aanbevolen</span><span class="sxs-lookup"><span data-stu-id="dd4a4-128">Recommended</span></span> | `/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'` <br/> `/referrals?$filter=status eq 'New' and qualification eq 'SalesQualified'` <br/> `/referrals?$filter=customerProfile/address/country eq 'US' and direction eq 'Incoming'` |
| <span data-ttu-id="dd4a4-129">$orderby</span><span class="sxs-lookup"><span data-stu-id="dd4a4-129">$orderby</span></span> | <span data-ttu-id="dd4a4-130">Resultaten van orders</span><span class="sxs-lookup"><span data-stu-id="dd4a4-130">Orders results</span></span>  | <span data-ttu-id="dd4a4-131">Aanbevolen</span><span class="sxs-lookup"><span data-stu-id="dd4a4-131">Recommended</span></span> | `/referrals?$orderby=createdDateTime desc`                                                                                                                                                                                                                  |

#### <a name="supported-orderby-parameters"></a><span data-ttu-id="dd4a4-132">Ondersteunde OrderBy-para meters</span><span class="sxs-lookup"><span data-stu-id="dd4a4-132">Supported orderby parameters</span></span>

<span data-ttu-id="dd4a4-133">Gebruik de volgende $orderby para meters om de lijst met leads en kansen te sorteren</span><span class="sxs-lookup"><span data-stu-id="dd4a4-133">Use the following $orderby parameters to sort the list of leads and opportunities</span></span>

| <span data-ttu-id="dd4a4-134">Naam</span><span class="sxs-lookup"><span data-stu-id="dd4a4-134">Name</span></span>            | <span data-ttu-id="dd4a4-135">Type</span><span class="sxs-lookup"><span data-stu-id="dd4a4-135">Type</span></span>     | <span data-ttu-id="dd4a4-136">Description</span><span class="sxs-lookup"><span data-stu-id="dd4a4-136">Description</span></span>                                       |
|:----------------|:---------|:--------------------------------------------------|
| <span data-ttu-id="dd4a4-137">createdDateTime</span><span class="sxs-lookup"><span data-stu-id="dd4a4-137">createdDateTime</span></span> | <span data-ttu-id="dd4a4-138">DateTime</span><span class="sxs-lookup"><span data-stu-id="dd4a4-138">DateTime</span></span> | <span data-ttu-id="dd4a4-139">Aanmaak datum en-tijd van de lead of kans</span><span class="sxs-lookup"><span data-stu-id="dd4a4-139">Creation date and time of the lead or opportunity</span></span> |
| <span data-ttu-id="dd4a4-140">updatedDateTime</span><span class="sxs-lookup"><span data-stu-id="dd4a4-140">updatedDateTime</span></span> | <span data-ttu-id="dd4a4-141">DateTime</span><span class="sxs-lookup"><span data-stu-id="dd4a4-141">DateTime</span></span> | <span data-ttu-id="dd4a4-142">De datum en tijd van de lead of de opportuniteit bijwerken</span><span class="sxs-lookup"><span data-stu-id="dd4a4-142">Update date and time of the lead or opportunity</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="dd4a4-143">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="dd4a4-143">Request headers</span></span>

<span data-ttu-id="dd4a4-144">Zie [partner rest headers](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-144">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="dd4a4-145">Aanvraagbody</span><span class="sxs-lookup"><span data-stu-id="dd4a4-145">Request body</span></span>

<span data-ttu-id="dd4a4-146">Geen.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="dd4a4-147">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="dd4a4-147">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$orderby=createdDateTime desc HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="dd4a4-148">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="dd4a4-148">REST response</span></span>

<span data-ttu-id="dd4a4-149">Als dit lukt, bevat de antwoord tekst een verzameling [leads en/of verkoop kansen](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="dd4a4-149">If successful, the response body contains a collection of [leads and/or opportunities](referral-resources.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dd4a4-150">Geslaagde en fout codes</span><span class="sxs-lookup"><span data-stu-id="dd4a4-150">Response success and error codes</span></span>

<span data-ttu-id="dd4a4-151">Elk antwoord wordt geleverd met een [HTTP-status code](error-codes.md) die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-151">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dd4a4-152">Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-152">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="dd4a4-153">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="dd4a4-153">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
  "@odata.context": "http://api.partner.microsoft.com/v1.0/$metadata#Referrals",
  "@odata.count": 1,
  "value": [
    {
      "id": "c5fbb3b6-be74-4795-9fb5-4324c73fed37",
      "engagementId": "65edc0b5-3485-41b7-a17e-dfa9ef4706e2",
      "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
      "organizationName": "Contoso Company",
      "createdDateTime": "2020-10-30T21:03:00.0000000Z",
      "updatedDateTime": "2020-10-30T21:03:00.0000000Z",
      "status": "New",
      "substatus": "Pending",
      "qualification": "Direct",
      "type": "Independent",
      "direction": "Incoming",
      "customerProfile": {
        "name": "Fabrikam Customer Inc",
        "address": {
          "addressLine1": "One Microsoft Way",
          "addressLine2": "",
          "city": "Redmond",
          "state": "WA",
          "postalCode": "98052",
          "country": "US"
        }
      },
      "details": {
        "notes": "We are interested in deploying Microsoft 365 and are looking for support in training our employees. Can you help?",
        "dealValue": 10000,
        "currency": "USD",
        "closingDateTime": "2020-12-01T00:00:00Z",
        "requirements": {
            "industries": [ { "id": "Education" } ],
            "products": [ { "id": "Microsoft365" } ],
            "services": [ { "id": "LearningAndCertification" } ],
            "solutions": [ { "id": "SOL-Microsoft365", "name": "Microsoft365" }
          ]
        }
      },
      "links": {
        "relatedReferrals": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
          "method": "GET"
        },
        "self": {
          "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals/c5fbb3b6-be74-4795-9fb5-4324c73fed37",
          "method": "GET"
        }
      }
    }
  ],
  "@odata.nextLink": "http://api.partner.microsoft.com/v1.0/referrals?$skiptoken=k181pEdP0ykypkieJfcxX"
}
```

<span data-ttu-id="dd4a4-154">Gebruik de `@odata.nextLink` om de volgende pagina met resultaten op te halen.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-154">Use the `@odata.nextLink` to get the next page of results.</span></span>

> [!Note]
> <span data-ttu-id="dd4a4-155">De velden in het bovenstaande voor beeld illustratration zijn niet volledig.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-155">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="dd4a4-156">Het daad werkelijke API-antwoord bevat meer velden, zoals de klant en partner teams.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-156">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="dd4a4-157">Zie [Referral resources](referral-resources.md)voor een volledige lijst met ondersteunde velden.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-157">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>

## <a name="sample-requests"></a><span data-ttu-id="dd4a4-158">Voorbeeld aanvragen</span><span class="sxs-lookup"><span data-stu-id="dd4a4-158">Sample requests</span></span>

1. <span data-ttu-id="dd4a4-159">Hiermee worden de Top 10 van de meest recente inkomende mogelijkheden voor co-sell opgehaald.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-159">Gets the top 10 most recent inbound co-sell opportunities.</span></span> <span data-ttu-id="dd4a4-160">De aanvraag haalt verkoop kansen op die zijn geïnitieerd door een vertegenwoordiger van micro soft of een andere partner, waarbij uw organisatie wordt uitgenodigd om deel te nemen aan een mede-verkoop activiteit.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-160">The request will fetch opportunities initiated by a Microsoft sales representative or another partner, inviting your organization to participate in a co-selling activity.</span></span>
    
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(type eq 'Shared' and direction eq 'Incoming')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

2. <span data-ttu-id="dd4a4-161">Haalt de meest recente inkomende leads en verkoop kansen op waarop niet is gereageerd.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-161">Gets the most recent inbound leads and opportunities that have not been responded to.</span></span>  

    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$top=10&$filter=(direction eq 'Incoming' and substatus eq 'Pending')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```

    > [!Important]
    > <span data-ttu-id="dd4a4-162">Als u niet binnen de toegewezen tijd (momenteel 14 dagen) op een lead of verkoop kans reageert, worden deze gearchiveerd als verlopen en wordt micro soft of de partner die u deze mogelijkheid heeft gestuurd.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-162">If you don't respond to a lead or opportunity within the allotted time (currently 14 days), we'll archive it as Expired and notify either Microsoft or the partner who sent you this opportunity.</span></span>

3. <span data-ttu-id="dd4a4-163">Hiermee worden de meest recente actieve verkoop kansen opgehaald die door uw organisatie zijn gestart en aan een specifieke verkoper worden door gegeven.</span><span class="sxs-lookup"><span data-stu-id="dd4a4-163">Gets the most recent active co-sell opportunities initiated by your organization and being worked on by a specific seller.</span></span>
    ```http
    GET https://api.partner.microsoft.com/v1.0/engagements/referrals?$filter=status eq 'Active' and direction eq 'Outgoing' and type eq 'Shared' and team/any(t:t/email eq 'r2d2@contoso.com')&$orderby=createdDateTime desc HTTP/1.1
    Authorization: Bearer <token>
    Content-Type: application/json
    ```
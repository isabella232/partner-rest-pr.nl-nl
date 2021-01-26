---
title: Een lead of verkoopkans ophalen op basis van id
description: Een lead of verkoop kans ophalen op basis van de id.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcfaea393afc6a9d09946b4c31b7168ba26aa255
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770421"
---
# <a name="get-a-lead-or-opportunity-by-id"></a><span data-ttu-id="a844d-103">Een lead of verkoopkans ophalen op basis van id</span><span class="sxs-lookup"><span data-stu-id="a844d-103">Get a lead or opportunity by Id</span></span>

<span data-ttu-id="a844d-104">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="a844d-104">Applies to:</span></span>

- <span data-ttu-id="a844d-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="a844d-105">Partner API</span></span>

<span data-ttu-id="a844d-106">In dit onderwerp wordt uitgelegd hoe u een lead of verkoop kansen op basis van id krijgt.</span><span class="sxs-lookup"><span data-stu-id="a844d-106">This topic explains how to get a lead or co-sell opportunity by Id.</span></span>

> [!Note]
> <span data-ttu-id="a844d-107">Leads die zijn ontvangen van de micro soft Commercial Marketplace (Azure Marketplace en AppSource) worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a844d-107">Leads received from the Microsoft commercial marketplace (Azure Marketplace and AppSource) are not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a844d-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a844d-108">Prerequisites</span></span>

- <span data-ttu-id="a844d-109">Referenties zoals beschreven in [partner API-verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="a844d-109">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="a844d-110">Dit scenario ondersteunt verificatie met app + gebruikers referenties.</span><span class="sxs-lookup"><span data-stu-id="a844d-110">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="a844d-111">Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, referentie beheerder of verwijzings gebruiker.</span><span class="sxs-lookup"><span data-stu-id="a844d-111">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a844d-112">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="a844d-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a844d-113">Syntaxis van aanvraag</span><span class="sxs-lookup"><span data-stu-id="a844d-113">Request syntax</span></span>

| <span data-ttu-id="a844d-114">Methode</span><span class="sxs-lookup"><span data-stu-id="a844d-114">Method</span></span>   | <span data-ttu-id="a844d-115">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="a844d-115">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a844d-116">**Toevoegen**</span><span class="sxs-lookup"><span data-stu-id="a844d-116">**GET**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}>                                     |

### <a name="uri-parameter"></a><span data-ttu-id="a844d-117">URI-para meter</span><span class="sxs-lookup"><span data-stu-id="a844d-117">URI parameter</span></span>


| <span data-ttu-id="a844d-118">Naam</span><span class="sxs-lookup"><span data-stu-id="a844d-118">Name</span></span>                   | <span data-ttu-id="a844d-119">Type</span><span class="sxs-lookup"><span data-stu-id="a844d-119">Type</span></span>     | <span data-ttu-id="a844d-120">Vereist</span><span class="sxs-lookup"><span data-stu-id="a844d-120">Required</span></span> | <span data-ttu-id="a844d-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a844d-121">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="a844d-122">Id</span><span class="sxs-lookup"><span data-stu-id="a844d-122">Id</span></span>                      | <span data-ttu-id="a844d-123">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a844d-123">string</span></span>   | <span data-ttu-id="a844d-124">Yes</span><span class="sxs-lookup"><span data-stu-id="a844d-124">Yes</span></span>       | <span data-ttu-id="a844d-125">De unieke id voor een lead of een verkoop kans op verkoop</span><span class="sxs-lookup"><span data-stu-id="a844d-125">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="a844d-126">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="a844d-126">Request headers</span></span>

<span data-ttu-id="a844d-127">Zie [partner rest headers](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a844d-127">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="a844d-128">Aanvraagbody</span><span class="sxs-lookup"><span data-stu-id="a844d-128">Request body</span></span>

<span data-ttu-id="a844d-129">Geen.</span><span class="sxs-lookup"><span data-stu-id="a844d-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a844d-130">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="a844d-130">Request example</span></span>

```http
GET https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id} HTTP/1.1
Authorization: Bearer <token>
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="a844d-131">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="a844d-131">REST response</span></span>

<span data-ttu-id="a844d-132">Als dit lukt, bevat de antwoord tekst de [lead of de opportuniteit](referral-resources.md) die overeenkomt met de id.</span><span class="sxs-lookup"><span data-stu-id="a844d-132">If successful, the response body contains the [lead or opportunity](referral-resources.md) matching the Id.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a844d-133">Geslaagde en fout codes</span><span class="sxs-lookup"><span data-stu-id="a844d-133">Response success and error codes</span></span>

<span data-ttu-id="a844d-134">Elk antwoord wordt geleverd met een [HTTP-status code](error-codes.md) die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing.</span><span class="sxs-lookup"><span data-stu-id="a844d-134">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a844d-135">Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.</span><span class="sxs-lookup"><span data-stu-id="a844d-135">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="a844d-136">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="a844d-136">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Type: application/json
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731

{
    "@odata.context": "https://api.partner.microsoft.com/v1.0/engagments/referrals/$metadata#Referrals/$entity",
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
      "notes": "We are interested in deploying Microsoft 365 and are looking forsupport in training our employees. Can you help?",
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
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referrals$filter=engagementId eq '65edc0b5-3485-41b7-a17e-dfa9ef4706e2'",
        "method": "GET"
      },
      "self": {
        "uri": "https://api.partner.microsoft.com/v1.0/engagements/referralsc5fbb3b6-be74-4795-9fb5-4324c73fed37",
        "method": "GET"
      }
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\""
}
```

> [!Note]
> <span data-ttu-id="a844d-137">De velden in het bovenstaande voor beeld illustratration zijn niet volledig.</span><span class="sxs-lookup"><span data-stu-id="a844d-137">The fields in the example illustratration above are not exhaustive.</span></span> <span data-ttu-id="a844d-138">Het daad werkelijke API-antwoord bevat meer velden, zoals de klant en partner teams.</span><span class="sxs-lookup"><span data-stu-id="a844d-138">The actual API response contains more fields like the customer and partner teams.</span></span> <span data-ttu-id="a844d-139">Zie [Referral resources](referral-resources.md)voor een volledige lijst met ondersteunde velden.</span><span class="sxs-lookup"><span data-stu-id="a844d-139">For the full list of supported fields, see [referral resources](referral-resources.md).</span></span>
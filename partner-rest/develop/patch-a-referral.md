---
title: Een lead of verkoopkans bijwerken
description: Hiermee kunt u de details van de lead of de opportuniteit bijwerken.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: abfe7308f46cd65b9358b369f6fa05bcca4c1df2
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770424"
---
# <a name="update-a-lead-or-opportunity"></a><span data-ttu-id="76359-103">Een lead of verkoopkans bijwerken</span><span class="sxs-lookup"><span data-stu-id="76359-103">Update a lead or opportunity</span></span>

<span data-ttu-id="76359-104">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="76359-104">Applies to:</span></span>

- <span data-ttu-id="76359-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="76359-105">Partner API</span></span>

<span data-ttu-id="76359-106">In dit onderwerp wordt uitgelegd hoe u de lead-of verkoopkansgegevens, zoals de deal waarde, de geschatte Sluitings datum, of de verkoop stadia onder andere details bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="76359-106">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76359-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="76359-107">Prerequisites</span></span>

- <span data-ttu-id="76359-108">Referenties zoals beschreven in [partner API-verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="76359-108">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="76359-109">Dit scenario ondersteunt verificatie met app + gebruikers referenties.</span><span class="sxs-lookup"><span data-stu-id="76359-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="76359-110">Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, referentie beheerder of verwijzings gebruiker.</span><span class="sxs-lookup"><span data-stu-id="76359-110">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="76359-111">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="76359-111">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="76359-112">Syntaxis van aanvraag</span><span class="sxs-lookup"><span data-stu-id="76359-112">Request syntax</span></span>

| <span data-ttu-id="76359-113">Methode</span><span class="sxs-lookup"><span data-stu-id="76359-113">Method</span></span>  | <span data-ttu-id="76359-114">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="76359-114">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="76359-115">**VERZENDEN**</span><span class="sxs-lookup"><span data-stu-id="76359-115">**PATCH**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="uri-parameter"></a><span data-ttu-id="76359-116">URI-para meter</span><span class="sxs-lookup"><span data-stu-id="76359-116">URI parameter</span></span>


| <span data-ttu-id="76359-117">Naam</span><span class="sxs-lookup"><span data-stu-id="76359-117">Name</span></span>                   | <span data-ttu-id="76359-118">Type</span><span class="sxs-lookup"><span data-stu-id="76359-118">Type</span></span>     | <span data-ttu-id="76359-119">Vereist</span><span class="sxs-lookup"><span data-stu-id="76359-119">Required</span></span> | <span data-ttu-id="76359-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="76359-120">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
|<span data-ttu-id="76359-121">Id</span><span class="sxs-lookup"><span data-stu-id="76359-121">Id</span></span>                      | <span data-ttu-id="76359-122">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76359-122">string</span></span>   | <span data-ttu-id="76359-123">Yes</span><span class="sxs-lookup"><span data-stu-id="76359-123">Yes</span></span>       | <span data-ttu-id="76359-124">De unieke id voor een lead of een verkoop kans op verkoop</span><span class="sxs-lookup"><span data-stu-id="76359-124">The unique identifier for a lead or co-sell opportunity</span></span>       |

### <a name="request-headers"></a><span data-ttu-id="76359-125">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="76359-125">Request headers</span></span>

<span data-ttu-id="76359-126">Zie [partner rest headers](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="76359-126">See [Partner REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="76359-127">Aanvraagbody</span><span class="sxs-lookup"><span data-stu-id="76359-127">Request body</span></span>

<span data-ttu-id="76359-128">De aanvraag tekst volgt de indeling van de [JSON-patch](https://tools.ietf.org/html/rfc6902) .</span><span class="sxs-lookup"><span data-stu-id="76359-128">The request body follows the [Json Patch](https://tools.ietf.org/html/rfc6902) format.</span></span> <span data-ttu-id="76359-129">Een JSON-patch document heeft een matrix met bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="76359-129">A JSON Patch document has an array of operations.</span></span> <span data-ttu-id="76359-130">Elke bewerking identificeert een bepaald type wijziging.</span><span class="sxs-lookup"><span data-stu-id="76359-130">Each operation identifies a particular type of change.</span></span> <span data-ttu-id="76359-131">Voor beelden van dergelijke wijzigingen zijn het toevoegen van een matrix element of het vervangen van een eigenschaps waarde.</span><span class="sxs-lookup"><span data-stu-id="76359-131">Examples of such changes include adding an array element or replacing a property value.</span></span>

> [!Important]
> <span data-ttu-id="76359-132">De API ondersteunt momenteel alleen de `replace` `add` bewerkingen en.</span><span class="sxs-lookup"><span data-stu-id="76359-132">The API currently only supports the `replace` and `add` operations.</span></span>

### <a name="request-example"></a><span data-ttu-id="76359-133">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="76359-133">Request example</span></span>

```http
PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
Authorization: Bearer <token>
Content-Type: application/json
Prefer: return=representation

[
    {
        "op": "replace",
        "path": "/details/dealValue",
        "value": "10000"
    },
    {
        "op": "add",
        "path": "/team/-",
        "value": {
            "email": "jane.doe@contoso.com",
            "firstName": "Jane",
            "lastName": "Doe",
            "phoneNumber": "0000000001"
        }
    }
]
```

> [!Note]
> <span data-ttu-id="76359-134">Als de **if-match-** header wordt door gegeven, wordt deze gebruikt voor gelijktijdigheids beheer.</span><span class="sxs-lookup"><span data-stu-id="76359-134">If the **If-Match** header is passed, it will be used for concurrency control.</span></span>

## <a name="rest-response"></a><span data-ttu-id="76359-135">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="76359-135">REST Response</span></span>

<span data-ttu-id="76359-136">Als dit lukt, bevat de antwoord tekst de bijgewerkte [lead of verkoop kans](referral-resources.md).</span><span class="sxs-lookup"><span data-stu-id="76359-136">If successful, the response body contains the updated [lead or opportunity](referral-resources.md).</span></span>


### <a name="response-success-and-error-codes"></a><span data-ttu-id="76359-137">Geslaagde en fout codes</span><span class="sxs-lookup"><span data-stu-id="76359-137">Response success and error codes</span></span>

<span data-ttu-id="76359-138">Elk antwoord wordt geleverd met een [HTTP-status code](error-codes.md) die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing.</span><span class="sxs-lookup"><span data-stu-id="76359-138">Each response comes with an [HTTP status code](error-codes.md) that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="76359-139">Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.</span><span class="sxs-lookup"><span data-stu-id="76359-139">Use a network trace tool to read this code, the error type, and additional parameters.</span></span>

### <a name="response-example"></a><span data-ttu-id="76359-140">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="76359-140">Response example</span></span>

``` http
HTTP/1.1 204 No Content
Content-Length: 0
Request-ID: 9f8bed52-e4df-4d0c-9ca6-929a187b0731
```

> [!Tip]
> <span data-ttu-id="76359-141">De antwoord tekst is afhankelijk van de voor **Keurs** -header.</span><span class="sxs-lookup"><span data-stu-id="76359-141">The response body depends on the **Prefer** header.</span></span> <span data-ttu-id="76359-142">Als de waarde van de header wordt wegge laten in de aanvraag, is de antwoord tekst leeg met de HTTP-status code 204.</span><span class="sxs-lookup"><span data-stu-id="76359-142">If the header value is omitted in the request, the response body is empty with a HTTP Status code 204.</span></span> <span data-ttu-id="76359-143">Voeg toe `Prefer: return=representation` aan de koptekst om de bijgewerkte lead of verkoop kans te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="76359-143">Add `Prefer: return=representation` to the header to get the updated lead or opportunity.</span></span>

## <a name="sample-requests"></a><span data-ttu-id="76359-144">Voorbeeld aanvragen</span><span class="sxs-lookup"><span data-stu-id="76359-144">Sample requests</span></span>

1. <span data-ttu-id="76359-145">Hiermee wordt de deal waarde voor de verkoop kans bijgewerkt naar 10000 en worden de notities bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="76359-145">Updates the deal value for the opportunity to 10000 and updates the notes.</span></span> <span data-ttu-id="76359-146">Er zijn geen gelijktijdigheids controles mogelijk vanwege de er zijn van de `If-Match` header.</span><span class="sxs-lookup"><span data-stu-id="76359-146">There are no concurrency checks because of the absense of the `If-Match` header.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace","path":"/details/dealValue","value":"10000"},
        {"op":"replace","path":"/details/notes","value":"Lorem ipsum dolor sit amet."}
    ]
    ```

2. <span data-ttu-id="76359-147">Hiermee wordt de status van een lead of verkoop kans bijgewerkt naar binnengehaald.</span><span class="sxs-lookup"><span data-stu-id="76359-147">Updates the status of a lead or opportunity to Won.</span></span>
    
    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    
    [
        {"op":"replace", "path":"/status", "value":"Closed"},
        {"op":"replace", "path":"/substatus", "value":"Won"}
    ]
    ```

    > [!Important]
    > <span data-ttu-id="76359-148">De `status` `substatus` velden en moeten overeenkomen met de toegestane set overgangs waarden, zoals [hier](referral-resources.md)wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="76359-148">The `status` and `substatus` fields should conform to the allowed set of transition values as described [here](referral-resources.md).</span></span>

3. <span data-ttu-id="76359-149">Voegt een nieuw lid van uw organisatie toe aan het team van lead of verkoop kansen.</span><span class="sxs-lookup"><span data-stu-id="76359-149">Adds a new member from your organization to the lead or opportunity team.</span></span> <span data-ttu-id="76359-150">Het antwoord bevat de bijgewerkte lead of verkoop kans vanwege de aanwezigheid van de `Prefer: return=representation` header.</span><span class="sxs-lookup"><span data-stu-id="76359-150">The response will contain the updated lead or opportunity because of the presence of the `Prefer: return=representation` header.</span></span>

    ```http
    PATCH https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}
    Authorization: Bearer <token>
    Content-Type: application/json
    Prefer: return=representation
    
    [
        {
            "op": "add",
            "path": "/team/-",
            "value": {
                "email": "jane.doe@contoso.com",
                "firstName": "Jane",
                "lastName": "Doe",
                "phoneNumber": "0000000001"
            }
        }
    ]
    ```

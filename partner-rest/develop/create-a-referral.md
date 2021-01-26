---
title: Een verwijzing maken
description: Maak onafhankelijke of gedeelde verwijzingen in de partner-API.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 6aab4b5f45030c3c16294b2929b1a6d3086fb951
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770408"
---
# <a name="create-a-referral"></a><span data-ttu-id="5b50f-103">Een verwijzing maken</span><span class="sxs-lookup"><span data-stu-id="5b50f-103">Create a referral</span></span>

<span data-ttu-id="5b50f-104">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="5b50f-104">Applies to:</span></span>

- <span data-ttu-id="5b50f-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="5b50f-105">Partner API</span></span>

<span data-ttu-id="5b50f-106">In dit onderwerp wordt uitgelegd hoe u een verwijzing maakt.</span><span class="sxs-lookup"><span data-stu-id="5b50f-106">This topic explains how to create a referral.</span></span> <span data-ttu-id="5b50f-107">Er zijn twee soorten [ReferralType](referral-resources.md#referraltype):</span><span class="sxs-lookup"><span data-stu-id="5b50f-107">There are two types of [ReferralType](referral-resources.md#referraltype):</span></span>

1. <span data-ttu-id="5b50f-108">Onafhankelijk: een verwijzing is zichtbaar voor één partner.</span><span class="sxs-lookup"><span data-stu-id="5b50f-108">Independent: Where a referral is visible to one partner.</span></span>
2. <span data-ttu-id="5b50f-109">Gedeeld: wanneer een verwijzing zichtbaar is voor twee partijen die samen werken.</span><span class="sxs-lookup"><span data-stu-id="5b50f-109">Shared: Where a referral is visible to two parties that are working together.</span></span> <span data-ttu-id="5b50f-110">Als micro soft en een partner bijvoorbeeld samen werken in een mede-verkoop transactie, kan een verwijzing tussen beide partijen worden gedeeld.</span><span class="sxs-lookup"><span data-stu-id="5b50f-110">For example, if Microsoft and a partner are working together in a co-selling deal, a referral can be shared between both parties.</span></span> <span data-ttu-id="5b50f-111">Zie de sectie [een gedeelde verwijzing maken](#create-a-shared-referral)voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5b50f-111">For more information, see the section [Creating a shared referral](#create-a-shared-referral).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b50f-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5b50f-112">Prerequisites</span></span>

- <span data-ttu-id="5b50f-113">Referenties zoals beschreven in [partner API-verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5b50f-113">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="5b50f-114">Dit scenario ondersteunt verificatie met app + gebruikers referenties.</span><span class="sxs-lookup"><span data-stu-id="5b50f-114">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5b50f-115">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="5b50f-115">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5b50f-116">Syntaxis van aanvraag</span><span class="sxs-lookup"><span data-stu-id="5b50f-116">Request syntax</span></span>

| <span data-ttu-id="5b50f-117">Methode</span><span class="sxs-lookup"><span data-stu-id="5b50f-117">Method</span></span>  | <span data-ttu-id="5b50f-118">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="5b50f-118">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="5b50f-119">**Verzenden**</span><span class="sxs-lookup"><span data-stu-id="5b50f-119">**POST**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals> |

### <a name="request-headers"></a><span data-ttu-id="5b50f-120">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="5b50f-120">Request headers</span></span>

- <span data-ttu-id="5b50f-121">Zie de REST-headers van de [partner-API](headers.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5b50f-121">See [Partner API REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="5b50f-122">Aanvraagbody</span><span class="sxs-lookup"><span data-stu-id="5b50f-122">Request body</span></span>

<span data-ttu-id="5b50f-123">In deze tabel worden de [verwijzings](referral-resources.md) eigenschappen in de hoofd tekst van de aanvraag voor een gloed nieuwe verwijzing beschreven.</span><span class="sxs-lookup"><span data-stu-id="5b50f-123">This table describes the [Referral](referral-resources.md) properties in the request body for a brand new referral.</span></span>

| <span data-ttu-id="5b50f-124">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5b50f-124">Property</span></span>            | <span data-ttu-id="5b50f-125">Type</span><span class="sxs-lookup"><span data-stu-id="5b50f-125">Type</span></span>                                                                 | <span data-ttu-id="5b50f-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5b50f-126">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5b50f-127">Name</span><span class="sxs-lookup"><span data-stu-id="5b50f-127">Name</span></span>                | <span data-ttu-id="5b50f-128">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b50f-128">string</span></span>                                                               | <span data-ttu-id="5b50f-129">De naam van de verwijzing.</span><span class="sxs-lookup"><span data-stu-id="5b50f-129">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="5b50f-130">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="5b50f-130">ExternalReferenceId</span></span> | <span data-ttu-id="5b50f-131">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b50f-131">string</span></span>                                                               | <span data-ttu-id="5b50f-132">Een externe ID voor de verwijzing.</span><span class="sxs-lookup"><span data-stu-id="5b50f-132">An external identifier for the referral.</span></span> <span data-ttu-id="5b50f-133">Bijvoorbeeld uw eigen Dynamics 365-lead-of verkoop kans-ID.</span><span class="sxs-lookup"><span data-stu-id="5b50f-133">For example, your own Dynamics 365 lead or opportunity ID.</span></span>                   |
| <span data-ttu-id="5b50f-134">Status</span><span class="sxs-lookup"><span data-stu-id="5b50f-134">Status</span></span>              | [<span data-ttu-id="5b50f-135">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="5b50f-135">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="5b50f-136">Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven.</span><span class="sxs-lookup"><span data-stu-id="5b50f-136">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="5b50f-137">Substatus</span><span class="sxs-lookup"><span data-stu-id="5b50f-137">Substatus</span></span>           | [<span data-ttu-id="5b50f-138">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="5b50f-138">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="5b50f-139">Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de substatus van de verwijzing aangeven.</span><span class="sxs-lookup"><span data-stu-id="5b50f-139">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral substatus.</span></span>       |
| <span data-ttu-id="5b50f-140">StatusReason</span><span class="sxs-lookup"><span data-stu-id="5b50f-140">StatusReason</span></span>        | <span data-ttu-id="5b50f-141">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5b50f-141">string</span></span>                                                               | <span data-ttu-id="5b50f-142">Een beschrijvende bericht over de status.</span><span class="sxs-lookup"><span data-stu-id="5b50f-142">A descriptive message about the status.</span></span> <span data-ttu-id="5b50f-143">Leg bijvoorbeeld uit waarom de Referral verloren is gegaan.</span><span class="sxs-lookup"><span data-stu-id="5b50f-143">For example, explain why the referral was lost.</span></span>                            |
| <span data-ttu-id="5b50f-144">ReferralType</span><span class="sxs-lookup"><span data-stu-id="5b50f-144">ReferralType</span></span>        | [<span data-ttu-id="5b50f-145">ReferralType</span><span class="sxs-lookup"><span data-stu-id="5b50f-145">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="5b50f-146">Hiermee wordt het verwijzings type aangeduid.</span><span class="sxs-lookup"><span data-stu-id="5b50f-146">Represents the referral type.</span></span> <span data-ttu-id="5b50f-147">**Vereist.**</span><span class="sxs-lookup"><span data-stu-id="5b50f-147">**Required.**</span></span>                                                                                        |
| <span data-ttu-id="5b50f-148">Kwalificatie</span><span class="sxs-lookup"><span data-stu-id="5b50f-148">Qualification</span></span>       | [<span data-ttu-id="5b50f-149">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="5b50f-149">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="5b50f-150">Vertegenwoordigt de kwaliteit van de verwijzing.</span><span class="sxs-lookup"><span data-stu-id="5b50f-150">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="5b50f-151">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="5b50f-151">CustomerProfile</span></span>     | [<span data-ttu-id="5b50f-152">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="5b50f-152">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="5b50f-153">Contact gegevens van de klant.</span><span class="sxs-lookup"><span data-stu-id="5b50f-153">Customer contact information.</span></span>  <span data-ttu-id="5b50f-154">**Vereist.**</span><span class="sxs-lookup"><span data-stu-id="5b50f-154">**Required.**</span></span>                                                                                      |
| <span data-ttu-id="5b50f-155">Toestemming</span><span class="sxs-lookup"><span data-stu-id="5b50f-155">Consent</span></span>             | [<span data-ttu-id="5b50f-156">Toestemming</span><span class="sxs-lookup"><span data-stu-id="5b50f-156">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="5b50f-157">Markering van toestemming voor het delen van gegevens met andere organisaties, zodat ze contact kunnen opnemen met de gebruikers. **Vereist.**</span><span class="sxs-lookup"><span data-stu-id="5b50f-157">Consent flags around sharing information with other organizations and allowing them to contact users.**Required.**</span></span>               |
| <span data-ttu-id="5b50f-158">Details</span><span class="sxs-lookup"><span data-stu-id="5b50f-158">Details</span></span>             | [<span data-ttu-id="5b50f-159">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="5b50f-159">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="5b50f-160">Details van klant, notities, deal waarde, valuta afsluitings datum.</span><span class="sxs-lookup"><span data-stu-id="5b50f-160">Customer details, notes, deal value, currency closing date.</span></span> <span data-ttu-id="5b50f-161">**Vereist.**</span><span class="sxs-lookup"><span data-stu-id="5b50f-161">**Required.**</span></span>                                                           |
| <span data-ttu-id="5b50f-162">Team</span><span class="sxs-lookup"><span data-stu-id="5b50f-162">Team</span></span>                | [<span data-ttu-id="5b50f-163">Lid</span><span class="sxs-lookup"><span data-stu-id="5b50f-163">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="5b50f-164">Vertegenwoordigt gebruikers in de organisaties die betrokken zijn bij de partner engagement.</span><span class="sxs-lookup"><span data-stu-id="5b50f-164">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="5b50f-165">InviteContext</span><span class="sxs-lookup"><span data-stu-id="5b50f-165">InviteContext</span></span>       | [<span data-ttu-id="5b50f-166">InviteContext</span><span class="sxs-lookup"><span data-stu-id="5b50f-166">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="5b50f-167">Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.</span><span class="sxs-lookup"><span data-stu-id="5b50f-167">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="5b50f-168">Doel</span><span class="sxs-lookup"><span data-stu-id="5b50f-168">Target</span></span>         | [<span data-ttu-id="5b50f-169">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="5b50f-169">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="5b50f-170">Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.</span><span class="sxs-lookup"><span data-stu-id="5b50f-170">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

#### <a name="status--substatus-transition-states"></a><span data-ttu-id="5b50f-171">Status & overgangs toestanden voor substatus</span><span class="sxs-lookup"><span data-stu-id="5b50f-171">Status & Substatus transition states</span></span>

| <span data-ttu-id="5b50f-172">Status</span><span class="sxs-lookup"><span data-stu-id="5b50f-172">Status</span></span> | <span data-ttu-id="5b50f-173">Status overgang toegestaan</span><span class="sxs-lookup"><span data-stu-id="5b50f-173">Allowed status transition</span></span> | <span data-ttu-id="5b50f-174">Toegestane substatus</span><span class="sxs-lookup"><span data-stu-id="5b50f-174">Allowed substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="5b50f-175">Nieuw</span><span class="sxs-lookup"><span data-stu-id="5b50f-175">New</span></span>    | <span data-ttu-id="5b50f-176">Nieuw, actief, gesloten</span><span class="sxs-lookup"><span data-stu-id="5b50f-176">New, Active, Closed</span></span>       | <span data-ttu-id="5b50f-177">In behandeling, ontvangen</span><span class="sxs-lookup"><span data-stu-id="5b50f-177">Pending, Received</span></span>            |
| <span data-ttu-id="5b50f-178">Actief</span><span class="sxs-lookup"><span data-stu-id="5b50f-178">Active</span></span> | <span data-ttu-id="5b50f-179">Actief, gesloten</span><span class="sxs-lookup"><span data-stu-id="5b50f-179">Active, Closed</span></span>            | <span data-ttu-id="5b50f-180">Geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="5b50f-180">Accepted</span></span>                     |
| <span data-ttu-id="5b50f-181">Gesloten</span><span class="sxs-lookup"><span data-stu-id="5b50f-181">Closed</span></span> | <span data-ttu-id="5b50f-182">Gesloten</span><span class="sxs-lookup"><span data-stu-id="5b50f-182">Closed</span></span>                    | <span data-ttu-id="5b50f-183">Gewonnen, verloren, afgewezen, verlopen</span><span class="sxs-lookup"><span data-stu-id="5b50f-183">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="5b50f-184">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="5b50f-184">Request example</span></span>

```http
POST https://api.partner.microsoft.com/v1.0/engagements/referrals HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "name": "Test Cosell Invite_20",
    "status": "New",
    "substatus": "Pending",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "closingDateTime": "2018-11-14T00:00:00Z",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="5b50f-185">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="5b50f-185">REST Response</span></span>

<span data-ttu-id="5b50f-186">Als dit lukt, retourneert deze methode de gevulde [verwijzings](referral-resources.md) bron in de antwoord tekst.</span><span class="sxs-lookup"><span data-stu-id="5b50f-186">If successful, this method returns the populated [Referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5b50f-187">Geslaagde en fout codes</span><span class="sxs-lookup"><span data-stu-id="5b50f-187">Response success and error codes</span></span>

<span data-ttu-id="5b50f-188">Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing.</span><span class="sxs-lookup"><span data-stu-id="5b50f-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5b50f-189">Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.</span><span class="sxs-lookup"><span data-stu-id="5b50f-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5b50f-190">Zie [fout codes](error-codes.md)voor de volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="5b50f-190">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5b50f-191">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="5b50f-191">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "name": "Test Cosell Invite_20",
    "externalReferenceId": null,
    "createdDateTime": "2019-02-23T02:05:23.2931817Z",
    "updatedDateTime": "2019-02-23T02:05:23.2931817Z",
    "expirationDateTime": null,
    "status": "Active",
    "substatus": "Accepted",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Shared",
    "eTag": "\"00006d10-0000-0000-0000-5c70aa630000\"",
    "target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-34104-EBB"
        }
    ],
    "customerProfile": {
        "name": "Contoso Customer Inc",
        "address": {
            "addressLine1": "One Microsoft Way",
            "addressLine2": "34",
            "city": "Redmond",
            "state": "WA",
            "postalCode": "98052",
            "country": "US"
        },
        "size": "10to50employees",
        "team": [
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Sue",
                "lastName": "Smith",
                "phoneNumber": "1234567890",
                "email": "sue.smith@contoso.com"
            },
            {
                "contactPreference": {
                    "locale": "en-us",
                    "disableNotifications": false
                },
                "firstName": "Joe",
                "lastName": "Hansen",
                "phoneNumber": "4035698759",
                "email": "joe.hansen@contoso.com"
            }
        ],
        "ids": []
    },
    "consent": {
        "consentToToShareInfoWithOthers": true,
        "consentToContact": true
    },
    "details": {
        "notes": "Customer is looking to leverage Dynamics 365 to manage their supply chain. There is also a need to leverage a set of custom apps to enable their business processes.",
        "dealValue": 50000,
        "currency": "USD",
        "requirements": {
            "industries": [
                {
                    "id": "Manufacturing"
                }
            ],
            "products": [
                {
                    "id": "Dynamics365Enterprise"
                }
            ],
            "services": [
                {
                    "id": "DeploymentOrMigration"
                }
            ],
            "solutions": [
                {
                    "name": "Dynamics 365 for Field Service",
                    "type": "Category",
                    "id": "Dynamics365forFieldService"
                }
            ]
        }
    },
    "team": [
        {
            "contactPreference": {
                "locale": "en-us",
                "disableNotifications": false
            },
            "firstName": "John",
            "lastName": "Doe",
            "phoneNumber": "1231231234",
            "email": "john.doe@microsoft.com"
        }
    ],
    "inviteContext": {
        "notes": "Hi ABC Partner, hoping you can help this customer. Thanks, John @ Microsoft",
        "invitedBy": {
            "organizationId": "msft"
        }
    },
    "links": {
        "relatedReferrals": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals?$filter=engagementId eq '37ef26aa-1d15-4533-9f93-a69bd33ab1e5'",
            "method": "GET"
        },
        "self": {
            "uri": "https://api.partner.microsoft.com/v1.0/engagments/referrals/4111fffc-f9ee-4d53-bba6-569135228642",
            "method": "GET"
        }
    }
}
```

## <a name="create-a-shared-referral"></a><span data-ttu-id="5b50f-192">Een gedeelde verwijzing maken</span><span class="sxs-lookup"><span data-stu-id="5b50f-192">Create a shared referral</span></span>

<span data-ttu-id="5b50f-193">Er zijn twee stappen voor het maken van een verwijzing naar het **gedeelde** [verwijzings type](referral-resources.md#referraltype).</span><span class="sxs-lookup"><span data-stu-id="5b50f-193">There are two steps to create a referral of the **Shared** [referral type](referral-resources.md#referraltype).</span></span>

1. [<span data-ttu-id="5b50f-194">Uw gedeelde Referral maken</span><span class="sxs-lookup"><span data-stu-id="5b50f-194">Create your shared referral</span></span>](#create-your-referral)
2. [<span data-ttu-id="5b50f-195">Een verbonden verwijzing maken voor de tweede partij</span><span class="sxs-lookup"><span data-stu-id="5b50f-195">Create a connected referral for the second party</span></span>](#create-a-connected-referral)

<span data-ttu-id="5b50f-196">In het volgende diagram ziet u deze twee stappen bij het maken van een gedeelde verwijzing.</span><span class="sxs-lookup"><span data-stu-id="5b50f-196">The following flow chart illustrates these two steps in creating a shared referral.</span></span>

![Stroom diagram met een gedeelde Referral met 2 referrals die zijn verbonden via de micro soft partner-API](../images/SharedReferral.png)

### <a name="create-your-referral"></a><span data-ttu-id="5b50f-198">Uw verwijzing maken</span><span class="sxs-lookup"><span data-stu-id="5b50f-198">Create your referral</span></span>

1. <span data-ttu-id="5b50f-199">Een verwijzing maken waarbij [ReferralType](referral-resources.md#referraltype) is ingesteld op gedeeld.</span><span class="sxs-lookup"><span data-stu-id="5b50f-199">Create a referral with [ReferralType](referral-resources.md#referraltype) set to shared.</span></span>
2. <span data-ttu-id="5b50f-200">Kopieer de **engagementId** van het retour antwoord.</span><span class="sxs-lookup"><span data-stu-id="5b50f-200">Copy the **engagementId** from the return response.</span></span>

<span data-ttu-id="5b50f-201">Voor beeld van [ReferralTarget](referral-resources.md#target) voor verwijzing</span><span class="sxs-lookup"><span data-stu-id="5b50f-201">[ReferralTarget](referral-resources.md#target) sample for referral</span></span>

```json
"target": [
        {
            "type": "SolutionProfile",
            "id": "SOL-ABC-DEF"
        }
    ]
```

### <a name="create-a-connected-referral"></a><span data-ttu-id="5b50f-202">Een verbonden Referral maken</span><span class="sxs-lookup"><span data-stu-id="5b50f-202">Create a connected referral</span></span>

1. <span data-ttu-id="5b50f-203">Maak een andere referral voor micro soft.</span><span class="sxs-lookup"><span data-stu-id="5b50f-203">Create another referral for Microsoft.</span></span>
2. <span data-ttu-id="5b50f-204">Neem de **enagementId** op uit uw referral, zodat deze aan elkaar zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="5b50f-204">Include the **enagementId** from your referral so they are tied together.</span></span>

<span data-ttu-id="5b50f-205">[ReferralTarget](referral-resources.md#target) -voor beeld voor micro soft Referral</span><span class="sxs-lookup"><span data-stu-id="5b50f-205">[ReferralTarget](referral-resources.md#target) sample for Microsoft referral</span></span>

```json
"target": [
        {
            "type": "BusinessProfileLocation",
            "id": "msft"
        }
    ]
```
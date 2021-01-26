---
title: Een lead of verkoop kans bijwerken (verouderd)
description: Hiermee kunt u de details van de lead of de opportuniteit bijwerken. Deze methode voor het bijwerken van een lead of verkoop kans is verouderd en we recommmend in plaats daarvan de aanroep van de PATCH te gebruiken.
ms.date: 09/30/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 9705db1c21dbec7099cfefebdc7bb23ec65e428c
ms.sourcegitcommit: 1e38faa376f317151aca15ae126015e290baa556
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/29/2020
ms.locfileid: "97770425"
---
# <a name="update-a-lead-or-opportunity-obsolete"></a><span data-ttu-id="031fc-104">Een lead of verkoop kans bijwerken (verouderd)</span><span class="sxs-lookup"><span data-stu-id="031fc-104">Update a lead or opportunity (Obsolete)</span></span>

<span data-ttu-id="031fc-105">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="031fc-105">Applies to:</span></span>

- <span data-ttu-id="031fc-106">Partner-API</span><span class="sxs-lookup"><span data-stu-id="031fc-106">Partner API</span></span>

<span data-ttu-id="031fc-107">In dit onderwerp wordt uitgelegd hoe u de lead-of verkoopkansgegevens, zoals de deal waarde, de geschatte Sluitings datum, of de verkoop stadia onder andere details bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="031fc-107">This topic explains how to update the lead or opportunity details like the deal value, estimated close date or manage the sales stages amongst other details.</span></span> 


> [!IMPORTANT]
<span data-ttu-id="031fc-108">Deze methode voor het bijwerken van een lead of verkoop kans is verouderd en we recommmend in plaats daarvan de aanroep van de [patch](patch-a-referral.md) te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="031fc-108">This method of updating a lead or opportunity is obsolete and we recommmend using the [PATCH](patch-a-referral.md) call instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="031fc-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="031fc-109">Prerequisites</span></span>

- <span data-ttu-id="031fc-110">Referenties zoals beschreven in [partner API-verificatie](api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="031fc-110">Credentials as described in [Partner API authentication](api-authentication.md).</span></span> <span data-ttu-id="031fc-111">Dit scenario ondersteunt verificatie met app + gebruikers referenties.</span><span class="sxs-lookup"><span data-stu-id="031fc-111">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="031fc-112">Deze API ondersteunt momenteel alleen gebruikers toegang waarbij partners een van de volgende rollen moeten hebben: globale beheerder, referentie beheerder of verwijzings gebruiker.</span><span class="sxs-lookup"><span data-stu-id="031fc-112">This API currently supports only user access where partners must be in one of the following roles: Global Admin, Referral Admin or Referral User.</span></span>

## <a name="rest-request"></a><span data-ttu-id="031fc-113">REST-aanvraag</span><span class="sxs-lookup"><span data-stu-id="031fc-113">REST Request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="031fc-114">Syntaxis van aanvraag</span><span class="sxs-lookup"><span data-stu-id="031fc-114">Request syntax</span></span>

| <span data-ttu-id="031fc-115">Methode</span><span class="sxs-lookup"><span data-stu-id="031fc-115">Method</span></span>  | <span data-ttu-id="031fc-116">Aanvraag-URI</span><span class="sxs-lookup"><span data-stu-id="031fc-116">Request URI</span></span>                                                       |
|---------|-------------------------------------------------------------------|
| <span data-ttu-id="031fc-117">**PUT**</span><span class="sxs-lookup"><span data-stu-id="031fc-117">**PUT**</span></span> | <https://api.partner.microsoft.com/v1.0/engagements/referrals/{Id}> |

### <a name="request-headers"></a><span data-ttu-id="031fc-118">Aanvraagheaders</span><span class="sxs-lookup"><span data-stu-id="031fc-118">Request headers</span></span>

- <span data-ttu-id="031fc-119">Zie de REST-headers van de [partner-API](headers.md)voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="031fc-119">For more information, see [Partner API REST headers](headers.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="031fc-120">Zorg ervoor dat u de header **if-match** instelt.</span><span class="sxs-lookup"><span data-stu-id="031fc-120">Be sure to set the **If-Match** header.</span></span>

### <a name="request-body"></a><span data-ttu-id="031fc-121">Aanvraagbody</span><span class="sxs-lookup"><span data-stu-id="031fc-121">Request body</span></span>

<span data-ttu-id="031fc-122">In deze tabel worden de [verwijzings](referral-resources.md) eigenschappen in de hoofd tekst van de aanvraag beschreven.</span><span class="sxs-lookup"><span data-stu-id="031fc-122">This table describes the [Referral](referral-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="031fc-123">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="031fc-123">Property</span></span>            | <span data-ttu-id="031fc-124">Type</span><span class="sxs-lookup"><span data-stu-id="031fc-124">Type</span></span>                                                                 | <span data-ttu-id="031fc-125">Description</span><span class="sxs-lookup"><span data-stu-id="031fc-125">Description</span></span>                                                                                                          |
|---------------------|----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="031fc-126">Id</span><span class="sxs-lookup"><span data-stu-id="031fc-126">Id</span></span>                  | <span data-ttu-id="031fc-127">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="031fc-127">string</span></span>                                                               | <span data-ttu-id="031fc-128">De ID voor deze verwijzing.</span><span class="sxs-lookup"><span data-stu-id="031fc-128">The ID for this Referral.</span></span>                                                                                            |
| <span data-ttu-id="031fc-129">EngagementId</span><span class="sxs-lookup"><span data-stu-id="031fc-129">EngagementId</span></span>        | <span data-ttu-id="031fc-130">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="031fc-130">string</span></span>                                                               | <span data-ttu-id="031fc-131">De EngagementID voor deze verwijzing.</span><span class="sxs-lookup"><span data-stu-id="031fc-131">The EngagementID for this Referral.</span></span> <span data-ttu-id="031fc-132">Meerdere verwijzingen kunnen worden gekoppeld aan één EngagementID</span><span class="sxs-lookup"><span data-stu-id="031fc-132">Multiple referrals can be associated to a single EngagementID</span></span>                    |
| <span data-ttu-id="031fc-133">Name</span><span class="sxs-lookup"><span data-stu-id="031fc-133">Name</span></span>                | <span data-ttu-id="031fc-134">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="031fc-134">string</span></span>                                                               | <span data-ttu-id="031fc-135">De naam van de verwijzing.</span><span class="sxs-lookup"><span data-stu-id="031fc-135">The name of the Referral.</span></span>                                                                                            |
| <span data-ttu-id="031fc-136">ExternalReferenceId</span><span class="sxs-lookup"><span data-stu-id="031fc-136">ExternalReferenceId</span></span> | <span data-ttu-id="031fc-137">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="031fc-137">string</span></span>                                                               | <span data-ttu-id="031fc-138">Een externe ID voor de verwijzing.</span><span class="sxs-lookup"><span data-stu-id="031fc-138">An external identifier for the referral.</span></span> <span data-ttu-id="031fc-139">Voor beeld: uw eigen Dynamics 365-ID voor potentiële klanten en verkoop kansen opslaan</span><span class="sxs-lookup"><span data-stu-id="031fc-139">Example: Store your own Dynamics 365 lead/opportunity ID</span></span>                    |
| <span data-ttu-id="031fc-140">CreatedDateTime</span><span class="sxs-lookup"><span data-stu-id="031fc-140">CreatedDateTime</span></span>     | <span data-ttu-id="031fc-141">teken reeks in UTC-datum tijd notatie</span><span class="sxs-lookup"><span data-stu-id="031fc-141">string in UTC date time format</span></span>                                       | <span data-ttu-id="031fc-142">De datum waarop de verwijzing is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="031fc-142">The date the referral was created.</span></span>                                                                                   |
| <span data-ttu-id="031fc-143">UpdatedDateTime</span><span class="sxs-lookup"><span data-stu-id="031fc-143">UpdatedDateTime</span></span>     | <span data-ttu-id="031fc-144">teken reeks in UTC-datum tijd notatie</span><span class="sxs-lookup"><span data-stu-id="031fc-144">string in UTC date time format</span></span>                                       | <span data-ttu-id="031fc-145">De datum waarop de verwijzing voor het laatst is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="031fc-145">The date the referral was last updated.</span></span>                                                                              |
| <span data-ttu-id="031fc-146">ExpirationDateTime</span><span class="sxs-lookup"><span data-stu-id="031fc-146">ExpirationDateTime</span></span>  | <span data-ttu-id="031fc-147">teken reeks in UTC-datum tijd notatie</span><span class="sxs-lookup"><span data-stu-id="031fc-147">string in UTC date time format</span></span>                                       | <span data-ttu-id="031fc-148">De datum waarop de verwijzing verloopt.</span><span class="sxs-lookup"><span data-stu-id="031fc-148">The date the referral will expire.</span></span>                                                                                   |
| <span data-ttu-id="031fc-149">Status</span><span class="sxs-lookup"><span data-stu-id="031fc-149">Status</span></span>              | [<span data-ttu-id="031fc-150">ReferralStatus</span><span class="sxs-lookup"><span data-stu-id="031fc-150">ReferralStatus</span></span>](referral-resources.md#referralstatus)               | <span data-ttu-id="031fc-151">Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven.</span><span class="sxs-lookup"><span data-stu-id="031fc-151">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral status.</span></span>          |
| <span data-ttu-id="031fc-152">Substatus</span><span class="sxs-lookup"><span data-stu-id="031fc-152">Substatus</span></span>           | [<span data-ttu-id="031fc-153">ReferralSubstatus</span><span class="sxs-lookup"><span data-stu-id="031fc-153">ReferralSubstatus</span></span>](referral-resources.md#referralsubstatus)         | <span data-ttu-id="031fc-154">Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de verwijzings substatus aangeven.</span><span class="sxs-lookup"><span data-stu-id="031fc-154">An [Enum](https://docs.microsoft.com/dotnet/api/system.enum) with values that indicate the referral sub status.</span></span>      |
| <span data-ttu-id="031fc-155">StatusReason</span><span class="sxs-lookup"><span data-stu-id="031fc-155">StatusReason</span></span>        | <span data-ttu-id="031fc-156">tekenreeks</span><span class="sxs-lookup"><span data-stu-id="031fc-156">string</span></span>                                                               | <span data-ttu-id="031fc-157">Een beschrijvende bericht over de status.</span><span class="sxs-lookup"><span data-stu-id="031fc-157">A descriptive message about the status.</span></span> <span data-ttu-id="031fc-158">Leg bijvoorbeeld uit waarom de Referral verloren is gegaan.</span><span class="sxs-lookup"><span data-stu-id="031fc-158">For example, explain why the referral was lost.</span></span>                              |
| <span data-ttu-id="031fc-159">ReferralType</span><span class="sxs-lookup"><span data-stu-id="031fc-159">ReferralType</span></span>        | [<span data-ttu-id="031fc-160">ReferralType</span><span class="sxs-lookup"><span data-stu-id="031fc-160">ReferralType</span></span>](referral-resources.md#referraltype)                   | <span data-ttu-id="031fc-161">Hiermee wordt het verwijzings type aangeduid.</span><span class="sxs-lookup"><span data-stu-id="031fc-161">Represents the referral type.</span></span>                                                                                        |
| <span data-ttu-id="031fc-162">Kwalificatie</span><span class="sxs-lookup"><span data-stu-id="031fc-162">Qualification</span></span>       | [<span data-ttu-id="031fc-163">ReferralQualification</span><span class="sxs-lookup"><span data-stu-id="031fc-163">ReferralQualification</span></span>](referral-resources.md#referralqualification) | <span data-ttu-id="031fc-164">Vertegenwoordigt de kwaliteit van de verwijzing.</span><span class="sxs-lookup"><span data-stu-id="031fc-164">Represents the quality of the referral.</span></span>                                                                              |
| <span data-ttu-id="031fc-165">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="031fc-165">CustomerProfile</span></span>     | [<span data-ttu-id="031fc-166">CustomerProfile</span><span class="sxs-lookup"><span data-stu-id="031fc-166">CustomerProfile</span></span>](referral-resources.md#customerprofile)             | <span data-ttu-id="031fc-167">Contact gegevens van de klant.</span><span class="sxs-lookup"><span data-stu-id="031fc-167">Customer contact information.</span></span>                                                                                        |
| <span data-ttu-id="031fc-168">Toestemming</span><span class="sxs-lookup"><span data-stu-id="031fc-168">Consent</span></span>             | [<span data-ttu-id="031fc-169">Toestemming</span><span class="sxs-lookup"><span data-stu-id="031fc-169">Consent</span></span>](referral-resources.md#consent)                             | <span data-ttu-id="031fc-170">Markering van toestemming voor het delen van gegevens met andere organisaties, zodat ze contact kunnen opnemen met de gebruikers.</span><span class="sxs-lookup"><span data-stu-id="031fc-170">Consent flags around sharing information with other organizations and allowing them to contact users.</span></span>                |
| <span data-ttu-id="031fc-171">Details</span><span class="sxs-lookup"><span data-stu-id="031fc-171">Details</span></span>             | [<span data-ttu-id="031fc-172">ReferralDetails</span><span class="sxs-lookup"><span data-stu-id="031fc-172">ReferralDetails</span></span>](referral-resources.md#referraldetails)             | <span data-ttu-id="031fc-173">Details van klant, notities, deal waarde, valuta afsluitings datum.</span><span class="sxs-lookup"><span data-stu-id="031fc-173">Customer details, notes, deal value, currency closing date.</span></span>                                                          |
| <span data-ttu-id="031fc-174">Team</span><span class="sxs-lookup"><span data-stu-id="031fc-174">Team</span></span>                | [<span data-ttu-id="031fc-175">Lid</span><span class="sxs-lookup"><span data-stu-id="031fc-175">Member</span></span>](referral-resources.md#member)                               | <span data-ttu-id="031fc-176">Vertegenwoordigt gebruikers in de organisaties die betrokken zijn bij de partner engagement.</span><span class="sxs-lookup"><span data-stu-id="031fc-176">Represents users in the organizations that are involved in the partner engagement.</span></span>                                   |
| <span data-ttu-id="031fc-177">InviteContext</span><span class="sxs-lookup"><span data-stu-id="031fc-177">InviteContext</span></span>       | [<span data-ttu-id="031fc-178">InviteContext</span><span class="sxs-lookup"><span data-stu-id="031fc-178">InviteContext</span></span>](referral-resources.md#invitecontext)                 | <span data-ttu-id="031fc-179">Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.</span><span class="sxs-lookup"><span data-stu-id="031fc-179">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span> |
| <span data-ttu-id="031fc-180">Doel</span><span class="sxs-lookup"><span data-stu-id="031fc-180">Target</span></span>         | [<span data-ttu-id="031fc-181">ReferralTarget</span><span class="sxs-lookup"><span data-stu-id="031fc-181">ReferralTarget</span></span>](referral-resources.md#target)        | <span data-ttu-id="031fc-182">Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.</span><span class="sxs-lookup"><span data-stu-id="031fc-182">Represents additional information a user can provide when inviting another organization into the partner engagement.</span></span>  |

### <a name="status-and-substatus-transition-states"></a><span data-ttu-id="031fc-183">Status en overgang van de substatus</span><span class="sxs-lookup"><span data-stu-id="031fc-183">Status and substatus transition states</span></span>

| <span data-ttu-id="031fc-184">Status</span><span class="sxs-lookup"><span data-stu-id="031fc-184">Status</span></span> | <span data-ttu-id="031fc-185">Status overgang toegestaan</span><span class="sxs-lookup"><span data-stu-id="031fc-185">Allowed Status Transition</span></span> | <span data-ttu-id="031fc-186">Toegestane substatus</span><span class="sxs-lookup"><span data-stu-id="031fc-186">Allowed Substatus</span></span>            |
|--------|---------------------------|------------------------------|
| <span data-ttu-id="031fc-187">Nieuw</span><span class="sxs-lookup"><span data-stu-id="031fc-187">New</span></span>    | <span data-ttu-id="031fc-188">Nieuw, actief, gesloten</span><span class="sxs-lookup"><span data-stu-id="031fc-188">New, Active, Closed</span></span>       | <span data-ttu-id="031fc-189">In behandeling, ontvangen</span><span class="sxs-lookup"><span data-stu-id="031fc-189">Pending, Received</span></span>            |
| <span data-ttu-id="031fc-190">Actief</span><span class="sxs-lookup"><span data-stu-id="031fc-190">Active</span></span> | <span data-ttu-id="031fc-191">Actief, gesloten</span><span class="sxs-lookup"><span data-stu-id="031fc-191">Active, Closed</span></span>            | <span data-ttu-id="031fc-192">Geaccepteerd</span><span class="sxs-lookup"><span data-stu-id="031fc-192">Accepted</span></span>                     |
| <span data-ttu-id="031fc-193">Gesloten</span><span class="sxs-lookup"><span data-stu-id="031fc-193">Closed</span></span> | <span data-ttu-id="031fc-194">Gesloten</span><span class="sxs-lookup"><span data-stu-id="031fc-194">Closed</span></span>                    | <span data-ttu-id="031fc-195">Gewonnen, verloren, afgewezen, verlopen</span><span class="sxs-lookup"><span data-stu-id="031fc-195">Won, Lost, Declined, Expired</span></span> |

### <a name="request-example"></a><span data-ttu-id="031fc-196">Voorbeeld van aanvraag</span><span class="sxs-lookup"><span data-stu-id="031fc-196">Request example</span></span>

```http
PUT https://api.partner.microsoft.com/v1.0/engagements/referrals/49d90c72-3326-4f61-aacc-2cb57970448c HTTP/1.1
Authorization: Bearer <token>
Host: api.partner.microsoft.com
Content-Type: application/json

 {
    "id": "49d90c72-3326-4f61-aacc-2cb57970448c",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:40:42.6178337Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    },
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",

}
```

> [!IMPORTANT]
> <span data-ttu-id="031fc-197">Verwijder het `"links": { }` object uit de put-resource.</span><span class="sxs-lookup"><span data-stu-id="031fc-197">Remove the `"links": { }` object from the PUT resource.</span></span>

## <a name="rest-response"></a><span data-ttu-id="031fc-198">REST-antwoord</span><span class="sxs-lookup"><span data-stu-id="031fc-198">REST Response</span></span>

<span data-ttu-id="031fc-199">Als dit lukt, retourneert deze methode de gevulde [verwijzings](referral-resources.md) bron in de antwoord tekst.</span><span class="sxs-lookup"><span data-stu-id="031fc-199">If successful, this method returns the populated [referral](referral-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="031fc-200">Geslaagde en fout codes</span><span class="sxs-lookup"><span data-stu-id="031fc-200">Response success and error codes</span></span>

<span data-ttu-id="031fc-201">Elk antwoord wordt geleverd met een HTTP-status code die aangeeft of de fout is opgetreden of mislukt en aanvullende informatie over fout opsporing.</span><span class="sxs-lookup"><span data-stu-id="031fc-201">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="031fc-202">Gebruik een hulp programma voor netwerk tracering om deze code, het fout type en aanvullende para meters te lezen.</span><span class="sxs-lookup"><span data-stu-id="031fc-202">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="031fc-203">Zie [fout codes](error-codes.md)voor de volledige lijst.</span><span class="sxs-lookup"><span data-stu-id="031fc-203">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="031fc-204">Voorbeeld van antwoord</span><span class="sxs-lookup"><span data-stu-id="031fc-204">Response example</span></span>

``` http
{
    "id": "4111fffc-f9ee-4d53-bba6-569135228642",
    "organizationId": "7d23e5ca-19dc-4eaa-aac8-5e6b559f0d1d",
    "organizationName": "Contoso Company",
    "engagementId": "37ef26aa-1d15-4533-9f93-a69bd33ab1e5",
    "createdDateTime": "2018-11-06T18:40:42.6178337Z",
    "updatedDateTime": "2018-11-06T18:43:38.9948636Z",
    "expirationDateTime": "2018-11-14T00:00:00Z",
    "status": "Closed",
    "substatus": "Won",
    "statusReason": "Customer engagement was a success!",
    "qualification": "SalesQualified",
    "type": "Independent",
    "target": [
        {
            "type": "BusinessProfileLocation",
            "id": "01e2abcd-52b0-4af3-a3ae-1fd1530b3563"
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
    "eTag": "\"2500ec5a-0000-0000-0000-5bf4967d0000\"",
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
---
title: Referral-connectors.
description: Synchroniseer partner referrals met Dynamics 365 CRM-leads met behulp van Microsoft Flow.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0a62023feb03114bb7ba1136b7700875f24c2e01
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770395"
---
# <a name="referral-connectors"></a><span data-ttu-id="66532-103">Referral-connectors</span><span class="sxs-lookup"><span data-stu-id="66532-103">Referral connectors</span></span>

<span data-ttu-id="66532-104">U kunt referentie connectors gebruiken voor het synchroniseren van partner verwijzingen met CRM-leads (Customer Relationship Management).</span><span class="sxs-lookup"><span data-stu-id="66532-104">You can use referral connectors to synchronize partner referrals with customer relationship management (CRM) leads.</span></span> <span data-ttu-id="66532-105">U kunt een referentie connector maken met [Microsoft flow](https://flow.microsoft.com) als het HTTPS-eind punt om partner verwijzingen te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="66532-105">You can create a referral connector using [Microsoft Flow](https://flow.microsoft.com) as the HTTPS endpoint to receive partner referrals.</span></span> <span data-ttu-id="66532-106">U kunt vervolgens de verwijzing die door de stroom is ontvangen, naar een CRM-systeem schrijven als lead.</span><span class="sxs-lookup"><span data-stu-id="66532-106">You can then write the referral received by the flow to a CRM system as a lead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66532-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="66532-107">Prerequisites</span></span>

* <span data-ttu-id="66532-108">Microsoft Flow-abonnement</span><span class="sxs-lookup"><span data-stu-id="66532-108">Microsoft Flow subscription</span></span>
  * <span data-ttu-id="66532-109">Account met beheerders toegang tot dit abonnement</span><span class="sxs-lookup"><span data-stu-id="66532-109">Account with administrator access to this subscription</span></span>
* <span data-ttu-id="66532-110">Azure Active Directory (Azure AD) toepassings-id, gebruikers-id, wacht woord en Tenant-ID (gebruikt voor toegang tot de partner-API).</span><span class="sxs-lookup"><span data-stu-id="66532-110">Azure Active Directory (Azure AD) application ID, user id, password and tenant ID (used to access the Partner API).</span></span> <span data-ttu-id="66532-111">Zie [partner verificatie](api-authentication.md)voor meer informatie over de installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="66532-111">For setup instructions, see [Partner authentication](api-authentication.md).</span></span>
* <span data-ttu-id="66532-112">[Azure function-app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) -abonnement.</span><span class="sxs-lookup"><span data-stu-id="66532-112">[Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) subscription.</span></span>
* <span data-ttu-id="66532-113">[Partner centrum webhook gebeurtenis](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) abonnement op [verwijzing gemaakt](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) en [bijgewerkte](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) gebeurtenissen door verwijzing.</span><span class="sxs-lookup"><span data-stu-id="66532-113">[Partner Center webhook event](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events) subscription to [Referral Created](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-created-event) and [Referral Updated](https://docs.microsoft.com/partner-center/develop/partner-center-webhook-events#referral-updated-event) events.</span></span>
* <span data-ttu-id="66532-114">[Micro soft Dynamics 365](https://dynamics.microsoft.com) -abonnement</span><span class="sxs-lookup"><span data-stu-id="66532-114">[Microsoft Dynamics 365](https://dynamics.microsoft.com) subscription</span></span>
  * <span data-ttu-id="66532-115">Module Sales ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="66532-115">Sales module enabled</span></span>
  * <span data-ttu-id="66532-116">Account met beheerders toegang tot dit abonnement</span><span class="sxs-lookup"><span data-stu-id="66532-116">Account with administrator access to this subscription</span></span>

## <a name="flow-overview"></a><span data-ttu-id="66532-117">Stroom overzicht</span><span class="sxs-lookup"><span data-stu-id="66532-117">Flow overview</span></span>

<span data-ttu-id="66532-118">Verwijzingen worden met de volgende stroom in het CRM geïmporteerd:</span><span class="sxs-lookup"><span data-stu-id="66532-118">Referrals are imported into the CRM using the following flow:</span></span>

1. <span data-ttu-id="66532-119">De partner stelt een webhook in voor het ontvangen van verwijzings meldingen.</span><span class="sxs-lookup"><span data-stu-id="66532-119">Partner sets up a webhook to receive referral notifications.</span></span>
2. <span data-ttu-id="66532-120">De partner registreert de webhook met het partner centrum.</span><span class="sxs-lookup"><span data-stu-id="66532-120">Partner registers the webhook with Partner Center.</span></span> <span data-ttu-id="66532-121">De partner is ook geabonneerd op webhook-gebeurtenissen voor wanneer verwijzingen worden gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="66532-121">The partner also subscribes to webhook events for when referrals are created or updated.</span></span>
3. <span data-ttu-id="66532-122">Referral client maakt of update een verwijzing.</span><span class="sxs-lookup"><span data-stu-id="66532-122">Referral client creates or updates a referral.</span></span>
4. <span data-ttu-id="66532-123">Partner Center-webhooksysteem controles voor de registratie van de partner en verzenden van een melding naar de webhook.</span><span class="sxs-lookup"><span data-stu-id="66532-123">Partner Center webhook system checks for the partner's registration and sends a notification to the webhook.</span></span>
5. <span data-ttu-id="66532-124">Webhook ontvangt de melding.</span><span class="sxs-lookup"><span data-stu-id="66532-124">Webhook receives the notification.</span></span>
6. <span data-ttu-id="66532-125">Flow-document in micro soft Flow gebruikt een token om een aanroep naar de Partner Center-Referral-API te maken.</span><span class="sxs-lookup"><span data-stu-id="66532-125">Flow document in Microsoft flow uses a token to make a call to the Partner Center referral API.</span></span>
7. <span data-ttu-id="66532-126">Het eind punt van de stroom haalt de verwijzing op.</span><span class="sxs-lookup"><span data-stu-id="66532-126">Flow endpoint gets the referral.</span></span>
8. <span data-ttu-id="66532-127">Met Flow-eind punt wordt de CRM-lead gemaakt.</span><span class="sxs-lookup"><span data-stu-id="66532-127">Flow endpoint creates the CRM lead.</span></span>

![Stroom diagram met de stappen in deze sectie voor het importeren van partner referrals in CRM.](../images/referralwebhook.png)

## <a name="flow-document-process"></a><span data-ttu-id="66532-129">Stroom document proces</span><span class="sxs-lookup"><span data-stu-id="66532-129">Flow document process</span></span>

<span data-ttu-id="66532-130">Het stroom document voor een verwijzings Connector synchroniseert een partner referentie met een CRM-lead van Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="66532-130">The flow document for a referral connector synchronizes a partner referral with a CRM lead from Dynamics 365.</span></span>

1. <span data-ttu-id="66532-131">Connector haalt een token op waarmee verbinding moet worden gemaakt `https://api.partner.microsoft.com/v1.0/engagements/referrals` .</span><span class="sxs-lookup"><span data-stu-id="66532-131">Connector gets a token to connect to `https://api.partner.microsoft.com/v1.0/engagements/referrals`.</span></span>
2. <span data-ttu-id="66532-132">De connector verkrijgt de Referral die de connector heeft geactiveerd met behulp van `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}` .</span><span class="sxs-lookup"><span data-stu-id="66532-132">Connector obtains referral that triggered the connector using `https://api.partner.microsoft.com/v1.0/engagements/referrals/{id}`.</span></span>
3. <span data-ttu-id="66532-133">Connector maakt verbinding met Dynamics 365.</span><span class="sxs-lookup"><span data-stu-id="66532-133">Connector connects to Dynamics 365.</span></span>
4. <span data-ttu-id="66532-134">Connector maakt een nieuwe lead of werkt een bestaande lead bij met de meest recente informatie over de verwijzing.</span><span class="sxs-lookup"><span data-stu-id="66532-134">Connector creates a new lead or updates an existing lead with the latest information on the referral.</span></span>
5. <span data-ttu-id="66532-135">Connector updates Referral met de meest recente updates van de CRM-lead.</span><span class="sxs-lookup"><span data-stu-id="66532-135">Connector updates referral with the latest updates from the CRM lead.</span></span>

![Stroom diagram met de stappen in deze sectie voor het proces van het stroom document.](../images/ReferralFlowSteps.png)

## <a name="sample-referral-connector"></a><span data-ttu-id="66532-137">Voor beeld van referentie connector</span><span class="sxs-lookup"><span data-stu-id="66532-137">Sample referral connector</span></span>

<span data-ttu-id="66532-138">De volgende voor *beeld-verwijzings connector* laat zien hoe u partner Center-verwijzingen naar CRM-leads in Dynamics 365 kunt synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="66532-138">The following *sample referral connector* shows how to synchronize Partner Center referrals to CRM leads in Dynamics 365.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66532-139">U kunt schrijven naar verschillende CRMs door de [flow-connectors](https://flow.microsoft.com/en-us/connectors/) in de voorbeeld code te vervangen.</span><span class="sxs-lookup"><span data-stu-id="66532-139">You can write to different CRMs by replacing the [flow connectors](https://flow.microsoft.com/en-us/connectors/) in the sample code.</span></span>

### <a name="import-flow-synchronization-package"></a><span data-ttu-id="66532-140">Stroom synchronisatie pakket importeren</span><span class="sxs-lookup"><span data-stu-id="66532-140">Import flow synchronization package</span></span>

<span data-ttu-id="66532-141">Down load en importeer het *voorbeeld code pakket* in Microsoft flow en maak verbinding met Dynamics 365:</span><span class="sxs-lookup"><span data-stu-id="66532-141">Download and import the *sample code package* into Microsoft Flow and connect to Dynamics 365:</span></span>

1. <span data-ttu-id="66532-142">Down load het [stroom synchronisatie pakket](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) van de [github opslag plaats](https://github.com/microsoft/Partner-Center-Referrals).</span><span class="sxs-lookup"><span data-stu-id="66532-142">Download the [flow synchronization package](https://github.com/microsoft/Partner-Center-Referrals/blob/master/flowconnectors/MicrosoftDynamicsCRM/PartnerReferralsToDynamicsCRMLead.zip?raw=true) from the [GitHub repo](https://github.com/microsoft/Partner-Center-Referrals).</span></span>
2. <span data-ttu-id="66532-143">Meld u aan bij [Microsoft flow](https://flow.microsoft.com) met de juiste referenties.</span><span class="sxs-lookup"><span data-stu-id="66532-143">Sign in to [Microsoft Flow](https://flow.microsoft.com) using the appropriate credentials.</span></span>
3. <span data-ttu-id="66532-144">Kies **mijn stromen** in het navigatie menu.</span><span class="sxs-lookup"><span data-stu-id="66532-144">Choose **My Flows** in the navigation menu.</span></span> <span data-ttu-id="66532-145">Kies vervolgens **importeren**.</span><span class="sxs-lookup"><span data-stu-id="66532-145">Then choose **Import**.</span></span>
4. <span data-ttu-id="66532-146">Selecteer op de pagina **pakket importeren** het stroom synchronisatie pakket dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="66532-146">On the **Import package** page, select the flow synchronization package that you downloaded.</span></span> <span data-ttu-id="66532-147">Kies vervolgens **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="66532-147">Then choose **Upload**.</span></span>

    ![Scherm pakket importeren voor pakket bestanden](../images/importPackage.png)

5. <span data-ttu-id="66532-149">Nadat het uploaden van het pakket is voltooid, gaat u naar het pakket dat u hebt geüpload in de inhoud van het **beoordelings pakket** .</span><span class="sxs-lookup"><span data-stu-id="66532-149">After the package upload is complete, find the package you uploaded in the **Review Package Content** .</span></span>

    ![Details van het scherm pakket importeren](../images/importPackageDetails.png)

6. <span data-ttu-id="66532-151">Kies de **actie** knop (potlood pictogram) voor het geüploade pakket.</span><span class="sxs-lookup"><span data-stu-id="66532-151">Choose the **Action** button (pencil icon) for your uploaded package.</span></span> <span data-ttu-id="66532-152">Hiermee opent u de Blade **import instellingen** .</span><span class="sxs-lookup"><span data-stu-id="66532-152">This opens the **Import setup** blade.</span></span>
7. <span data-ttu-id="66532-153">Kies uw **installatie** type.</span><span class="sxs-lookup"><span data-stu-id="66532-153">Choose your **Setup** type.</span></span>

    * <span data-ttu-id="66532-154">Als u een nieuwe stroom wilt maken, selecteert u **maken als nieuw** en voert u een nieuwe **resource naam** in.</span><span class="sxs-lookup"><span data-stu-id="66532-154">To create a new flow, select **Create as new**, and enter a new **Resource name**.</span></span>
    * <span data-ttu-id="66532-155">Als u een bestaande stroom met dezelfde naam wilt bijwerken, selecteert u **bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="66532-155">To update an existing flow with the same name, select **Update**.</span></span>

    ![Een nieuw pakket-scherm maken of bijwerken](../images/CreateNewConnection.png)

8. <span data-ttu-id="66532-157">Zoek op de pagina **pakket importeren** uw Dynamics 365-verbinding in het gedeelte **pakket inhoud beoordelen** onder **gerelateerde resources**.</span><span class="sxs-lookup"><span data-stu-id="66532-157">On the **Import package** page, find your Dynamics 365 connection in the **Review Package Content** section under **Related Resources**.</span></span>
9. <span data-ttu-id="66532-158">Kies de **actie** knop (potlood pictogram) voor uw Dynamics 365-verbinding.</span><span class="sxs-lookup"><span data-stu-id="66532-158">Choose the **Action** button (pencil icon) for your Dynamics 365 connection.</span></span> <span data-ttu-id="66532-159">Hiermee opent u de Blade **import instellingen** voor deze gerelateerde resource.</span><span class="sxs-lookup"><span data-stu-id="66532-159">This opens the **Import setup** blade for this related resource.</span></span>
10. <span data-ttu-id="66532-160">Kies **Nieuw maken** om een nieuwe Dynamics 365-verbinding te maken of selecteer een bestaande verbinding.</span><span class="sxs-lookup"><span data-stu-id="66532-160">Choose **Create new** to create a new Dynamics 365 connection, or select an existing connection.</span></span>
11. <span data-ttu-id="66532-161">Controleer of op de pagina **pakket importeren** nu het geselecteerde type stroom installatie en Dynamics 365-verbinding worden weer gegeven.</span><span class="sxs-lookup"><span data-stu-id="66532-161">Verify that the **Import package** page now shows your selected flow setup type and Dynamics 365 connection.</span></span> <span data-ttu-id="66532-162">Kies vervolgens **importeren**.</span><span class="sxs-lookup"><span data-stu-id="66532-162">Then choose **Import**.</span></span>

    ![Scherm pakket status importeren](../images/importStatus.png)

12. <span data-ttu-id="66532-164">Controleer of de stroom resource nu is gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="66532-164">Verify that your flow resource is now created or updated.</span></span>

### <a name="configure-flow-parameters"></a><span data-ttu-id="66532-165">Flow-para meters configureren</span><span class="sxs-lookup"><span data-stu-id="66532-165">Configure flow parameters</span></span>

<span data-ttu-id="66532-166">De para meters van uw stroom resource configureren:</span><span class="sxs-lookup"><span data-stu-id="66532-166">Configure the parameters of your flow resource:</span></span>

1. <span data-ttu-id="66532-167">In [Microsoft flow](https://flow.microsoft.com)kiest u **mijn stromen** in het navigatie menu.</span><span class="sxs-lookup"><span data-stu-id="66532-167">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="66532-168">Kies de stroom resource die u hebt gemaakt of bijgewerkt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="66532-168">Choose the flow resource you created or updated in the previous section.</span></span>
3. <span data-ttu-id="66532-169">Op de pagina stroom kiest u **stroom bewerken**.</span><span class="sxs-lookup"><span data-stu-id="66532-169">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="66532-170">Kies de ID-variabele van de **Aad-toepassing (client)** en voer de id van uw Azure AD-toepassing in.</span><span class="sxs-lookup"><span data-stu-id="66532-170">Choose the **AAD-Application (client) ID** variable and enter the ID of your Azure AD application.</span></span>
5. <span data-ttu-id="66532-171">Kies de variabele **UserID** en voer uw gebruikers-id in.</span><span class="sxs-lookup"><span data-stu-id="66532-171">Choose the **UserId** variable and enter your user ID.</span></span>
6. <span data-ttu-id="66532-172">Kies de variabele **userPassword** en voer uw gebruikers wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="66532-172">Choose the **UserPassword** variable and enter your user password.</span></span>
7. <span data-ttu-id="66532-173">Selecteer de ID-variabele voor **Aad-Directory (Tenant)** .</span><span class="sxs-lookup"><span data-stu-id="66532-173">Select the **AAD-Directory (tenant) ID** variable.</span></span> <span data-ttu-id="66532-174">Voer de Tenant-ID van uw Azure AD-toepassing in.</span><span class="sxs-lookup"><span data-stu-id="66532-174">Enter the tenant ID of your Azure AD application.</span></span>
8. <span data-ttu-id="66532-175">Kies **Opslaan** om uw stroom op te slaan.</span><span class="sxs-lookup"><span data-stu-id="66532-175">Choose **Save** to save your flow.</span></span>

    ![Scherm instellingen van stroom variabelen](../images/SetFlowVariables.png)

### <a name="authenticate-the-callback"></a><span data-ttu-id="66532-177">De call back verifiëren</span><span class="sxs-lookup"><span data-stu-id="66532-177">Authenticate the callback</span></span>

<span data-ttu-id="66532-178">De Terugbel gebeurtenis van het partner centrum verifiëren:</span><span class="sxs-lookup"><span data-stu-id="66532-178">Authenticate the callback event from the Partner Center:</span></span>

> [!TIP]
> <span data-ttu-id="66532-179">Zie de [voorbeeld functie-app code](#sample-function-app-code) in de volgende sectie voor een voor beeld.</span><span class="sxs-lookup"><span data-stu-id="66532-179">For an example, see the [sample function app code](#sample-function-app-code) in the following section.</span></span>

1. <span data-ttu-id="66532-180">[Maak een Azure-functie-app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) die [de call back gebeurtenis verifieert vanuit het partner centrum](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span><span class="sxs-lookup"><span data-stu-id="66532-180">[Create an Azure function app](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal) that [authenticates the callback event from the Partner Center](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#how-to-authenticate-the-callback).</span></span>

    1. <span data-ttu-id="66532-181">Controleer of de vereiste headers aanwezig zijn (**autorisatie**, **x-MS-Certificate-URL** en **x-MS-Signature-algoritme**).</span><span class="sxs-lookup"><span data-stu-id="66532-181">Verify that the required headers are present (**Authorization**, **x-ms-certificate-url**, and **x-ms-signature-algorithm**).</span></span>
    2. <span data-ttu-id="66532-182">Down load het certificaat dat wordt gebruikt om de inhoud te ondertekenen (**x-MS-Certificate-URL**).</span><span class="sxs-lookup"><span data-stu-id="66532-182">Download the certificate used to sign the content (**x-ms-certificate-url**).</span></span>
    3. <span data-ttu-id="66532-183">Controleer de certificaat keten.</span><span class="sxs-lookup"><span data-stu-id="66532-183">Verify the certificate chain.</span></span>
    4. <span data-ttu-id="66532-184">Controleer de **organisatie** van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="66532-184">Verify the **Organization** of the certificate.</span></span>
    5. <span data-ttu-id="66532-185">Lees de inhoud met UTF-8-code ring in een buffer.</span><span class="sxs-lookup"><span data-stu-id="66532-185">Read the content with UTF-8 encoding into a buffer.</span></span>
    6. <span data-ttu-id="66532-186">Maak een RSA crypto-provider.</span><span class="sxs-lookup"><span data-stu-id="66532-186">Create an RSA Crypto Provider.</span></span>
    7. <span data-ttu-id="66532-187">[Controleer of de hand tekening overeenkomt](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) met wat is ondertekend met het opgegeven hash-algoritme (bijvoorbeeld sha256).</span><span class="sxs-lookup"><span data-stu-id="66532-187">[Verify that the signature matches](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#example-for-signature-validation) what was signed with the specified hash algorithm (for example, SHA256).</span></span>
    8. <span data-ttu-id="66532-188">Als de verificatie slaagt, wordt er een **OK** -bericht weer gegeven.</span><span class="sxs-lookup"><span data-stu-id="66532-188">If the verification succeeds, an **OK** message is returned.</span></span>

2. <span data-ttu-id="66532-189">Noteer de gegenereerde call back-URI voor het HTTP-eind punt van uw functie-app.</span><span class="sxs-lookup"><span data-stu-id="66532-189">Note the generated callback URI for your function app's HTTP endpoint.</span></span> <span data-ttu-id="66532-190">Deze URI wordt weer gegeven wanneer u de functie-app maakt.</span><span class="sxs-lookup"><span data-stu-id="66532-190">This URI is displayed when you create your function app.</span></span> <span data-ttu-id="66532-191">U kunt deze URI ook vinden op de Azure-resource pagina van de functie-app.</span><span class="sxs-lookup"><span data-stu-id="66532-191">You can also find this URI on your function app's Azure resource page.</span></span>
3. <span data-ttu-id="66532-192">Bewerk in [Microsoft flow](https://flow.microsoft.com)de stroom ' partner referral to micro soft Dynamics CRM lead ' die u hebt geïmporteerd in het gedeelte *[import flow Synchronization package](#import-flow-synchronization-package)*.</span><span class="sxs-lookup"><span data-stu-id="66532-192">In [Microsoft Flow](https://flow.microsoft.com), edit the flow "Partner Referral to Microsoft Dynamics CRM Lead" that you imported in the section *[Import flow synchronization package](#import-flow-synchronization-package)*.</span></span>

    1. <span data-ttu-id="66532-193">Voeg de waarde van de URI van de functie-app toe aan de stap ' validatie van webhook-certificaat '.</span><span class="sxs-lookup"><span data-stu-id="66532-193">Add the value of the function app's URI to the "web hook certificate validation" step.</span></span>
    2. <span data-ttu-id="66532-194">Kopieer en plak de call back-URI van uw functie-app in het stroom document.</span><span class="sxs-lookup"><span data-stu-id="66532-194">Copy and paste your function app's callback URI into the flow document.</span></span>
    3. <span data-ttu-id="66532-195">Sla het stroom document op.</span><span class="sxs-lookup"><span data-stu-id="66532-195">Save your flow document.</span></span>

#### <a name="sample-function-app-code"></a><span data-ttu-id="66532-196">Code voor voorbeeld functie-app</span><span class="sxs-lookup"><span data-stu-id="66532-196">Sample function app code</span></span>

```csharp
using System.Net;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Primitives;
using Newtonsoft.Json;
using Microsoft.Azure.WebJobs;
using Microsoft.Extensions.Logging;
using System;
using System.IO;
using System.Linq;
using System.Net.Http;
using System.Security.Cryptography.X509Certificates;
using System.Text;
using System.Threading.Tasks;

public static async Task<IActionResult> Run(HttpRequest req, ILogger log)
{
    string requestBody = null;
    if (!string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-certificate-url")) && !string.IsNullOrWhiteSpace(GetFirstValueFromHeader(req, "x-ms-signature-algorithm")))
    {
        var certificateUrl = req?.Headers["x-ms-certificate-url"].First();
        try
        {
            string resultContent = null;
            using (var client = new HttpClient())
            {
                var result = await client.GetAsync(req.Headers["x-ms-certificate-url"].First());
                resultContent = await result.Content.ReadAsStringAsync();
                log.LogInformation(resultContent);
            }
            if (!string.IsNullOrEmpty(resultContent))
            {
                var certificate = new X509Certificate2(Encoding.UTF8.GetBytes(resultContent));
                var validationResult = certificate.Verify() && certificate.Issuer.Contains("O=Microsoft Corporation");
                if (validationResult)
                {
                    return new OkResult();
                }
                else
                {
                    return new BadRequestResult();
                }
            }
        }
        catch (Exception)
        {
            new BadRequestObjectResult("Certificate could not be retrieved, invalid caller to flow");
        }

        requestBody = await new StreamReader(req.Body).ReadToEndAsync();
        dynamic data = JsonConvert.DeserializeObject(requestBody);
    }
    else
    {
        new BadRequestObjectResult("Missing headers");
    }

    return new BadRequestObjectResult("Certificate validation failed");
}

private static string GetFirstValueFromHeader(HttpRequest request, string headerName)
{
    StringValues matchingHeaderValues;
    request.Headers.TryGetValue(headerName, out matchingHeaderValues);
    return matchingHeaderValues.Count != 0 ? matchingHeaderValues.First() : string.Empty;
}
```

### <a name="register-flow-with-partner-center"></a><span data-ttu-id="66532-197">Stroom registreren met partner centrum</span><span class="sxs-lookup"><span data-stu-id="66532-197">Register flow with Partner Center</span></span>

<span data-ttu-id="66532-198">Registreer uw stroom resource bij het partner centrum om de stroom te activeren en de gebeurtenissen van de webhook te ontvangen:</span><span class="sxs-lookup"><span data-stu-id="66532-198">Register your flow resource with the Partner Center to trigger the flow and receive webhook events:</span></span>

1. <span data-ttu-id="66532-199">In [Microsoft flow](https://flow.microsoft.com)kiest u **mijn stromen** in het navigatie menu.</span><span class="sxs-lookup"><span data-stu-id="66532-199">In [Microsoft Flow](https://flow.microsoft.com), choose **My Flows** in the navigation menu.</span></span>
2. <span data-ttu-id="66532-200">Kies de stroom die u hebt gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="66532-200">Choose the flow you created or updated.</span></span>
3. <span data-ttu-id="66532-201">Op de pagina stroom kiest u **stroom bewerken**.</span><span class="sxs-lookup"><span data-stu-id="66532-201">On the flow page, choose **Edit flow**.</span></span>
4. <span data-ttu-id="66532-202">Kopieer de **http post-URL** van de stroom en sla deze op.</span><span class="sxs-lookup"><span data-stu-id="66532-202">Copy and save the flow's **HTTP POST URL**.</span></span> <span data-ttu-id="66532-203">U moet deze URL gebruiken om de stroom te activeren.</span><span class="sxs-lookup"><span data-stu-id="66532-203">You will need to use this URL to trigger the flow.</span></span>
5. <span data-ttu-id="66532-204">[Meld u aan om webhook-gebeurtenissen te ontvangen](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) wanneer verwijzingen worden gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="66532-204">[Register to receive webhook events](https://docs.microsoft.com/partner-center/develop/partner-center-webhooks#register-to-receive-events) when referrals are created or updated.</span></span> <span data-ttu-id="66532-205">Gebruik de volgende hoofd indeling:</span><span class="sxs-lookup"><span data-stu-id="66532-205">Use the following body format:</span></span>

```json
{
    "WebhookUrl": "<<FlowUrl>>",
    "WebhookEvents": [
        "referral-created",
        "referral-updated"
    ],
    "signatureTokenToMsSignatureHeader": true
}
```

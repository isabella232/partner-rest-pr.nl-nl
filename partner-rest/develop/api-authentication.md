---
title: Verificatie van Partner-API
description: Configureer uw verificatie-instellingen om de partner-API met Azure AD te gebruiken voor verificatie.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: c5810678dccc2be1c3c084c901299961d6ba7820
ms.sourcegitcommit: 3c165938f544ff226cbe11ca21ed5aa00448d9b4
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/23/2020
ms.locfileid: "97770411"
---
# <a name="partner-api-authentication"></a><span data-ttu-id="f1d85-103">Verificatie van Partner-API</span><span class="sxs-lookup"><span data-stu-id="f1d85-103">Partner API authentication</span></span>

<span data-ttu-id="f1d85-104">Van toepassing op:</span><span class="sxs-lookup"><span data-stu-id="f1d85-104">Applies to:</span></span>

- <span data-ttu-id="f1d85-105">Partner-API</span><span class="sxs-lookup"><span data-stu-id="f1d85-105">Partner API</span></span>

<span data-ttu-id="f1d85-106">De partner-API maakt gebruik van Azure Active Directory (Azure AD) voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="f1d85-106">The Partner API utilizes Azure Active Directory (Azure AD) for authentication.</span></span> <span data-ttu-id="f1d85-107">Wanneer u met de partner-API communiceert, moet u een Azure AD-toepassing op de juiste wijze configureren en een toegangs token verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="f1d85-107">When you interact with the Partner API, you must correctly configure an Azure AD application and obtain an access token.</span></span> <span data-ttu-id="f1d85-108">U kunt toegangs tokens verkrijgen voor toegang tot [toepassingen en gebruikers](#application-and-user-access) of [alleen voor toegang tot een toepassing](#application-only-access).</span><span class="sxs-lookup"><span data-stu-id="f1d85-108">You can obtain access tokens for [application and user access](#application-and-user-access) or [application-only access](#application-only-access).</span></span>

## <a name="application-and-user-access"></a><span data-ttu-id="f1d85-109">Toegang voor toepassingen en gebruikers</span><span class="sxs-lookup"><span data-stu-id="f1d85-109">Application and user access</span></span>

<span data-ttu-id="f1d85-110">Deze methode wordt aanbevolen om toepassings- **en gebruikers toegang** tot de API in te stellen.</span><span class="sxs-lookup"><span data-stu-id="f1d85-110">This method is recommended to set up **application and user access** to the API.</span></span>

1. <span data-ttu-id="f1d85-111">Meld u aan bij de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f1d85-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f1d85-112">Kies de **Azure Active Directory** -service.</span><span class="sxs-lookup"><span data-stu-id="f1d85-112">Choose the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="f1d85-113">Kies **app-registraties** en kies vervolgens **nieuwe toepassing registreren**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-113">Choose **App registrations**, then choose **New application registration**.</span></span>
4. <span data-ttu-id="f1d85-114">Maak een nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1d85-114">Create your new application.</span></span> <span data-ttu-id="f1d85-115">Selecteer voor **toepassings type** **systeem eigen**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-115">For **Application type**, select **Native**.</span></span> <span data-ttu-id="f1d85-116">Geef een naam en URL op en selecteer vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-116">Provide a name and URL, then select **Create**.</span></span>
5. <span data-ttu-id="f1d85-117">Kies **API-machtigingen** voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1d85-117">Choose **API permissions** for the application.</span></span> <span data-ttu-id="f1d85-118">Kies op het scherm **API-machtigingen voor aanvragen** de optie **een machtiging toevoegen** en kies vervolgens **de api's die mijn organisatie gebruikt**</span><span class="sxs-lookup"><span data-stu-id="f1d85-118">On the **Request API permissions** screen, choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="f1d85-119">Zoek naar de *micro soft-partner* (*micro soft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="f1d85-119">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Scherm afbeelding van de weer gave van aanvraag-API-machtigingen met een zoek opdracht voor de micro soft partner-API](../images/SearchGatewayApi.png)

7. <span data-ttu-id="f1d85-121">Stel de **gedelegeerde machtigingen** in op het **partner centrum**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-121">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Scherm afbeelding van de configuratie van gedelegeerde machtigingen voor de micro soft partner-API](../images/SelectUserPermission.png)
    
8. <span data-ttu-id="f1d85-123">Zoek naar de *micro soft-partner* (*micro soft Partner Center*) API ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ).</span><span class="sxs-lookup"><span data-stu-id="f1d85-123">Search for the *Microsoft Partner* (*Microsoft Partner Center*) API (`fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd`).</span></span>

    ![Scherm afbeelding van de weer gave van aanvraag-API-machtigingen met een zoek opdracht voor de micro soft Partner Center-API](../images/SearchPCApi.png)
    
9. <span data-ttu-id="f1d85-125">Selecteer **micro soft-partner centrum** en controleer **user_impersonation**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-125">Select **Microsoft Partner Center** and check **user_impersonation**.</span></span>

10. <span data-ttu-id="f1d85-126">Stel de **gedelegeerde machtigingen** in op het **partner centrum**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-126">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Scherm afbeelding van de configuratie van gedelegeerde machtigingen voor de micro soft Partner Center-API](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a><span data-ttu-id="f1d85-128">Alleen-toepassing toegang</span><span class="sxs-lookup"><span data-stu-id="f1d85-128">Application-only access</span></span>

<span data-ttu-id="f1d85-129">Deze methode wordt aanbevolen voor de Api's die **alleen toegankelijk** zijn voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1d85-129">This method is recommended for **application-only access** setup to the APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f1d85-130">U moet de toepassings-ID, toepassings sleutel en map-ID van uw Azure AD-toepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="f1d85-130">You must provide the application ID, application key, and directory ID from your Azure AD application.</span></span>

1. <span data-ttu-id="f1d85-131">Meld u aan bij de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f1d85-131">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f1d85-132">Selecteer de service **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-132">Select the **Azure Active Directory** service.</span></span>
3. <span data-ttu-id="f1d85-133">Kies **app-registraties** en selecteer vervolgens **nieuwe toepassings registratie**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-133">Choose **App registrations**, then select **New application registration**.</span></span>
4. <span data-ttu-id="f1d85-134">Maak een nieuwe toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1d85-134">Create your new application.</span></span> <span data-ttu-id="f1d85-135">Kies voor **toepassings type** **Web-app/API**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-135">For **Application type**, choose **Web app/API**.</span></span> <span data-ttu-id="f1d85-136">Voer een toepassings **naam** en **URL** in.</span><span class="sxs-lookup"><span data-stu-id="f1d85-136">Enter a an application **name** and **URL**.</span></span> <span data-ttu-id="f1d85-137">Kies **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-137">Then choose **Create**.</span></span>
5. <span data-ttu-id="f1d85-138">Kies **API-machtigingen** voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1d85-138">Choose **API permissions** for the application.</span></span> <span data-ttu-id="f1d85-139">Kies **een machtiging toevoegen** en kies vervolgens **de api's die mijn organisatie gebruikt**</span><span class="sxs-lookup"><span data-stu-id="f1d85-139">Choose **Add a permission**, then choose **APIs my organization uses**</span></span>
6. <span data-ttu-id="f1d85-140">Zoek naar de *micro soft-partner* (*micro soft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).</span><span class="sxs-lookup"><span data-stu-id="f1d85-140">Search for the *Microsoft Partner* (*Microsoft Dev Center*) API (`4990cffe-04e8-4e8b-808a-1175604b879f`).</span></span>

    ![Scherm afbeelding van de weer gave van aanvraag-API-machtigingen met een zoek opdracht voor de micro soft partner-API](../images/SearchGatewayApi.png)

7. <span data-ttu-id="f1d85-142">Stel de **gedelegeerde machtigingen** in op het **partner centrum**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-142">Set the **Delegated Permissions** to **Partner Center**.</span></span>

    ![Scherm afbeelding van de configuratie van gedelegeerde machtigingen voor de micro soft partner-API](../images/SelectUserPermission.png)

8. <span data-ttu-id="f1d85-144">Voor de toepassing die u hebt geregistreerd, kiest u **Eigenschappen** en selecteert u vervolgens **de toepassings-id kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-144">For the application you registered, choose **Properties** and then select **copy the Application ID**.</span></span>
9. <span data-ttu-id="f1d85-145">Kies **instellingen** en kies vervolgens **certificaten & geheimen**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-145">Choose **Settings**, then choose **Certificates & Secrets**.</span></span> <span data-ttu-id="f1d85-146">Kies **Nieuw client geheim** en stel de **verloop tijd**  in op **nooit verlopen**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-146">Choose **New Client Secret** and set the **Expiration**  to **Never expires**.</span></span> <span data-ttu-id="f1d85-147">Kies vervolgens **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-147">Then choose **Save**.</span></span>
10. <span data-ttu-id="f1d85-148">Kies **de sleutel waarde kopiëren** in het menu **sleutels** .</span><span class="sxs-lookup"><span data-stu-id="f1d85-148">On the **Keys** menu, choose **Copy the key value**.</span></span> <span data-ttu-id="f1d85-149">Sla een kopie van deze waarde op.</span><span class="sxs-lookup"><span data-stu-id="f1d85-149">Save a copy of this value.</span></span>

> [!WARNING]
> <span data-ttu-id="f1d85-150">Zorg ervoor dat u een kopie van de sleutel waarde opslaat voor de sleutel die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f1d85-150">Be sure to save a copy of the key value for the key you created.</span></span> <span data-ttu-id="f1d85-151">U moet deze sleutel waarde later gebruiken om een token op te halen.</span><span class="sxs-lookup"><span data-stu-id="f1d85-151">You will need to use this key value later to obtain a token.</span></span>

## <a name="partner-consent"></a><span data-ttu-id="f1d85-152">Partner toestemming</span><span class="sxs-lookup"><span data-stu-id="f1d85-152">Partner consent</span></span>

<span data-ttu-id="f1d85-153">Selecteer in de Azure-beheer Portal **bedrijfs toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-153">In the Azure management portal, select **Enterprise applications**.</span></span> <span data-ttu-id="f1d85-154">Zoek naar de toepassing die u in de vorige sectie hebt gemaakt en selecteer de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f1d85-154">Search for the application you created in the previous section, and select that application.</span></span> <span data-ttu-id="f1d85-155">Selecteer **machtigingen** en selecteer **beheerder toestemming geven voor partner account**.</span><span class="sxs-lookup"><span data-stu-id="f1d85-155">Select **Permissions** , then select **Grant Admin Consent for Partner Account**.</span></span>

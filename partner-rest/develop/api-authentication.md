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
# <a name="partner-api-authentication"></a>Verificatie van Partner-API

Van toepassing op:

- Partner-API

De partner-API maakt gebruik van Azure Active Directory (Azure AD) voor verificatie. Wanneer u met de partner-API communiceert, moet u een Azure AD-toepassing op de juiste wijze configureren en een toegangs token verkrijgen. U kunt toegangs tokens verkrijgen voor toegang tot [toepassingen en gebruikers](#application-and-user-access) of [alleen voor toegang tot een toepassing](#application-only-access).

## <a name="application-and-user-access"></a>Toegang voor toepassingen en gebruikers

Deze methode wordt aanbevolen om toepassings- **en gebruikers toegang** tot de API in te stellen.

1. Meld u aan bij de [Azure-portal](https://portal.azure.com/).
2. Kies de **Azure Active Directory** -service.
3. Kies **app-registraties** en kies vervolgens **nieuwe toepassing registreren**.
4. Maak een nieuwe toepassing. Selecteer voor **toepassings type** **systeem eigen**. Geef een naam en URL op en selecteer vervolgens **maken**.
5. Kies **API-machtigingen** voor de toepassing. Kies op het scherm **API-machtigingen voor aanvragen** de optie **een machtiging toevoegen** en kies vervolgens **de api's die mijn organisatie gebruikt**
6. Zoek naar de *micro soft-partner* (*micro soft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Scherm afbeelding van de weer gave van aanvraag-API-machtigingen met een zoek opdracht voor de micro soft partner-API](../images/SearchGatewayApi.png)

7. Stel de **gedelegeerde machtigingen** in op het **partner centrum**.

    ![Scherm afbeelding van de configuratie van gedelegeerde machtigingen voor de micro soft partner-API](../images/SelectUserPermission.png)
    
8. Zoek naar de *micro soft-partner* (*micro soft Partner Center*) API ( `fa3d9a0c-3fb0-42cc-9193-47c7ecd2edbd` ).

    ![Scherm afbeelding van de weer gave van aanvraag-API-machtigingen met een zoek opdracht voor de micro soft Partner Center-API](../images/SearchPCApi.png)
    
9. Selecteer **micro soft-partner centrum** en controleer **user_impersonation**.

10. Stel de **gedelegeerde machtigingen** in op het **partner centrum**.

    ![Scherm afbeelding van de configuratie van gedelegeerde machtigingen voor de micro soft Partner Center-API](../images/SelectPCUserPermission.png)

## <a name="application-only-access"></a>Alleen-toepassing toegang

Deze methode wordt aanbevolen voor de Api's die **alleen toegankelijk** zijn voor de toepassing.

> [!IMPORTANT]
> U moet de toepassings-ID, toepassings sleutel en map-ID van uw Azure AD-toepassing opgeven.

1. Meld u aan bij de [Azure-portal](https://portal.azure.com/).
2. Selecteer de service **Azure Active Directory**.
3. Kies **app-registraties** en selecteer vervolgens **nieuwe toepassings registratie**.
4. Maak een nieuwe toepassing. Kies voor **toepassings type** **Web-app/API**. Voer een toepassings **naam** en **URL** in. Kies **Maken**.
5. Kies **API-machtigingen** voor de toepassing. Kies **een machtiging toevoegen** en kies vervolgens **de api's die mijn organisatie gebruikt**
6. Zoek naar de *micro soft-partner* (*micro soft dev Center*) API ( `4990cffe-04e8-4e8b-808a-1175604b879f` ).

    ![Scherm afbeelding van de weer gave van aanvraag-API-machtigingen met een zoek opdracht voor de micro soft partner-API](../images/SearchGatewayApi.png)

7. Stel de **gedelegeerde machtigingen** in op het **partner centrum**.

    ![Scherm afbeelding van de configuratie van gedelegeerde machtigingen voor de micro soft partner-API](../images/SelectUserPermission.png)

8. Voor de toepassing die u hebt geregistreerd, kiest u **Eigenschappen** en selecteert u vervolgens **de toepassings-id kopiëren**.
9. Kies **instellingen** en kies vervolgens **certificaten & geheimen**. Kies **Nieuw client geheim** en stel de **verloop tijd**  in op **nooit verlopen**. Kies vervolgens **Opslaan**.
10. Kies **de sleutel waarde kopiëren** in het menu **sleutels** . Sla een kopie van deze waarde op.

> [!WARNING]
> Zorg ervoor dat u een kopie van de sleutel waarde opslaat voor de sleutel die u hebt gemaakt. U moet deze sleutel waarde later gebruiken om een token op te halen.

## <a name="partner-consent"></a>Partner toestemming

Selecteer in de Azure-beheer Portal **bedrijfs toepassingen**. Zoek naar de toepassing die u in de vorige sectie hebt gemaakt en selecteer de toepassing. Selecteer **machtigingen** en selecteer **beheerder toestemming geven voor partner account**.

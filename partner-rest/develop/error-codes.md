---
title: Fout codes van de partner-API-REST
description: Partner REST-Api's retour neren een JSON-object met een status code over het slagen of mislukken van uw aanvraag.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 0829f48e5028b4a19e8a6f7b89fbb41d83a50cab
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770410"
---
# <a name="partner-api-rest-error-codes"></a>Fout codes van de partner-API-REST

Van toepassing op:

- Partner-API

Fouten in partner REST-Api's worden geretourneerd met behulp van standaard HTTP-status codes, evenals een JSON-fout object.

## <a name="http-status-codes"></a>HTTP-statuscode

In de volgende tabel worden de HTTP-status codes vermeld en beschreven die kunnen worden geretourneerd.

| Statuscode | Statusbericht                  | Description                                                                                                                            |
|:------------|:--------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------|
| 400         | Onjuiste aanvraag                     | Kan de aanvraag niet verwerken omdat deze onjuist is of onjuist is.                                                                       |
| 401         | Niet geautoriseerd                    | De vereiste authenticatie-informatie ontbreekt of is niet geldig voor de resource.                                                   |
| 403         | Verboden                       | De toegang tot de aangevraagde resource is geweigerd. De gebruiker heeft mogelijk niet voldoende machtigingen. **Belang rijk: als het beleid voor voorwaardelijke toegang wordt toegepast op een resource, `HTTP 403; Forbidden error=insufficent_claims` kan dit worden geretourneerd.** Zie voor meer informatie over Microsoft Graph en voorwaardelijke toegang [ontwikkelaars richtlijnen voor voorwaardelijke toegang voor Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-conditional-access-developer)  |
| 404         | Niet gevonden                       | De aangevraagde resource bestaat niet.                                                                                                  |
| 405         | Methode niet toegestaan              | De HTTP-methode in de aanvraag is niet toegestaan voor de resource.                                                                         |
| 406         | Niet geaccepteerd                  | Deze service biedt geen ondersteuning voor de indeling die is aangevraagd in de Accept-header.                                                                |
| 409         | Conflict                        | De huidige status is in conflict met wat de aanvraag verwacht. Het is bijvoorbeeld mogelijk dat de opgegeven bovenliggende map niet bestaat.                   |
| 410         | Missen                            | The requested resource is no longer available at the server.                                               |
| 411         | Lengte vereist                 | Er is een content-length-header vereist voor de aanvraag.                                                                                    |
| 412         | Voor waarde is mislukt             | Een voor waarde die in de aanvraag is opgegeven (zoals een if-match-header) komt niet overeen met de huidige status van de resource.                       |
| 413         | De aanvraag entiteit is te groot        | De aanvraag grootte overschrijdt de maximum limiet.                                                                                            |
| 415         | Niet-ondersteund media type          | Het inhouds type van de aanvraag is een indeling die niet wordt ondersteund door de service.                                                      |
| 416         | Het aangevraagde bereik is niet Satisfiable | Het opgegeven bereik van de byte is ongeldig of niet beschikbaar.                                                                                    |
| 422         | Niet-verwerkbare entiteit            | Kan de aanvraag niet verwerken omdat deze semantisch onjuist is.                                                                        |
| 423         | Vergrendeld                          | De resource die wordt geopend, is vergrendeld.                                                                                          |
| 429         | Te veel aanvragen               | Client toepassing is beperkt en moet niet proberen om de aanvraag te herhalen totdat er een hoeveelheid tijd is verstreken.                |
| 500         | Interne server fout           | Er is een interne server fout opgetreden tijdens het verwerken van de aanvraag.                                                                       |
| 501         | Niet geïmplementeerd                 | De aangevraagde functie is niet geïmplementeerd.                                                                                               |
| 503         | Service niet beschikbaar             | De service is tijdelijk niet beschikbaar voor onderhoud of is overbelast. U kunt de aanvraag herhalen na een vertraging, waarvan de lengte kan worden opgegeven in een Retry-After-header.|
| 504         | Time-out van Gateway                 | De server heeft tijdens het fungeren als proxy geen tijdige reactie ontvangen van de upstream-server die nodig is om toegang te krijgen bij een poging om de aanvraag te volt ooien. Kan optreden in combi natie met 503. |
| 507         | Onvoldoende opslag ruimte            | De maximale opslag limiet is bereikt.                                                                                            |
| 509         | Bandbreedte limiet overschreden        | Uw app is beperkt tot de maximale bandbreedte limiet is overschreden. Uw app kan de aanvraag opnieuw proberen nadat er meer tijd is verstreken. |

Het fout bericht is één JSON-object dat één eigenschap met de naam **fout** bevat. Dit object bevat alle details van de fout. U kunt de informatie die hier wordt geretourneerd, gebruiken in plaats van of naast de HTTP-status code. Hier volgt een voor beeld van een volledige JSON-fout tekst.

## <a name="error-resource-type"></a>Bron type voor fout

Het fout bericht is één JSON-object dat één eigenschap met de naam **fout** bevat. Dit object bevat alle details van de fout. U kunt de informatie die hier wordt geretourneerd, gebruiken in plaats van of naast de HTTP-status code. Hier volgt een voor beeld van een volledige JSON-fout tekst.

In het volgende tabel-en code voorbeeld wordt het schema van een fout bericht beschreven.

| Naam        | Type   | Description                                                                                    |
|-------------|--------|------------------------------------------------------------------------------------------------|
| code        | tekenreeks | Altijd geretourneerd. Hiermee wordt het soort fout aangegeven dat is opgetreden. Niet-null.                          |
| message | tekenreeks | Altijd geretourneerd. Hierin wordt de fout in details beschreven en vindt u meer informatie over fout opsporing. Niet-null en niet-leeg. De maximale lengte is 1024 tekens. |
| innerError        | object  | Optioneel. Aanvullend fout object dat mogelijk specifieker is dan de fout op het hoogste niveau.                                   |
| stemming      | tekenreeks | Het doel waarvan de fout afkomstig is.                                                      |

### <a name="code-property"></a>Code-eigenschap

De `code` eigenschap bevat een van de volgende mogelijke waarden. Uw apps moeten worden voor bereid om een van deze fouten te kunnen verwerken.

| Code                      | Description
|:--------------------------|:--------------
| **accessDenied**          | De aanroeper is niet gemachtigd om de actie uit te voeren.
| **generalException**      | Er is een niet nader omschreven fout opgetreden.
| **invalidRequest**        | De aanvraag is ongeldig of onjuist.
| **itemNotFound**          | De resource is niet gevonden.
|**preconditionFailed**     | Een voor waarde die in de aanvraag is opgegeven (zoals een if-match-header) komt niet overeen met de huidige status van de resource.
| **resourceModified**      | De resource die wordt bijgewerkt, is gewijzigd sinds de aanroeper het laatst heeft gelezen, meestal niet-overeenkomende eTag.
| **serviceNotAvailable**   | De service is niet beschikbaar. Probeer de aanvraag opnieuw uit te proberen na een vertraging. Er is mogelijk een Retry-After-header.
| **geverifieerde**       | De aanroeper is niet geverifieerd.

### <a name="message-property"></a>Bericht eigenschap

De `message` eigenschap op de hoofdmap bevat een fout bericht dat is bedoeld om te worden gelezen door de ontwikkelaar. Fout berichten zijn niet gelokaliseerd en mogen niet rechtstreeks worden weer gegeven voor de gebruiker. Bij het afhandelen van fouten moet uw code niet controleren op `message` waarden omdat ze op elk gewenst moment kunnen worden gewijzigd en bevatten ze vaak dynamische gegevens die specifiek zijn voor de mislukte aanvraag. U moet alleen code met fout codes die zijn geretourneerd in `code` Eigenschappen.

### <a name="innererror-object"></a>InnerError-object

Het `innererror` object kan recursief meer objecten bevatten `innererror` met aanvullende, meer specifieke fout codes. Bij het afhandelen van een fout moeten apps alle beschik bare fout codes door lopen en de meest gedetailleerde versie gebruiken die ze begrijpen.

Er zijn een aantal extra fouten die uw app kan tegen komen binnen de geneste `innererror` objecten. Apps zijn niet vereist voor het afhandelen van deze, maar kunnen als ze kiezen. De service kan nieuwe fout codes toevoegen of de oude retour nering op elk gewenst moment stoppen. het is dus belang rijk dat alle apps de [Basic error codes] kunnen verwerken.

```json
{
  "error": {
    "code": "unAuthorized",
    "message": "Caller is not authorized to access the resource.",
    "target": "referral",
    "innerError": {
      "code": "innerErrorCode",
      "message": "Unauthorized referral access"
    }
  }
}
```

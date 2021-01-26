---
title: Verwijzingsbronnen
description: Verwijzings resources vertegenwoordigen een verkoop lead direct van een klant, micro soft of een andere partner.
ms.date: 05/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 08438d208da57a4df40aeb609b14b6b6a6128d45
ms.sourcegitcommit: 0508b7302a3965fd5537b05c1f0397a1da014257
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 03/27/2020
ms.locfileid: "97770396"
---
# <a name="referral-resources"></a>Verwijzingsbronnen

Van toepassing op:

- Partnercentrum

Deze resources vertegenwoordigen een verkoop lead direct van een klant, micro soft of een andere partner.

## <a name="referral"></a>Doorverwezen

Vertegenwoordigt de verwijzing.

| Eigenschap              | Type                                              | Description                                                                                                       |
|-----------------------|---------------------------------------------------|-------------------------------------------------------------------------------------------------------------------|
| Id                    | tekenreeks                                            | De ID voor deze verwijzing.                                                                                         |
| EngagementId          | tekenreeks                                            | De EngagementID voor deze verwijzing. Meerdere verwijzingen kunnen worden gekoppeld aan één EngagementID                 |
| Name                  | tekenreeks                                            | De naam van de verwijzing.                 |
| ExternalReferenceId   | tekenreeks                                            | Een externe ID voor de verwijzing. Voor beeld: uw eigen Dynamics 365-ID voor potentiële klanten en verkoop kansen opslaan                    |
| CreatedDateTime       | teken reeks in UTC-datum tijd notatie                    | De datum waarop de verwijzing is gemaakt.                                                                                |
| UpdatedDateTime       | teken reeks in UTC-datum tijd notatie                    | De datum waarop de verwijzing voor het laatst is bijgewerkt.                                                                           |
| ExpirationDateTime    | teken reeks in UTC-datum tijd notatie                    | De datum waarop de verwijzing verloopt.                                                                                |
| Status                | [ReferralStatus](referral-resources.md#referralstatus)      | Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven. |
| Substatus          | [ReferralSubstatus](referral-resources.md#referralsubstatus)      | Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de verwijzings substatus aangeven. |
| StatusReason          | tekenreeks                                            | Een beschrijvende bericht over de status. Voor beeld: Waarom is de verwijzing verloren gegaan? |
| ReferralType          | [ReferralType](referral-resources.md#referraltype)          | Hiermee wordt het verwijzings type aangeduid.                                                                                     |
| Kwalificatie         | [ReferralQualification](referral-resources.md#referralqualification)| Vertegenwoordigt de kwaliteit van de verwijzing.                                                                           |
| CustomerProfile       | [CustomerProfile](referral-resources.md#customerprofile)    | Informatie over de klant.                                                                                     |
| Toestemming               | [Toestemming](referral-resources.md#consent)                    | Markering van toestemming voor het delen van gegevens met andere organisaties, zodat ze contact kunnen opnemen met de gebruikers.         |
| Details               | [ReferralDetails](referral-resources.md#referraldetails)    | Details van klant, notities, deal waarde, valuta afsluitings datum.                                                                |
| Team                  | [Lid](referral-resources.md#member)                      | Vertegenwoordigt gebruikers in de organisaties die betrokken zijn.                                |
| InviteContext         | [InviteContext](referral-resources.md#invitecontext)        | Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.  |
| ETag                  | tekenreeks                                            | ETags worden gebruikt en zijn vereist voor gelijktijdigheids controles bij het bijwerken van resources. |
| Doel         | [ReferralTarget](referral-resources.md#target)        | Vertegenwoordigt aanvullende informatie die een gebruiker kan bieden bij het uitnodigen van een andere organisatie in de partner engagement.  |

## <a name="referralstatus"></a>ReferralStatus

Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven.

| Waarde           | Beschrijving                                                                                |
|-----------------|---------------------------------------------------------------------------------------------|
| Geen            |                                                                                             |
| Nieuw             | Hiermee wordt een nieuwe verwijzing aangeduid.                                                                 |
| Actief          | Hiermee wordt een actieve verwijzing aangeduid.                                                             |
| Gesloten          | Vertegenwoordigt een gesloten verwijzing.                                                              |

## <a name="referralsubstatus"></a>ReferralSubstatus

Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven.

| Waarde           | Beschrijving                                                                                |
|-----------------|--------------------------------------------------------------------------------------------|
| Geen            |                                                                                            |
| In behandeling         | Hiermee wordt een nieuwe verwijzing aangeduid die in behandeling is.                                                 |
| Ontvangen        | Vertegenwoordigt een nieuwe verwijzing die is ontvangen.                   |
| Geaccepteerd        | Vertegenwoordigt een actieve verwijzing die is geaccepteerd.                                                    |
| Concurrenten             | Vertegenwoordigt een gesloten verwijzing die is gewonnen.                                            |
| Verdwenen            | Hiermee wordt een gesloten verwijzing aangeduid die verloren is gegaan.                                           |
| Geweigerd        | Vertegenwoordigt een gesloten verwijzing die is afgewezen.                                       |
| Verlopen         | Vertegenwoordigt een gesloten referentie die is verlopen.                                             |

### <a name="status--substatus-transition-states"></a>Status & overgangs toestanden voor substatus

| Status                | Status overgang toegestaan     | Toegestane substatus                |
|-----------------------|-------------------------------|---------------------------------------|
| Nieuw                   | Nieuw, actief, gesloten           | In behandeling, ontvangen                     |
| Actief                | Actief, gesloten                | Geaccepteerd                              |
| Gesloten                | Gesloten                        | Gewonnen, verloren, afgewezen, verlopen          |

## <a name="referraltype"></a>ReferralType

Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die het verwijzings type aangeven.

| Eigenschap              | Beschrijving                                                                     |
|-----------------------|---------------------------------------------------------------------------------|
| Gedeeld                | Hiermee wordt een verwijzing aangeduid waarin alle betrokken partijen samen werken om te sluiten.  |
| Onafhankelijk           | Hiermee wordt een verwijzing aangeduid waarin twee partijen samen werken om te sluiten.           |

## <a name="referralqualification"></a>ReferralQualification

Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die de referentie status aangeven.

| Waarde                | Beschrijving                                                                                 |
|----------------------|---------------------------------------------------------------------------------------------|
| Geen                 | Vertegenwoordigt een verwijzing waaraan geen kwaliteits meting is gekoppeld.                               |
| Direct               | Vertegenwoordigt een verwijzing die rechtstreeks door een klant is gemaakt.                         |
| MarketingQualified   | Vertegenwoordigt een verwijzing die is gegenereerd via micro soft marketing automation-systemen.   |
| SalesQualified       | Vertegenwoordigt een verwijzing van een micro soft-verkoop medewerker.                                         |

## <a name="customerprofile"></a>CustomerProfile

Bevat de contact gegevens van de klant.

| Eigenschap | Type                                                   | Beschrijving                                            |
|----------|--------------------------------------------------------|--------------------------------------------------------|
| Name     | tekenreeks                                                 | De naam van de organisatie van de klant.                        |
| Adres  | [Adres](referral-resources.md#address)                         | Het adres van de klant.                           |
| Grootte     | tekenreeks                                                 | Het aantal werk nemers in de organisatie van de klant. |
| Team     | [Lid](referral-resources.md#member)                           | De contact personen voor de organisatie van de klant.            |
| Id's      | [CustomerProfileType](referral-resources.md#customerprofiletype) | Een [matrix](https://docs.microsoft.com/dotnet/api/system.array) met waarden die de externe id's voor de klant aangeven.                        |

## <a name="customerprofiletype"></a>CustomerProfileType

Bevat de externe Id's voor de klant.

| Eigenschap | Type   | Description                                                                           |
|----------|--------|---------------------------------------------------------------------------------------|
| Duns     | tekenreeks | Het [Bradstreet-nummer van de inbel netwerk-&](https://www.dnb.com/duns-number.html) voor de klant. |
| Extern | tekenreeks | Een klant-ID die uniek is voor uw organisatie.                                            |

## <a name="address"></a>Adres

Een adres dat voor de klant moet worden gebruikt.

| Eigenschap     | Type   | Description                                                |
|--------------|--------|------------------------------------------------------------|
| AddressLine1 | tekenreeks | De eerste regel van het adres.                             |
| AddressLine2 | tekenreeks | De tweede regel van het adres. Deze eigenschap is optioneel. |
| Plaats         | tekenreeks | De plaats.                                                  |
| Staat        | tekenreeks | De status.                                                 |
| PostalCode   | tekenreeks | De post code                                |
| Land/regio      | tekenreeks | Het land/de regio in de [ISO-land nummer indeling](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.threeletterisoregionname?view=netframework-4.7.2).             |
| Regio       | tekenreeks | De regio.                                                |

## <a name="member"></a>Lid

Hierin worden de contact gegevens voor een specifieke persoon beschreven.

| Eigenschap    | Type   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | tekenreeks | De voor naam van de contact persoon.    |
| LastName    | tekenreeks | De achternaam van de contact persoon.     |
| PhoneNumber | tekenreeks | Het telefoon nummer van de contact persoon.  |
| E-mail       | tekenreeks | Het e-mail adres van de contact persoon. |
| ContactPreference       | [ContactPreference](referral-resources.md#contactpreference) | De voor keur van de contact persoon voor het ontvangen van e-mail meldingen. |

## <a name="contactpreference"></a>ContactPreference

Hierin worden de contact voorkeuren voor het ontvangen van e-mail meldingen beschreven.

| Eigenschap    | Type   | Description                  |
|-------------|--------|------------------------------|
| Landinstelling   | tekenreeks | De land instelling van de e-mail melding. [AllCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_AllCultures), [NeutralCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_NeutralCultures)en [SpecificCultures](https://docs.microsoft.com/dotnet/api/system.globalization.culturetypes?view=netframework-4.7.2#System_Globalization_CultureTypes_SpecificCultures) worden ondersteund  |
| DisableNotifications    | booleaans | De e-mail meldingen voor de gebruiker worden uitgeschakeld.     |

## <a name="consent"></a>Toestemming

Markering van toestemming voor het delen van gegevens met andere organisaties, zodat ze contact kunnen opnemen met de gebruikers.

| Eigenschap                                         | Type      | Description                                                                                |
|--------------------------------------------------|-----------|--------------------------------------------------------------------------------------------|
| ConsentToToShareInfoWithOthers                   | booleaans   | Geeft toestemming voor het delen van persoons gegevens (PII) met anderen.             |
| ConsentToContact                                 | booleaans   | Hiermee wordt toestemming voor contact personen van gebruikers aangegeven.  |

## <a name="invitecontext"></a>InviteContext

Aanvullende informatie die kan worden gedeeld wanneer een andere organisatie wordt uitgenodigd.

| Eigenschap              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notities                 | tekenreeks                                                     | Aanvullende opmerkingen voor de ontvangende organisatie.                |
| InvitedBy | [InvitedBy](referral-resources.md#invitedby)                                     | De organisatie-ID die de verwijzing heeft verzonden.                                   |

## <a name="invitedby"></a>InvitedBy

Aanvullende informatie die kan worden gedeeld wanneer een andere organisatie wordt uitgenodigd.

| Eigenschap              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| OrganizationId        | tekenreeks                                                     | De organisatie-ID die de verwijzing heeft verzonden.                |
| OrganizationName      | tekenreeks                                                     | De naam van de organisatie die de verwijzing heeft verzonden.                                   |

## <a name="referraldetails"></a>ReferralDetails

Hiermee worden de verwijzings Details aangeduid.

| Eigenschap              | Type                                                       | Description                                                                   |
|-----------------------|------------------------------------------------------------|-------------------------------------------------------------------------------|
| Notities                 | tekenreeks                                                     | Aanvullende opmerkingen voor de ontvangende organisatie.                |
| DealValue             | decimal                                                    | De waarde van de verwijzing.                                    |
| Valuta              | tekenreeks                                                    | Het [valuta symbool ISO 4217](https://docs.microsoft.com/dotnet/api/system.globalization.regioninfo.isocurrencysymbol?view=netframework-4.7.2)                                   |
| ClosingDateTime       | teken reeks in UTC-datum tijd notatie                         | De datum waarop de klant op zoek is te sluiten.                           |
| Vereisten          | [ReferralRequirements](referral-resources.md#referralrequirements)   | Industrie, producten, Service type en oplossingen waarop de klant is geïnteresseerd.|

## <a name="referralrequirements"></a>ReferralRequirements

Bevat de klant vereisten.

| Eigenschap        | Type                                                         | Description                                          |
|-----------------|--------------------------------------------------------------|------------------------------------------------------|
| Branches      | [Tag](referral-resources.md#tag)                                       | De sectoren waarin de klant is geïnteresseerd.        |
| Producten        | [Tag](referral-resources.md#tag)                                       | De producten waarop de klant is geïnteresseerd.          |
| Services        | [Tag](referral-resources.md#tag)                                       | De services waarop de klant is geïnteresseerd.          |
| Oplossingen       | [SolutionTag](referral-resources.md#solutiontag)                       | De oplossingen waarop de klant is geïnteresseerd.                             |

## <a name="solutiontag"></a>SolutionTag

Bevat de details van de oplossing.

| Eigenschap        | Type                                         | Description                                          |
|-----------------|----------------------------------------------|------------------------------------------------------|
| Id              | tekenreeks                                       | De ID van de oplossing.        |
| Name            | tekenreeks                                       | De naam van de oplossing.          |
| Solution type    | [Solution type](referral-resources.md#solutiontype)     | Het type oplossing.          |

## <a name="solutiontype"></a>Solution type

Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die het type oplossing aangeven.

| Eigenschap        | Beschrijving                                                     |
|-----------------|-----------------------------------------------------------------|
| Geen            |                                                                  |
| Categorie        |  Maakt gebruik van vooraf gedefinieerde namen van oplossingen.                            |
| Name            |  De mogelijkheid om te verwijzen naar oplossingen vanuit de micro soft Catalog. |

## <a name="target"></a>Doel

Hiermee wordt het referentie doel beschreven.

| Eigenschap                  | Type                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | tekenreeks                                                | De ID van het referentie doel. |
| Type                      | [ReferralTargetType](referral-resources.md#targettype) | Type verwijzings doel |

## <a name="targettype"></a>Target

Een [Enum](https://docs.microsoft.com/dotnet/api/system.enum) met waarden die het type oplossing aangeven.

| Eigenschap        | Beschrijving                                                     |
|-----------------|-----------------------------------------------------------------|
| Geen            |                                                                  |
| BusinessProfileLocation         |  Profiel locatie van het zakelijke profiel van de partner.                            |
| SolutionProfile            |  Het oplossings Profiel van de partner. |

## <a name="tag"></a>Tag

Hier wordt de tag beschreven.

| Eigenschap                  | Type                                                  | Description                                                   |
|---------------------------|-------------------------------------------------------|---------------------------------------------------------------|
| Id                        | tekenreeks                                                | De ID voor deze tag.                                          |

### <a name="products"></a>Producten

| Waarde        |
|-----------------|
|Azure|
|EnterpriseMobilityAndSecurity|
|Exchange|
|Ontwikkel aars|
|Dynamics365Business|
|Dynamics365Enterprise|
|DynamicsAX, GP, NAV, SL|
|Microsoft365|
|Office|
|Power BI|
|Project|
|SharePoint|
|SkypeForBusiness|
|Surface|
|SurfaceHub|
|SQL|
|Teams|
|Visio|
|Windows|
|Yammer|

### <a name="services"></a>Services

| Waarde        |
|-----------------|
|ConsultingAndProfessional|
|CustomSolution (ISV)|
|DeploymentOrMigration|
|Hardware|
|Integratie|
|IPServices (ISV)|
|LearningAndCertification|
|Licentieverlening|
|ManagedServices|
|ProjectServices|

### <a name="industries"></a>Branches

| Waarde        |
|-----------------|
|Land bouw, bosbouw & visserij|
|Communicatie & media|
|Onderwijs|
|Financiële diensten|
|Overheid|
|Gezondheidszorg|
|Horeca|
|Productie|
|Hulpprogram Ma's voor energie &|
|Open bare veiligheid en nationale veiligheid|
|Retail & consumenten goederen|
|Services|
|Reis & vervoer|
|Distributie van groothandels &|

### <a name="solutions"></a>Oplossingen

| Waarde        |
|-----------------|
|AdvancedAnalytics|
|ApplicationIntegration|
|ArtificialIntelligence|
|AzureSecurityOperationManagement|
    |AzureStack|
    |BackupDisasterRecovery|
    |BigData|
    |Blockchain|
    |Chatbot|
    |CloudDatabaseMigration|
    |CloudMigration|
    |CloudVoice|
    |CognitiveServices|
    |CompetitiveDatabaseMigration|
    |Containers|
    |DataWarehouse|
    |DatabaseonLinux|
    |DevelopmentandTest|
    |DevOps|
    |DigitalMedia|
    |Dynamics365forCustomerService|
    |Dynamics365forFieldService|
    |Dynamics365forFinanceOperations|
    |Dynamics365forRetail|
    |Dynamics365forSales|
    |Dynamics365forTalent|
    |DynamicsonAzure|
    |EnterpriseBusinessIntelligence|
    |Gaming|
    |HighPerformanceComputing|
    |HybridStorage|
    |IdentityandAccessManagement|
    |InformationManagement|
    |InternetofThings|
    |MachineLearning|
    |Microserviceapplications|
    |MobileApplications|
    |MySQLPostgresMigrationtoAzure|
    |Netwerken|
    |NoSQLMigration|
    |RedhatonAzure|
    |RegulatoryComplianceGDPR|
    |SAPonAzure|
    |ServerlessComputing|
    |SharepointonAzure|
    |SQLServerUpgrade|
    |ThreatProtection|
    |Webontwikkeling|

### <a name="customer-size"></a>Klant grootte

| Waarde        |
|-----------------|
|    1to50employees|
|    51to500employees|
|    Morethan500employees|
|    1to9employees|
|    10to50employees|
|    51to250employees|
|    251to1000employees|
|    1001to5000employees|
|    5001to10000employees|
|    10001to20000employees|
|    Morethan20000employees|

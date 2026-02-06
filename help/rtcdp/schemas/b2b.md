---
title: Schémas dans l’édition B2B de Real-time Customer Data Platform
description: Présentation du rôle des schémas de modèle de données d’expérience (XDM) dans Adobe Real-Time Customer Data Platform B2B edition.
feature: Get Started, Data Management, Schemas
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 24%

---

# Schémas dans l’édition B2B de Real-time Customer Data Platform

Adobe Real-Time Customer Data Platform B2B edition fournit plusieurs classes [modèle de données d’expérience (XDM)](../../xdm/schema/composition.md#class) standard qui capturent des détails sur les entités de données B2B essentielles, telles que les comptes, les opportunités, les campagnes, etc. En outre, Real-Time CDP B2B edition vous permet de définir des relations multiples-à-un entre ces schémas afin qu’ils puissent participer à des cas d’utilisation de segmentation avancée.

>[!IMPORTANT]
>
>Les schémas B2B peuvent être utilisés dans les applications Experience Platform (par exemple, dans [Customer Journey Analytics B2B edition](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-b2b/cja-b2b-edition)). <br/>Cependant, vous devez avoir accès à Real-Time CDP B2B edition pour que les schémas B2B (de profils dans) participent au [profil client en temps réel](../../profile/home.md).

Les classes standard suivantes sont fournies dans Real-Time CDP B2B edition :

* [Compte d’entreprise XDM](../../xdm/classes/b2b/business-account.md)
* [Relation avec la personne du compte d’entreprise XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [Membres de XDM Business Campaign](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [Relation avec la personne de XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list.md)
* [Membres de la liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list-members.md)

Pour comprendre comment les schémas s’intègrent à votre workflow B2B, reportez-vous au [tutoriel de bout en bout](../b2b-tutorial.md).

Pour savoir comment créer une relation multiple-à-un entre deux schémas, reportez-vous au tutoriel sur la [définition des relations de schéma B2B](../../xdm/tutorials/relationship-b2b.md).

Si vous utilisez une connexion source B2B, vous pouvez utiliser un outil pour générer automatiquement les schémas requis et les relations entre eux. Pour plus d’informations, consultez le guide sur les [espaces de noms B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) dans la documentation des sources.


Le tableau suivant contient des informations sur la configuration sous-jacente des schémas B2B.

>[!NOTE]
>
>Veuillez faire défiler la page vers la gauche/droite pour consulter le contenu complet du tableau.

| Nom du schéma | Classe de base | Groupes de champs | [!DNL Profile] dans le schéma | Identité principale | Espace de noms d’identité principal | identité Secondaire | Espace de noms d’identité Secondaire | Relation | Remarques |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Compte B2B | [ Compte professionnel XDM ](../../xdm/classes/b2b/business-account.md) | Détails du compte professionnel XDM | Activé | `accountKey.sourceKey` dans la classe de base | Compte B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Compte B2B | <ul><li>`accountParentKey.sourceKey` dans le groupe de champs Détails du compte professionnel XDM</li><li>Propriété de destination : `/accountKey/sourceKey`</li><li>Type : un à un</li><li>Schéma de référence : compte B2B</li><li>Espace De Noms : Compte B2B</li></ul> |  |
| Personne B2B | [XDM Individual Profile](../../xdm/classes/individual-profile.md) | <ul><li>Détails de professionnel XDM</li><li>Composants de professionnel XDM</li><li>IdentityMap</li><li>Détails relatifs au consentement et aux préférences</li></ul> | Activé | `b2b.personKey.sourceKey` dans le groupe de champs Détails professionnels XDM | Personne B2B | <ol><li>`extSourceSystemAudit.externalKey.sourceKey` du groupe de champs Détails professionnels XDM</li><li>`workEmail.address` du groupe de champs Détails professionnels XDM</ol></li> | <ol><li>Personne B2B</li><li>E-mail</li></ol> | <ul><li>`personComponents.sourceAccountKey.sourceKey` du groupe de champs Composants professionnels XDM .</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Compte B2B</li><li>Espace De Noms : Compte B2B</li><li>Propriété de destination : accountKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |  |
| Opportunité B2B | [Opportunité commerciale XDM](../../xdm/classes/b2b/business-opportunity.md) | Détails de l’opportunité commerciale XDM | Activé | `opportunityKey.sourceKey` dans la classe de base | Opportunité B2B | `extSourceSystemAudit.externalKey.sourceKey` dans la classe de base | Opportunité B2B | <ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Compte B2B</li><li>Espace De Noms : Compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation du schéma de référence : Opportunités</li></ul> |  |
| Relation de la personne avec l’opportunité B2B | [Relation de la personne avec l’opportunité commerciale XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md) | Aucune | Activé | `opportunityPersonKey.sourceKey` dans la classe de base | Relation de la personne avec l’opportunité B2B | | | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : b2b.personKey.sourceKey</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation du schéma de référence : Opportunités</li></ul>**Deuxième relation**<ul><li>`opportunityKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Opportunité B2B </li><li>Espace de noms : opportunité B2B </li><li>Propriété de destination : `opportunityKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : opportunité</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |  |
| Campagne B2B | [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md) | Détails de XDM Business Campaign | Activé | `campaignKey.sourceKey` dans la classe de base | Campagne B2B | | | | |
| Membre de la campagne B2B | [Membres de la campagne commerciale XDM](../../xdm/classes/b2b/business-campaign-members.md) | Détails du membre de la campagne commerciale XDM | Activé | `ccampaignMemberKey.sourceKey` dans la classe de base | Membre de la campagne B2B | | | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation du schéma de référence : Campagnes</li></ul>**Deuxième relation**<ul><li>`campaignKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Campagne B2B</li><li>Espace de noms : Campagne B2B</li><li>Propriété de destination : `campaignKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Campaign</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |  |
| Liste marketing B2B | [Liste marketing professionnelle XDM](../../xdm/classes/b2b/business-marketing-list.md) | Aucune | Activé | `marketingListKey.sourceKey` dans la classe de base | Liste marketing B2B | Aucune | Aucune | Aucune | La liste statique n’est pas synchronisée à partir de [!DNL Salesforce] et n’a donc pas d’identité secondaire. |
| Membre de la liste marketing B2B | [Membres de la liste marketing professionnelle XDM](../../xdm/classes/b2b/business-marketing-list-members.md) | Aucune | Activé | `marketingListMemberKey.sourceKey` dans la classe de base | Membre de la liste marketing B2B | Aucune | Aucune | **Première relation**<ul><li>`PersonKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personne</li><li>Nom de la relation à partir du schéma de référence : Listes marketing</li></ul>**Deuxième relation**<ul><li>`marketingListKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Liste Marketing B2B</li><li>Espace De Noms : Liste Marketing B2B</li><li>Propriété de destination : `marketingListKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Liste marketing</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> | Le membre de liste statique n’est pas synchronisé à partir de [!DNL Salesforce] et n’a donc pas d’identité secondaire. |
| Relation avec la personne du compte B2B | [Relation avec la personne du compte professionnel XDM](../../xdm/classes/b2b/business-account-person-relation.md) | Mappage d’identités | Activé | `accountPersonKey.sourceKey` dans la classe de base | Relation avec la personne du compte B2B | Aucune | Aucune | **Première relation**<ul><li>`personKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Personne B2B</li><li>Espace De Noms : Personne B2B</li><li>Propriété de destination : `b2b.personKey.SourceKey`</li><li>Nom de la relation à partir du schéma actuel : Personnes</li><li>Nom de la relation à partir du schéma de référence : Compte</li></ul>**Deuxième relation**<ul><li>`accountKey.sourceKey` dans la classe de base</li><li>Type : plusieurs à un</li><li>Schéma De Référence : Compte B2B</li><li>Espace De Noms : Compte B2B</li><li>Propriété de destination : `accountKey.sourceKey`</li><li>Nom de la relation à partir du schéma actuel : Compte</li><li>Nom de la relation du schéma de référence : Personnes</li></ul> |  |

{style="table-layout:auto"}


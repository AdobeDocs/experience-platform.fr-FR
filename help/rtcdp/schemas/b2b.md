---
title: Schémas dans l’édition B2B de Real-time Customer Data Platform
description: Présentation du rôle des schémas de modèle de données d’expérience (XDM) dans l’édition B2B de Real-time Customer Data Platform.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: 1a104d26b920082ee73178dd0ad7234ad43dec1a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 93%

---

# Schémas dans l’édition B2B de Real-time Customer Data Platform

L’édition B2B de Real-time Customer Data Platform offre plusieurs classes de [modèle de données d’expérience (XDM) standard](../../xdm/schema/composition.md#class) qui capturent des détails sur les entités de données B2B essentielles, telles que les comptes, les opportunités, les campagnes, etc. En outre, l’édition B2B de Real-time CDP permet de définir des relations multiples-à-un entre ces schémas afin qu’ils puissent participer à des cas d’utilisation de segmentation avancée.

>[!IMPORTANT]
>
>Pour pouvoir participer à [Real-time Customer Profile](../../profile/home.md), les schémas B2B doivent avoir accès à l’édition B2B de Real-time CDP.

Les classes standard suivantes sont fournies dans l’édition B2B de Real-time CDP :

* [Compte d’entreprise XDM](../../xdm/classes/b2b/business-account.md)
* [Relation avec la personne du compte d’entreprise XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [XDM Business Campaign](../../xdm/classes/b2b/business-campaign.md)
* [Membres de XDM Business Campaign](../../xdm/classes/b2b/business-campaign-members.md)
* [XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity.md)
* [Relation avec la personne de XDM Business Opportunity](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list.md)
* [Membres de la liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list-members.md)

Pour comprendre comment les schémas s’intègrent à votre workflow B2B, reportez-vous à la section [tutoriel de bout en bout](../b2b-tutorial.md).

Pour savoir comment créer une relation multiple-à-un entre deux schémas, reportez-vous au tutoriel sur la [définition des relations de schéma B2B](../../xdm/tutorials/relationship-b2b.md).

Si vous utilisez une connexion source B2B, vous pouvez utiliser un outil pour générer automatiquement les schémas requis et les relations entre eux. Pour plus d’informations, consultez le guide sur les [espaces de noms B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) dans la documentation des sources.

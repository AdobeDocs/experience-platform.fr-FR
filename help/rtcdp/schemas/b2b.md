---
title: Schémas de la plateforme de données clients en temps réel de l’édition B2B
description: Présentation du rôle des schémas de modèle de données d’expérience (XDM) dans l’édition B2B de la plateforme de données clients en temps réel.
source-git-commit: d83ad2870b6099d3c6359dcc7cd000ecad8a238f
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 3%

---

# Schémas de la plateforme de données clients en temps réel B2B (version bêta)

>[!IMPORTANT]
>
>La plateforme de données clients en temps réel de l’édition B2B est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

La plateforme de données clients en temps réel de l’édition B2B fournit plusieurs classes [Modèle de données d’expérience (XDM) standard](../../xdm/schema/composition.md#class) qui capturent des détails sur les entités de données B2B essentielles, telles que les comptes, les opportunités, les campagnes, etc. En outre, la plateforme CDP B2B en temps réel permet de définir des relations multiples-à-un entre ces schémas afin qu’ils puissent participer à des cas d’utilisation de segmentation avancée.

Les classes standard suivantes sont fournies dans l’édition B2B de la plateforme CDP en temps réel :

* [Compte d’entreprise XDM](../../xdm/classes/b2b/business-account.md)
* [Relation avec la personne du compte d’entreprise XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campagne commerciale XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membres de XDM Business Campaign](../../xdm/classes/b2b/business-campaign-members.md)
* [Opportunités commerciales XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relation de personne avec les opportunités commerciales XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list.md)
* [Membres de la liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list-members.md)

Pour savoir comment créer une relation multiple-à-un entre deux schémas, reportez-vous au tutoriel sur la [définition des relations de schémas B2B](../../xdm/tutorials/relationship-b2b.md).

Si vous utilisez une connexion source B2B, vous pouvez utiliser un outil pour générer automatiquement les schémas requis et les relations entre eux. Pour plus d’informations, consultez le guide sur les [espaces de noms B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) dans la documentation des sources.

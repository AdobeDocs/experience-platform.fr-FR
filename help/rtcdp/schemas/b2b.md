---
title: Schémas dans l’édition B2B de Real-time Customer Data Platform
description: Présentation du rôle des schémas de modèle de données d’expérience (XDM) dans l’édition B2B de Real-time Customer Data Platform.
exl-id: 3b18d377-108f-443f-86ae-dc7537cf9013
source-git-commit: f4ca1efe9c728f50008d7fbaa17aa009dfc18393
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 9%

---

# Schémas dans l’édition B2B de Real-time Customer Data Platform

L’édition B2B de Real-time Customer Data Platform offre plusieurs versions standard [Classes XDM (Experience Data Model)](../../xdm/schema/composition.md#class) qui capturent des détails sur les entités de données B2B essentielles, telles que les comptes, les opportunités, les campagnes, etc. En outre, la plateforme CDP B2B en temps réel permet de définir des relations multiples-à-un entre ces schémas afin qu’ils puissent participer à des cas d’utilisation de segmentation avancée.

Les classes standard suivantes sont fournies dans l’édition B2B de la plateforme CDP en temps réel :

* [Compte d’entreprise XDM](../../xdm/classes/b2b/business-account.md)
* [Relation avec la personne du compte d’entreprise XDM](../../xdm/classes/b2b/business-account-person-relation.md)
* [Campagne commerciale XDM](../../xdm/classes/b2b/business-campaign.md)
* [Membres de XDM Business Campaign](../../xdm/classes/b2b/business-campaign-members.md)
* [Opportunités commerciales XDM](../../xdm/classes/b2b/business-opportunity.md)
* [Relation de personne avec les opportunités commerciales XDM](../../xdm/classes/b2b/business-opportunity-person-relation.md)
* [Liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list.md)
* [Membres de la liste XDM Business Marketing](../../xdm/classes/b2b/business-marketing-list-members.md)

Pour savoir comment créer une relation multiple-à-un entre deux schémas, reportez-vous au tutoriel sur [définition des relations de schéma B2B](../../xdm/tutorials/relationship-b2b.md).

Si vous utilisez une connexion source B2B, vous pouvez utiliser un outil pour générer automatiquement les schémas requis et les relations entre eux. Consultez le guide sur la [Espaces de noms B2B](../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) pour plus d’informations, voir la documentation sur les sources .

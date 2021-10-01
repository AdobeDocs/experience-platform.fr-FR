---
keywords: extensions de balise;extension de balise;destinations de lancement extensions de balises Platform;extension de balises Platform;destinations de platform launch
title: Extensions de balises dans Adobe Experience Platform
description: Adobe Experience Platform offre la nouvelle génération de fonctionnalités de gestion des balises d’Adobe. Platform vous offre un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 272cf2906b44ccfeca041d9620ac0780e24ad1ae
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 35%

---

# Balisage des extensions dans Adobe Experience Platform

Adobe Experience Platform offre la nouvelle génération de fonctionnalités de gestion des balises d’Adobe. Platform vous offre un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Les balises sont proposées aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse.

Pour une présentation des balises, reportez-vous aux ressources ci-dessous :

- [Présentation des balises](../../../tags/home.md)
- [Guide de démarrage rapide](../../../tags/quick-start/quick-start.md)

## Comment trouver des extensions de balise dans l’interface de Platform {#how-to-find-extensions-in-interface}

Pour trouver les extensions dans l’interface de Platform, accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]** et sélectionnez **[!UICONTROL Extensions]** dans le filtre **[!UICONTROL Types]** .

![Filtre des extensions dans l’interface](../../assets/catalog/launch-extensions/filter.png)

## Fonctionnement des extensions de balise {#how-extensions-work}

Les extensions transfèrent les données d’événement brutes à plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](../personalization/gainsight.md) ou l’[extension de voix du client Confirmit](../voice/confirmit-digital-feedback.md).

**Les destinations d’** exportation de profils/segments dans Adobe Experience Platform capturent les données d’événement, les combinent à d’autres sources de données, appliquent la segmentation et exportent les segments et les profils qualifiés vers les destinations. Par exemple, la [destination de stockage dans le cloud Amazon S3](../cloud-storage/amazon-s3.md) ou la [destination publicitaire Google Display &amp; Video 360](../advertising/google-dv360.md).

![Comparaison des extensions de balise avec d’autres destinations](../../assets/common/launch-and-other-destinations.png)

## Avantages des extensions de balise {#extensions-benefits}

Les fonctionnalités de balise de Platform sont gratuites pour les clients Experience Cloud existants. Le système simplifie le déploiement des balises sur votre site web au moyen d’extensions conviviales que vous pouvez installer, configurer, mettre à jour et supprimer. Les balises n’ont qu’une faible empreinte sur votre site web et vous permettent de charger rapidement vos pages.

Bien que vous ne puissiez pas activer les segments pour baliser les extensions, vous pouvez configurer des règles afin de ne transférer les données d’événement que dans certaines situations. Cette puissante fonctionnalité vous permet de transférer les données d’événement uniquement dans certaines situations, plutôt que d’envoyer les données d’événement à chaque interaction. Pour plus d’informations, consultez les règles dans la [documentation sur les balises](../../../tags/ui/managing-resources/rules.md).

## Exemples d’utilisation des extensions de  {#extensions-use-cases}

Les extensions vous permettent de répondre à divers cas d’utilisation client. Voici quelques cas d’utilisation pour les extensions de 

- Vous pouvez envoyer des données de site web ou d’application native par le biais de l’extension pour Facebook Pixel. Facebook Pixel vous indique les parties du site web ou de l’application qu’un utilisateur a consultées, transfère ces informations à Facebook et vous permet ainsi de recibler cet utilisateur via Facebook.
- Vous pouvez transférer les données d’événement de vos sites web et de vos applications à Google Analytics afin d’analyser ces données et de prendre des décisions en fonction de celles-ci.
- Vous pouvez activer une application de messagerie instantanée côté client au bon moment en fonction de la manière dont vos utilisateurs interagissent avec vos pages, conformément aux règles que vous avez configurées.

## Catégories d’extensions {#extension-categories}

Les extensions peuvent appartenir aux catégories suivantes dans Platform :

- [Advertising](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plateforme de gestion des données](../data-management/overview.md)
- [Destinations de marketing par e-mail ](../email-marketing/overview.md)
- [Personnalisation](../personalization/overview.md)
- [Enquêtes](../survey/overview.md)
- [Retours des consommateurs](../voice/overview.md)

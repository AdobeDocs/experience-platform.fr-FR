---
keywords: launch extensions;launch extension;launch destinations; platform launch extensions;platform launch extension;platform launch destinations
title: Extensions d’Experience Platform Launch
seo-title: Extensions d’Experience Platform Launch
description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
seo-description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
translation-type: tm+mt
source-git-commit: 85e6a65e1407ca60e7b63681c045fadaaa24aef9
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 53%

---


# Extensions pour Adobe Experience Platform Launch {#overview.md}

Adobe Experience Platform Launch est la prochaine génération de fonctionnalités de gestion des balises issues de l’Adobe. Platform Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.  Platform Launch est une fonctionnalité gratuite intégrée à Adobe Experience Cloud.

Pour obtenir une présentation des fonctionnalités d’Experience Platform Launch, consultez les ressources ci-dessous :
- [Documentation Adobe Experience Platform Launch](https://docs.adobe.com/content/help/fr-FR/experience-cloud/user-guides/home.translate.html)
- Adobe Experience Platform Launch [quick start videos](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). Start with [Introduction to Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) and [Publishing process overview](https://helpx.adobe.com/fr/analytics/how-to/adobe-launch-publishing-process.html), then move on to the next concepts.

## How to find the Platform Launch extensions in the Real-time CDP interface {#how-to-find-extensions-in-interface}

To find the Platform Launch extensions in the Real-time CDP interface, browse to **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]** and select **[!UICONTROL Extensions]** in the **[!UICONTROL Types]** filter.

![Filtre des extensions dans l’interface](../../assets/catalog/launch-extensions/filter.png)

## Fonctionnement des extensions de lancement de plate-forme {#how-extensions-work}

Les extensions de lancement de plateforme transfèrent des données de événement brutes vers plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](../personalization/gainsight.md) ou l’[extension de voix du client Confirmit](../voice/confirmit-digital-feedback.md).

**Profil/segment Exportez** les destinations dans la plateforme de données clientes en temps réel pour capturer les données du événement, les combiner avec d’autres sources de données, appliquer la segmentation et exporter des segments et des profils qualifiés vers les destinations. Par exemple, la [destination de stockage dans le cloud Amazon S3](../cloud-storage/amazon-s3.md) ou la [destination publicitaire Google Display &amp; Video 360](../advertising/google-dv360.md).

![Comparaison entre les extensions d’Experience Platform Launch et d’autres destinations](../../assets/common/launch-and-other-destinations.png)

## Benefits of using Platform Launch extensions {#extensions-benefits}

Adobe Experience Platform Launch est gratuit pour les clients Experience Cloud existants. Le lancement de plate-forme simplifie le déploiement des balises sur votre site Web au moyen d’extensions conviviales que vous pouvez installer, configurer, mettre à jour et supprimer. Le lancement de plate-forme a une petite empreinte sur votre site Web et vous permet de charger rapidement vos pages.

>[!IMPORTANT]
>
>Bien que vous ne puissiez pas activer les segments dans les extensions de lancement de plate-forme, vous pouvez configurer des règles pour transférer uniquement les données de événement dans certaines situations. Retrouvez plus d’informations ci-dessous.

Vous pouvez créer des *règles* déterminant le moment où les données d’événement sont transférées aux extensions. Cette puissante fonctionnalité vous permet de transférer les données d’événement uniquement dans certaines situations, plutôt que d’envoyer les données d’événement à chaque interaction. For more information, read about rules in the [Adobe Experience Platform Launch documentation](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Example use cases for Platform Launch extensions {#extensions-use-cases}

Les extensions de lancement de plate-forme vous permettent de répondre à divers cas d’utilisation par les clients. Voici quelques exemples d’utilisation des extensions de lancement de plateforme :

- Vous pouvez envoyer des données de site web ou d’application native par le biais de l’extension pour Facebook Pixel. Facebook Pixel vous indique les parties du site web ou de l’application qu’un utilisateur a consultées, transfère ces informations à Facebook et vous permet ainsi de recibler cet utilisateur via Facebook.
- Vous pouvez transférer les données d’événement de vos sites web et de vos applications à Google Analytics afin d’analyser ces données et de prendre des décisions en fonction de celles-ci.
- Vous pouvez activer une application de messagerie instantanée côté client au bon moment en fonction de la manière dont vos utilisateurs interagissent avec vos pages, conformément aux règles que vous avez définies dans le lancement de la plateforme.

## Catégories d’extensions {#extension-categories}

Les extensions de lancement de plate-forme peuvent se trouver sous les catégories suivantes dans le CDP en temps réel :

- [Publicité](../advertising/overview.md)
- [Analyses](../analytics/overview.md)
- [Plateforme de gestion des données](../data-management/overview.md)
- [Destinations de marketing par e-mail](../email-marketing/overview.md)
- [Personnalisation](../personalization/overview.md)
- [Enquêtes](../survey/overview.md)
- [Retours des consommateurs](../voice/overview.md)

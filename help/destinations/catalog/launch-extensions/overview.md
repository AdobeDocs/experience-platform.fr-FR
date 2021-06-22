---
keywords: extensions de lancement;extension de lancement;destinations de lancement Extensions de platform launch;extension de platform launch;destinations de platform launch
title: Extension Adobe Experience Platform Launch
description: Adobe Experience Platform Launch représente la nouvelle génération des fonctionnalités de gestion des balises dʼAdobe. Platform Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
exl-id: 54fca635-0e37-460e-abb3-5da294d4e0cf
source-git-commit: 20a9103dd96116f3099bccc9eeb678be5ac2bb79
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 48%

---

# Extensions pour Adobe Experience Platform Launch

Adobe Experience Platform Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Platform Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.  Platform Launch est une fonctionnalité gratuite intégrée à Adobe Experience Cloud.

Pour obtenir une présentation des fonctionnalités d’Experience Platform Launch, consultez les ressources ci-dessous :

- [documentation d’Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/home.html?lang=fr)
- Adobe Experience Platform Launch [Vidéos de démarrage rapide](https://experienceleague.adobe.com/docs/launch/using/intro/get-started/videos.html?). Commencez par [Présentation d’Adobe Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) et [Présentation du processus de publication](https://helpx.adobe.com/fr/analytics/how-to/adobe-launch-publishing-process.html), puis passez aux concepts suivants.

## Comment trouver les extensions de Platform launch dans l’interface de Platform {#how-to-find-extensions-in-interface}

Pour rechercher les extensions de Platform launch dans l’interface de Platform, accédez à **[!UICONTROL Destinations]** > **[!UICONTROL Catalogue]** et sélectionnez **[!UICONTROL Extensions]** dans le filtre **[!UICONTROL Types]**.

![Filtre des extensions dans l’interface](../../assets/catalog/launch-extensions/filter.png)

## Fonctionnement des extensions de Platform launch {#how-extensions-work}

Les extensions Platform launch transfèrent les données d’événement brutes à plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](../personalization/gainsight.md) ou l’[extension de voix du client Confirmit](../voice/confirmit-digital-feedback.md).

**Les destinations d’** exportation de profils/segments dans Adobe Experience Platform capturent les données d’événement, les combinent à d’autres sources de données, appliquent la segmentation et exportent les segments et les profils qualifiés vers les destinations. Par exemple, la [destination de stockage dans le cloud Amazon S3](../cloud-storage/amazon-s3.md) ou la [destination publicitaire Google Display &amp; Video 360](../advertising/google-dv360.md).

![Comparaison entre les extensions d’Experience Platform Launch et d’autres destinations](../../assets/common/launch-and-other-destinations.png)

## Avantages de l’utilisation des extensions de Platform launch {#extensions-benefits}

Adobe Experience Platform Launch est gratuit pour les clients Experience Cloud existants. platform launch simplifie le déploiement des balises sur votre site web au moyen d’extensions simples d’utilisation que vous pouvez installer, configurer, mettre à jour et supprimer. platform launch a une petite empreinte sur votre site web et vous permet de charger rapidement vos pages.

>[!IMPORTANT]
>
>Bien que vous ne puissiez pas activer les segments vers des extensions de Platform launch, vous pouvez configurer des règles pour transférer les données d’événement uniquement dans certaines situations. Retrouvez plus d’informations ci-dessous.

Vous pouvez créer des *règles* déterminant le moment où les données d’événement sont transférées aux extensions. Cette puissante fonctionnalité vous permet de transférer les données d’événement uniquement dans certaines situations, plutôt que d’envoyer les données d’événement à chaque interaction. Pour plus d’informations, consultez les règles dans la [documentation Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## Exemples de cas d’utilisation pour les extensions de Platform launch {#extensions-use-cases}

Les extensions de platform launch vous permettent de répondre à divers cas pratiques client. Voici quelques exemples d’utilisation des extensions de Platform launch :

- Vous pouvez envoyer des données de site web ou d’application native par le biais de l’extension pour Facebook Pixel. Facebook Pixel vous indique les parties du site web ou de l’application qu’un utilisateur a consultées, transfère ces informations à Facebook et vous permet ainsi de recibler cet utilisateur via Facebook.
- Vous pouvez transférer les données d’événement de vos sites web et de vos applications à Google Analytics afin d’analyser ces données et de prendre des décisions en fonction de celles-ci.
- Vous pouvez activer une application de messagerie instantanée côté client au bon moment en fonction de la manière dont vos utilisateurs interagissent avec vos pages, conformément aux règles que vous avez configurées dans Platform launch.

## Catégories d’extensions {#extension-categories}

Les extensions de platform launch peuvent appartenir aux catégories suivantes dans Platform :

- [Publicité](../advertising/overview.md)
- [Analytics](../analytics/overview.md)
- [Plateforme de gestion des données](../data-management/overview.md)
- [Destinations de marketing par e-mail ](../email-marketing/overview.md)
- [Personnalisation](../personalization/overview.md)
- [Enquêtes](../survey/overview.md)
- [Retours des consommateurs](../voice/overview.md)

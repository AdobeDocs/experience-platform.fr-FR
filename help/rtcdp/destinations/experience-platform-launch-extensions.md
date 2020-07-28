---
title: Extensions d’Experience Platform Launch
seo-title: Extensions d’Experience Platform Launch
description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
seo-description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
translation-type: tm+mt
source-git-commit: 98c3356db178507e0a8d94b47030e9490e721e46
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 100%

---


# Extensions d’Experience Platform Launch {#experience-platform-launch-extensions}

Experience Platform Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Launch est une fonctionnalité proposée gratuitement dans le cadre d’Adobe Experience Cloud.

Pour obtenir une présentation des fonctionnalités d’Experience Platform Launch, consultez les ressources ci-dessous :
* [Documentation](https://docs.adobe.com/content/help/fr-FR/launch/using/overview.html) d’Experience Platform Launch
* [Vidéos de démarrage rapide](https://docs.adobe.com/content/help/fr-FR/launch/using/intro/get-started/videos.html) d’Experience Platform Launch. Commencez par la [Présentation d’Experience Platform Launch](https://www.youtube.com/embed/rwqqkG1SERU) et la [Présentation du processus de publication](https://helpx.adobe.com/fr/analytics/how-to/adobe-launch-publishing-process.html), puis passez aux concepts suivants.

## Accès aux extensions de Launch depuis l’interface de la plateforme de données clients en temps réel d’Adobe {#how-to-find-extensions-in-interface}

Pour accéder aux extensions de Launch depuis l’interface de la plateforme de données clients en temps réel d’Adobe, accédez à **[!UICONTROL Destinations > Catalogue]** et sélectionnez **[!UICONTROL Extensions]** dans le filtre **[!UICONTROL Types]**.

![Filtre des extensions dans l’interface](/help/rtcdp/destinations/assets/extensions-filter.png)

## Fonctionnement des extensions de Launch {#how-extensions-work}

Les extensions de Launch transfèrent les données d’événement brutes à plusieurs types de destinations. Considérez les extensions comme un type de destination **Transfert d’événement**. Il s’agit d’un type d’intégration aux plateformes de destination plus simple et qui ne transfère que les données d’événement brutes. Par exemple, l’[extension de personnalisation Gainsight](/help/rtcdp/destinations/gainsight-extension.md) ou l’[extension de voix du client Confirmit](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md).

Les destinations **Export de profil/segment** dans la plateforme de données clients en temps réel d’Adobe capturent les données d’événement, les combinent à d’autres sources de données, appliquent la segmentation et exportent les segments et les profils qualifiés vers les destinations. Par exemple, la [destination de stockage dans le cloud Amazon S3](/help/rtcdp/destinations/amazon-s3-destination.md) ou la [destination publicitaire Google Display &amp; Video 360](/help/rtcdp/destinations/google-dv360-destination.md).

![Comparaison entre les extensions d’Experience Platform Launch et d’autres destinations](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Avantages des extensions de Launch {#extensions-benefits}

Experience Platform Launch est gratuit pour les clients Experience Cloud. Launch simplifie le déploiement des balises sur votre site web grâce à des extensions simples d’utilisation que vous pouvez installer, configurer, mettre à jour et supprimer. L’empreinte de Launch sur votre site web est minime et le chargement des pages reste rapide.

>[!IMPORTANT]
>
>Bien que vous ne puissiez pas activer les segments transmis aux extensions de Launch, vous pouvez définir des règles afin de transférer les données d’événement uniquement dans certaines situations. Retrouvez plus d’informations ci-dessous.

Vous pouvez créer des *règles* déterminant le moment où les données d’événement sont transférées aux extensions. Cette puissante fonctionnalité vous permet de transférer les données d’événement uniquement dans certaines situations, plutôt que d’envoyer les données d’événement à chaque interaction. Pour plus d’informations, consultez les règles dans la [Documentation de Launch](https://docs.adobe.com/help/fr-FR/launch/using/reference/manage-resources/rules.html).

## Exemples d’utilisation des extensions de Launch {#extensions-use-cases}

Les extensions de Launch vous permettent de répondre à différents cas d’utilisation client. Voici quelques cas d’utilisation pour les extensions de Launch :

* Vous pouvez envoyer des données de site web ou d’application native par le biais de l’extension pour Facebook Pixel. Facebook Pixel vous indique les parties du site web ou de l’application qu’un utilisateur a consultées, transfère ces informations à Facebook et vous permet ainsi de recibler cet utilisateur via Facebook.
* Vous pouvez transférer les données d’événement de vos sites web et de vos applications à Google Analytics afin d’analyser ces données et de prendre des décisions en fonction de celles-ci.
* Vous pouvez activer une application de messagerie instantanée côté client au bon moment, en fonction de la manière dont vos utilisateurs interagissent avec vos pages, conformément aux règles définies dans Launch.


## Catégories d’extensions {#extension-categories}

Les extensions de Launch sont réparties dans les catégories suivantes dans la plateforme de données clients en temps réel d’Adobe :

* [Publicité](/help/rtcdp/destinations/advertising-destinations.md)
* [Analyses](/help/rtcdp/destinations/analytics-destinations.md)
* [Plateforme de gestion des données](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personnalisation](/help/rtcdp/destinations/personalization-destinations.md)
* [Enquêtes](/help/rtcdp/destinations/survey-destinations.md)
* [Retours des consommateurs](/help/rtcdp/destinations/voice-of-customer-destinations.md)

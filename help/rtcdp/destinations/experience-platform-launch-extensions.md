---
title: Extensions de lancement de plateforme d’expérience
seo-title: Extensions de lancement de plateforme d’expérience
description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
seo-description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
translation-type: tm+mt
source-git-commit: 98c3356db178507e0a8d94b47030e9490e721e46
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 22%

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Le lancement est proposé aux clients Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse.

Pour une présentation des fonctionnalités de lancement de plateforme d’expérience, voir les ressources ci-dessous :
* [Documentation sur le lancement de la plate-forme d’expérience](https://docs.adobe.com/content/help/fr-FR/launch/using/overview.html)
* Vidéos [de début](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html)rapide sur le lancement de la plate-forme d’expérience. Début présentant l’aperçu [du processus de lancement](https://www.youtube.com/embed/rwqqkG1SERU) et de [](https://helpx.adobe.com/fr/analytics/how-to/adobe-launch-publishing-process.html)publication de la plateforme d’expérience, puis passez aux concepts suivants.

## Comment trouver les extensions de lancement dans l’interface CDP d’Adobe en temps réel {#how-to-find-extensions-in-interface}

Pour rechercher les extensions de lancement dans l’interface CDP d’Adobe en temps réel, accédez à **[!UICONTROL Destinations > Catalogue]** et sélectionnez **[!UICONTROL Extensions]** dans le filtre **[!UICONTROL Types]** .

![Filtre Extensions dans l’interface](/help/rtcdp/destinations/assets/extensions-filter.png)

## Fonctionnement des extensions de lancement {#how-extensions-work}

Les extensions lancent des extensions pour transférer des données de événement brutes vers plusieurs types de destinations. Considérez les extensions comme un type de destination **Événement de transfert** . Il s’agit d’un type d’intégration plus simple avec les plateformes de destination, qui transfère uniquement les données de événement brutes. Par exemple, l’extension [de personnalisation de](/help/rtcdp/destinations/gainsight-extension.md) Gainsight ou la voix de [confirmation de l’extension](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Client.

**Profil/segment Exportez** les destinations dans la plateforme de données clientes Adobe en temps réel pour capturer les données du événement, les combiner avec d’autres sources de données, appliquer la segmentation et exporter des segments et des profils qualifiés vers des destinations. Par exemple, la destination [de l’enregistrement cloud](/help/rtcdp/destinations/amazon-s3-destination.md) Amazon S3 ou la destination [publicitaire](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Extensions de lancement de plateformes d’expérience par rapport à d’autres destinations](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Avantages de l’utilisation des extensions de lancement {#extensions-benefits}

Le lancement de la plate-forme d’expérience est gratuit pour les clients Experience Cloud existants. Le lancement simplifie le déploiement des balises sur votre site Web au moyen d’extensions conviviales que vous pouvez installer, configurer, mettre à jour et supprimer. Le lancement a une petite empreinte sur votre site Web et vous permet de continuer à charger rapidement vos pages.

>[!IMPORTANT]
>
>Bien que vous ne puissiez pas activer les segments pour lancer les extensions, vous pouvez configurer des règles pour ne transférer que les données de événement dans certaines situations. Lisez plus ci-dessous.

Vous pouvez créer *des règles* qui déterminent à quel moment transférer des données de événement vers des extensions. Cette puissante fonctionnalité vous permet de transférer des données de événement uniquement dans certaines situations, plutôt que d’envoyer des données de événement à chaque interaction. For more information, read about rules in the [Launch documentation](https://docs.adobe.com/help/fr-FR/launch/using/reference/manage-resources/rules.translate.html).

## Exemples de cas d’utilisation pour les extensions de lancement {#extensions-use-cases}

Les extensions de lancement vous permettent de répondre à divers cas d’utilisation par les clients. Voici quelques exemples d’utilisation des extensions de lancement :

* Vous pouvez envoyer des données de site Web ou d’application native à Facebook par le biais de l’extension de pixel Facebook. Pixel Facebook indique les parties de votre site ou application vers lesquelles un visiteur a navigué, transfère ces informations à Facebook et vous pouvez recibler votre visiteur via Facebook.
* Vous pouvez transférer des données de événement de vos sites Web et applications vers Google Analytics afin d’analyser ces données et de prendre des décisions en fonction de celles-ci.
* Vous pouvez activer une application de messagerie instantanée côté client au bon moment en fonction de la manière dont vos utilisateurs interagissent avec vos pages, conformément aux règles que vous avez définies dans Lancement.


## catégories d&#39;extension {#extension-categories}

Les extensions de lancement peuvent se trouver sous les catégories suivantes dans Adobe Real-time CDP :

* [Publicité](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Plateforme de Data Management](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinations de marketing par e-mail](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personnalisation ](/help/rtcdp/destinations/personalization-destinations.md)
* [Questionnaires](/help/rtcdp/destinations/survey-destinations.md)
* [Voix du client](/help/rtcdp/destinations/voice-of-customer-destinations.md)

---
title: Extensions de lancement de plateforme d’expérience
seo-title: Extensions de lancement de plateforme d’expérience
description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe.  Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
seo-description: Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe.  Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes.
translation-type: tm+mt
source-git-commit: 2a082dc46b50eba1a38eb9d6946e17f851b2fd3f

---


# Experience Platform Launch extensions {#experience-platform-launch-extensions}

Experience Platform Launch représente la nouvelle génération des fonctionnalités de gestion des balises d’Adobe. 
Launch offre aux clients un moyen simple de déployer et de gérer toutes les balises d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Le lancement est proposé aux clients d’Adobe Experience Cloud en tant que fonctionnalité à valeur ajoutée incluse.

Pour une présentation des fonctionnalités de lancement de plateforme d’expérience, voir les ressources ci-dessous :
* Experience Platform Launch [documentation](https://docs.adobe.com/content/help/fr-FR/launch/using/overview.html)
* Vidéo [de rapide du lancement de la plate-forme d’expérience](https://docs.adobe.com/content/help/en/launch/using/intro/get-started/videos.html).  avec [Présentation du processus de lancement](https://www.youtube.com/embed/rwqqkG1SERU) et de [publication de la plateforme d’expérience, présentation](https://helpx.adobe.com/fr/analytics/how-to/adobe-launch-publishing-process.html), puis passez aux concepts suivants.

## Comment trouver les extensions de lancement dans l’interface CDP en temps réel d’Adobe

Pour rechercher les extensions de lancement dans l’interface CDP en temps réel d’Adobe, accédez à **[!UICONTROL Destinations > Catalog]** et sélectionnez **[!UICONTROL Extensions]** dans le **[!UICONTROL Types]** filtre.

![Filtre Extensions dans l’interface](/help/rtcdp/destinations/assets/extensions-filter.png)

## Fonctionnement des extensions de lancement

Les extensions lancent des données de  brutes vers plusieurs types de destinations. Considérez les extensions comme un **type de destination Transfert** . Il s’agit d’un type d’intégration plus simple avec les plateformes de destination, qui ne transfère que les données  brutes. Par exemple, l’extension [de personnalisation de](/help/rtcdp/destinations/gainsight-extension.md) Gainsight ou la voix de [confirmation de l’extension](/help/rtcdp/destinations/confirmit-digital-feedback-extension.md)Client.

**/Segment d’exportation** des destinations dans la plateforme de données clientes Adobe en temps réel captent les données , les combinent à d’autres sources de données, appliquent la segmentation et exportent des segments et des qualifiés vers des destinations. Par exemple, le cloud [Amazon S3  la destination](/help/rtcdp/destinations/amazon-s3-destination.md) du ou la destination [publicitaire](/help/rtcdp/destinations/google-dv360-destination.md)Google Display &amp; Video 360.

![Expérience Platform Launch Extensions par rapport à d’autres destinations](/help/rtcdp/destinations/assets/launch-and-other-destinations.png)

## Avantages de l’utilisation des extensions de lancement

Le lancement de la plate-forme d’expérience est gratuit pour les clients Experience Cloud existants. Le lancement simplifie le déploiement des balises sur votre site Web au moyen d’extensions simples d’utilisation que vous pouvez installer, configurer, mettre à jour et supprimer. Le lancement a une petite empreinte sur votre site Web et vous permet de continuer à charger rapidement vos pages.

>[!IMPORTANT]
>
>Bien que vous ne puissiez pas activer les segments pour lancer les extensions, vous pouvez configurer des règles pour ne transférer  données que dans certaines situations. Lisez plus ci-dessous.

Vous pouvez créer *des règles* qui déterminent le moment où transférer des données  aux extensions. Cette puissante fonctionnalité vous permet de transférer des données  uniquement dans certaines situations, plutôt que d’envoyer des données de  à chaque interaction. For more information, read about rules in the [Launch documentation](https://docs.adobe.com/help/fr-FR/launch/using/reference/manage-resources/rules.translate.html).

## Exemples d’utilisation des extensions de lancement

Les extensions de lancement vous permettent de répondre à différents cas d’utilisation par les clients. Voici quelques exemples d’utilisation des extensions de lancement :

* Vous pouvez envoyer des données de site Web ou d’application native à Facebook par le biais de l’extension de pixel Facebook. Pixel Facebook indique les parties de votre site ou de l’application auxquelles un a accédé, transfère ces informations à Facebook et vous pouvez recibler votre via Facebook.
* Vous pouvez transférer  données de vos sites Web et de vos applications dans Google Analytics afin d’analyser ces données et de prendre des décisions en fonction de celles-ci.
* Vous pouvez activer une application de messagerie instantanée côté client au bon moment en fonction de la manière dont vos utilisateurs interagissent avec vos pages, conformément aux règles que vous avez définies dans Lancer.


##  d&#39;extension

Les extensions de lancement peuvent se trouver sous le  suivant dans le CDP en temps réel d’Adobe :

* [Publicité](/help/rtcdp/destinations/advertising-destinations.md)
* [Analytics](/help/rtcdp/destinations/analytics-destinations.md)
* [Plateforme](/help/rtcdp/destinations/dmp-destinations.md)
* [Destinations de marketing par e-mail ](/help/rtcdp/destinations/email-marketing-destinations.md)
* [Personnalisation  ](/help/rtcdp/destinations/personalization-destinations.md)
* [Des questionnaires (Survey)](/help/rtcdp/destinations/survey-destinations.md)
* [Voix du client](/help/rtcdp/destinations/voice-of-customer-destinations.md)

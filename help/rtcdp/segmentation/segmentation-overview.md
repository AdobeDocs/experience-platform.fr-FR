---
keywords: segmentation ; segmentation rtcdp ; segmentation des plateformes de données client en temps réel
title: Service de segmentation dans la plate-forme de données client en temps réel
seo-title: Service de segmentation dans la plate-forme de données client en temps réel
description: La plateforme CDP en temps réel repose sur Adobe Experience Platform et utilise de nombreux services et fonctionnalités d’Experience Platform. Grâce au service de segmentation, vous pouvez proposer un marketing sur mesure en divisant vos clients en groupes restreints aux caractéristiques similaires.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 35%

---


# [!DNL Segmentation Service] in [!DNL Real-time Customer Data Platform]

[!DNL Real-time Customer Data Platform] (CDP en temps réel) vous permet d’importer des données provenant de plusieurs sources afin de fournir à vos clients une expérience coordonnée et cohérente. Vous pouvez exécuter des campagnes de marketing personnalisées pertinentes à l&#39;aide de [!DNL Segmentation Service], partie de Adobe Experience Platform.

Le CDP en temps réel est construit sur Adobe Experience Platform et utilise de nombreux services et fonctionnalités [!DNL Experience Platform]. Grâce à [!DNL Segmentation Service], vous pouvez proposer un marketing sur mesure en divisant vos clients en groupes plus petits présentant des caractéristiques similaires.

## Segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat. En utilisant différents segments, vous pouvez vous concentrer sur les différentes audiences afin de fournir une expérience marketing plus personnalisée.

## [!DNL Segment Builder]

[!DNL Platform] vous permet de créer des segments et d’y accéder en toute facilité ainsi que d’utiliser différents blocs de création pour caractériser vos segments avec plus de précision. Pour plus d’informations sur l’utilisation du créateur de segments, consultez le [guide sur le créateur de segments](./segment-builder-guide.md).

## Customer AI

L’IA du client, incluse dans la plate-forme de données client en temps réel, vous permet de générer des prévisions client au niveau individuel avec des explications.

À l’aide de facteurs d’influence, Customer AI peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. En outre, vous pouvez tirer parti des prédictions et des informations d’API du client pour personnaliser les expériences client en fournissant les offres et les messages les plus appropriés. L’API du client peut vous aider à :

* Fournir des modèles de propension des clients à haute précision pour une segmentation et un ciblage renforcés.
* Comprendre les facteurs influents et la probabilité qui sous-tendent certains comportements des clients.
* Proposer des options personnalisables pour les cas d&#39;utilisation et les données uniques de votre société.
* Amélioration du Profil client en temps réel grâce à des scores de propension des clients tels que le déclenchement et la conversion.
* Amélioration des profils clients avec des facteurs influents pour les scores de propension.
* Création de segments de clients basés sur des facteurs influents et des scores de propension.

L’IA du client se trouve dans l’onglet **[!UICONTROL Services]** sous **[!UICONTROL Adobe services]**.

![Emplacement de l’API client](../assets/overview/rtcdp-customer-ai.png)

### Prise en main de Customer AI

Pour commencer à utiliser l’IA du client, vous devez suivre le [didacticiel de préparation des données](../../intelligent-services/data-preparation.md) et configurer le schéma d’entrée en fonction de votre cas d’utilisation. Ensuite, vous devrez [configurer une instance d’IA client](../../intelligent-services/customer-ai/user-guide/configure.md). Après avoir configuré une instance, un modèle est généré où vous pouvez [vue vos statistiques et scores](../../intelligent-services/customer-ai/user-guide/discover-insights.md). A l’aide des données générées à partir de votre modèle, vous pouvez créer des segments pour l’activation pilotée par les données.

Pour en savoir plus sur l’IA du client, début en visitant [Customer AI overview](../../intelligent-services/customer-ai/overview.md). En outre, la vidéo suivante montre comment l’IA du client enrichit les profils clients avec des propensions basées sur l’IA et renforce la segmentation et le ciblage des clients.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## Étapes suivantes

Après avoir lu cet aperçu, vous devez maintenant comprendre comment le CDP en temps réel utilise [!DNL Segmentation Service] pour améliorer la personnalisation et la personnalisation des campagnes marketing. Pour plus d&#39;informations sur [!DNL Segmentation Service], consultez la [documentation sur la segmentation](../../segmentation/home.md).

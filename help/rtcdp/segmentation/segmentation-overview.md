---
keywords: la segmentation; segmentation rtcdp;segmentation de la plateforme de données client en temps réel
title: Service de segmentation dans Real-time Customer Data Platform
description: La plateforme CDP en temps réel repose sur Adobe Experience Platform et utilise de nombreux services et fonctionnalités d’Experience Platform. Grâce au service de segmentation, vous pouvez proposer un marketing sur mesure en divisant vos clients en groupes restreints aux caractéristiques similaires.
exl-id: 140667c0-e288-40c4-8c45-c275e348b84a
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 35%

---

# [!DNL Segmentation Service] in [!DNL Real-time Customer Data Platform]

[!DNL Real-time Customer Data Platform] (CDP en temps réel) vous permet d’importer des données provenant de plusieurs sources afin de générer une expérience coordonnée et cohérente pour vos clients. La diffusion de campagnes marketing personnalisées pertinentes peut être réalisée à l’aide du [!DNL Segmentation Service], fait partie de Adobe Experience Platform.

La plateforme CDP en temps réel repose sur Adobe Experience Platform et utilise de nombreuses fonctionnalités de la [!DNL Experience Platform] services et fonctionnalités. En utilisant la variable [!DNL Segmentation Service], vous pouvez proposer un marketing sur mesure en divisant vos clients en groupes plus petits avec des caractéristiques similaires.

## Segmentation

La segmentation est le processus consistant à définir des attributs ou des comportements spécifiques partagés par un sous-ensemble de profils de votre magasin de profils afin d’identifier un groupe de clients potentiels dans votre base. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat. En utilisant différents segments, vous pouvez vous concentrer sur les différentes audiences afin de fournir une expérience marketing plus personnalisée.

## [!DNL Segment Builder]

[!DNL Platform] vous permet de créer des segments et d’y accéder en toute facilité ainsi que d’utiliser différents blocs de création pour caractériser vos segments avec plus de précision. Pour plus d’informations sur l’utilisation du créateur de segments, consultez le [guide sur le créateur de segments](./segment-builder-guide.md).

## IA dédiée aux clients

Customer AI, inclus dans Real-time Customer Data Platform, vous permet de générer des prédictions client au niveau individuel avec des explications.

À l’aide de facteurs d’influence, Customer AI peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. De plus, vous pouvez tirer parti des prédictions et des informations de Customer AI pour personnaliser les expériences client en diffusant les offres et messages les plus appropriés. Customer AI peut vous aider à :

* Fournir des modèles de propension des clients à haute précision pour une segmentation et un ciblage plus forts.
* Comprendre les facteurs d’influence et la probabilité derrière certains comportements des clients.
* Offrir des options personnalisables pour les cas d’utilisation et les données uniques de votre entreprise.
* Amélioration de Real-time Customer Profile avec des scores de propension des clients tels que l’attrition et la conversion.
* Amélioration des profils client avec des facteurs d’influence pour les scores de propension.
* Création de segments de clients en fonction de facteurs d’influence et de scores de propension.

Customer AI se trouve dans la variable **[!UICONTROL Services]** sous **[!UICONTROL Services Adobe]**.

![Emplacement de Customer AI](../assets/overview/rtcdp-customer-ai.png)

### Prise en main de Customer AI

Pour commencer à utiliser Customer AI, vous devez suivre le [tutoriel sur la préparation des données](../../intelligent-services/data-preparation.md) et configurez le schéma d’entrée en fonction de votre cas d’utilisation. Ensuite, vous devrez [configuration d’une instance Customer AI](../../intelligent-services/customer-ai/user-guide/configure.md). Après la configuration d’une instance, un modèle est généré, où vous pouvez [afficher vos insights et scores ;](../../intelligent-services/customer-ai/user-guide/discover-insights.md). En utilisant les données générées à partir de votre modèle, vous pouvez créer des segments pour l’activation pilotée par les données.

Pour en savoir plus sur Customer AI, commencez par consulter le [Présentation de Customer AI](../../intelligent-services/customer-ai/overview.md). En outre, la vidéo suivante montre comment Customer AI enrichit les profils clients avec des propensions basées sur l’IA et renforce la segmentation et le ciblage des clients.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## Étapes suivantes

Après avoir lu cette présentation, vous devez maintenant comprendre comment la plateforme CDP en temps réel utilise [!DNL Segmentation Service] pour améliorer la personnalisation et la personnalisation des campagnes marketing. Pour plus d’informations sur la variable [!DNL Segmentation Service], veuillez lire la [Documentation sur la segmentation](../../segmentation/home.md).

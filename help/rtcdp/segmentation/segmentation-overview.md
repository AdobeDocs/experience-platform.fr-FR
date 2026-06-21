---
keywords: segmentation;segmentation rtcdp;segmentation de real time customer data platform
title: Service de segmentation de Real-Time Customer Data Platform
description: Adobe Real-Time Customer Data Platform repose sur Adobe Experience Platform et utilise de nombreux services et fonctionnalités d’Experience Platform. Grâce au service de segmentation, vous pouvez proposer un marketing sur mesure en divisant vos clients en groupes restreints aux caractéristiques similaires.
feature: Get Started, Audiences, Segments
exl-id: 140667c0-e288-40c4-8c45-c275e348b84a
TQID: https://experienceleague.adobe.com/TdddFgUATtF3Y5gNzkxCbWdDa0ikPjrBlLCJAApmJkk
product_v2: id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2: id: a3f1e846-82a6-4574-9832-7d46ef69f306id: ba929a52-9339-4154-9487-317dc875a3c7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d00e9f03-e50b-4162-b143-0c0817c937c2id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eb30f47f-d87a-400f-8f78-63ce7979ff56id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 553
ht-degree: 73%

---

# [!DNL Segmentation Service] dans [!DNL Real-Time Customer Data Platform]

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) permet de rassembler des données issues de plusieurs sources afin de générer une expérience coordonnée et cohérente pour vos clients. Avec le [!DNL Segmentation Service], composant d’Adobe Experience Platform, il est possible de réaliser des campagnes marketing personnalisées et pertinentes.

Real-Time CDP repose sur Adobe Experience Platform et utilise de nombreux services et fonctionnalités d’[!DNL Experience Platform]. Grâce à [!DNL Segmentation Service], vous pouvez proposer un marketing sur mesure en divisant vos clients en groupes restreints aux caractéristiques similaires.

## Segmentation

La segmentation est le processus de définition d’attributs ou de comportements spécifiques partagés par un sous-ensemble de profils de votre banque de profils afin de distinguer un groupe de clients potentiels de votre base de clients. Par exemple, dans une campagne par e-mail intitulée « Avez-vous oublié d’acheter vos baskets ? », vous souhaitez peut-être connaître l’audience de tous les utilisateurs ayant recherché des baskets au cours des 30 derniers jours sans effectuer d’achat. En utilisant différentes définitions de segment, vous pouvez vous concentrer sur vos différentes audiences, offrant ainsi une expérience marketing plus personnalisée.

## [!DNL Audience Builder]

[!DNL Platform] vous permet de créer et d’accéder facilement à des définitions de segment, ainsi que d’utiliser différents blocs de création pour caractériser vos audiences avec plus de précision. Pour plus d’informations sur l’utilisation du Créateur d’audience, consultez le [guide du Créateur d’audience](./audience-builder.md).

## IA dédiée aux clients

L’IA dédiée aux clients, incluse dans Real-time Customer Data Platform, vous permet de générer des prédictions client au niveau individuel avec des explications.

À l’aide de facteurs d’influence, Customer AI peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. De plus, vous pouvez tirer parti des prédictions et des informations de l’IA dédiée aux clients pour personnaliser les expériences client en diffusant les offres et les messages les plus appropriés. L’IA dédiée aux clients peut vous aider à :

* proposer des modèles de propension des clients à haute précision pour une segmentation et un ciblage plus forts ;
* comprendre les facteurs d’influence et la probabilité derrière certains comportements des clients ;
* offrir des options personnalisables pour les cas d’utilisation et les données uniques de votre entreprise ;
* améliorer le profil client en temps réel grâce aux scores de propension des clients, comme les taux d’attrition et de conversion ;
* améliorer les profils client avec des facteurs d’influence pour les scores de propension ;
* Création d’audiences de clients en fonction de facteurs d’influence et de scores de propension.

L’IA dédiée aux clients se trouve dans l’onglet **[!UICONTROL Services]** sous **[!UICONTROL Services Adobe]**.

![Emplacement de l’IA dédiée aux clients](../assets/overview/rtcdp-customer-ai.png)

### Prise en main de Customer AI

Pour commencer à utiliser l’IA dédiée aux clients, vous devez suivre le [tutoriel sur la préparation des données](../../intelligent-services/data-preparation.md) et configurer le schéma d’entrée en fonction de votre cas d’utilisation. Ensuite, vous devrez [configurer une instance IA dédiée aux clients](../../intelligent-services/customer-ai/user-guide/configure.md). Après la configuration d’une instance, un modèle est généré, où vous pouvez [afficher vos informations et vos scores](../../intelligent-services/customer-ai/user-guide/discover-insights.md). En utilisant les données générées à partir de votre modèle, vous pouvez créer des audiences pour l’activation pilotée par les données.

Pour en savoir plus sur l’IA dédiée aux clients, commencez par consulter la [présentation de l’IA dédiée aux clients](../../intelligent-services/customer-ai/overview.md). En outre, la vidéo suivante montre comment l’IA dédiée aux clients enrichit les profils clients avec des propensions basées sur l’IA et renforce la segmentation et le ciblage des clients.

>[!VIDEO](https://video.tv.adobe.com/v/40374/?quality=12&learn=on)


## Étapes suivantes

Après avoir lu cette présentation, vous devriez maintenant comprendre comment Real-time CDP utilise [!DNL Segmentation Service] pour améliorer l’adaptation et la personnalisation des campagnes marketing. Pour plus d’informations sur [!DNL Segmentation Service], consultez la [documentation sur la segmentation](../../segmentation/home.md).

---
keywords: Experience Platform;accueil;rubriques populaires;Application des politiques;Application automatique;Application basée sur les API;gouvernance des données
solution: Experience Platform
title: Présentation de l’application des politiques
description: Découvrez comment les politiques d’utilisation des données sont appliquées sur Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
TQID: https://experienceleague.adobe.com/oyKG2F221xBKRdWXByxwY-MwI-QmveafBwsXj-8-MCM
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 100%

---

# Présentation de l’application des politiques

Une fois que les [libellés d’utilisation des données](../labels/overview.md) ont été appliqués et que les [politiques d’utilisation des données](../policies/overview.md) ont été définies, vous pouvez appliquer ces politiques afin d’empêcher les opérations de données qui constituent des violations de politique.

>[!NOTE]
>
>Ce document se concentre sur l’application des politiques d’utilisation des données. Pour plus d’informations sur les politiques de contrôle d’accès, reportez-vous au guide sur le [contrôle d’accès basé sur les attributs](../../access-control/abac/overview.md).

Il existe deux méthodes d’application des politiques dans Adobe Experience Platform : l’application automatique et l’application basée sur les API.

## Application automatique

Experience Platform tire parti des fonctionnalités de gestion des politiques, de classification des données et de parenté des données pour évaluer automatiquement et faire apparaître les violations de politiques. Pour plus d’informations, consultez la présentation de l’[application automatique des politiques](./auto-enforcement.md).

## Application basée sur les API

L’API [!DNL Policy Service] fournit des points d’entrée qui vous permettent de tester les actions marketing par rapport aux jeux de données ou à des combinaisons arbitraires de libellés d’utilisation des données, afin de vérifier si des violations de politiques se produisent. En fonction de la réponse de l’API, vous pouvez configurer des protocoles dans votre application d’expérience, afin d’être en conformité avec les politiques de gouvernance des données.

Pour savoir comment évaluer les politiques à l’aide de l’API, consultez le tutoriel sur [l’application basée sur l’API](./api-enforcement.md).

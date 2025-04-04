---
title: Synchronisation des identités entre Audience Manager et Adobe Experience Platform à l’aide de la SDK Web Experience Platform
description: Découvrez comment synchroniser les identités entre Audience Manager et Adobe Experience Platform à l’aide d’Experience Platform Web SDK
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identités;synchroniser les identités;espace de noms;
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Synchronisation des identités entre Audience Manager et Experience Platform

Adobe Experience Platform Web SDK prend en charge la possibilité de déclarer des ID client et leurs états d’authentification via la commande [sendEvent](./overview.md#syncing-identities).

Sélectionnez vos espaces de noms dans la [Espaces de noms du service d’identités](../../identity/../identity-service/features/namespaces.md) pour indiquer le contexte auquel une identité se rapporte, à l’aide des valeurs de la colonne Symbole d’identité :

![Affichage de l’interface utilisateur des espaces de noms](../assets/identity/edge_namespaceUI_identity-symbol.png)

En tant que client Audience Manager, toutes vos sources de données existantes qui utilisent le type d’identifiant : sur l’ensemble des appareils sont automatiquement associées à un espace de noms d’identité. Pour trouver l’espace de noms d’identité correspondant à votre Source de données Audience Manager, connectez-vous à Adobe Experience Platform et accédez à la section Identités .

Tout nouveau Source de données [!DNL Audience Manager] qui utilise le type d’identifiant : sur l’ensemble des appareils générera un espace de noms d’identité correspondant. Les types d’ID Data Source Cookie et ID d’appareil Advertising ne sont actuellement pas pris en charge. En outre, tout espace de noms d’identité créé dans Adobe Experience Platform génère un Source de données [!DNL Audience Manager] correspondant. Notez toutefois que la méthode syncIdentity ne prend en charge que les symboles d’identité d’espace de noms.

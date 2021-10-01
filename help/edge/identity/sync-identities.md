---
title: Synchronisation des identités entre Audience Manager et Adobe Experience Platform à l’aide du SDK Web Platform
description: Découvrez comment synchroniser les identités entre Audience Manager et Adobe Experience Platform à l’aide du SDK Web Platform
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identités;identités de synchronisation;espace de noms;
source-git-commit: 3a1d08a4ea87ee3db7a2a8b048d5721fa679c372
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Synchronisation des identités entre l’Audience Manager et l’Experience Platform

Le SDK Web de Adobe Experience Platform prend en charge la possibilité de déclarer les ID de client et leurs états d’authentification via la commande [sendEvent](./overview.md#syncing-identities).

Sélectionnez vos espaces de noms dans les [Espaces de noms Identity Service](../../identity/../identity-service/namespaces.md) pour indiquer le contexte auquel une identité se rapporte, à l’aide des valeurs de la colonne Symbole d’identité :

![Vue de l’interface utilisateur des espaces de noms](../images/identity/edge_namespaceUI_identity-symbol.png)

En tant que client d’Audience Manager, toutes vos sources de données existantes qui utilisent le type d’ID : Un espace de noms d’identité est automatiquement associé à l’ensemble des appareils. Pour trouver l’espace de noms d’identité correspondant à votre source de données d’Audience Manager, connectez-vous à Adobe Experience Platform et accédez à la section Identités .

Toute nouvelle source de données [!DNL Audience Manager] qui utilise le type d’ID : L’ensemble des appareils génère un espace de noms d’identité correspondant. Les types d’ID de source de données Cookie et ID de publicité de périphérique ne sont actuellement pas pris en charge. De plus, tout espace de noms d’identité créé dans Adobe Experience Platform génère une source de données [!DNL Audience Manager] correspondante, mais notez que la méthode syncIdentity ne prend en charge que les symboles d’identité de l’espace de noms.

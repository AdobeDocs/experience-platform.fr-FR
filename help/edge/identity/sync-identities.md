---
title: Synchronisation des identités entre Audience Manager et Adobe Experience Platform à l’aide du SDK Web Platform
description: Découvrez comment synchroniser les identités entre Audience Manager et Adobe Experience Platform à l’aide du SDK Web Platform
seo-description: Learn how to sync identities with Adobe Audience Manager with Experience Platform Web SDK
keywords: audience manager;aam;identités;identités de synchronisation;espace de noms;
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Synchronisation des identités entre Audience Manager et Experience Platform

Le SDK Web de Adobe Experience Platform prend en charge la possibilité de déclarer les ID de client et leurs états d’authentification via le [sendEvent](./overview.md#syncing-identities) .

Choisissez vos espaces de noms dans la [Espaces de noms Identity Service](../../identity/../identity-service/features/namespaces.md) pour indiquer le contexte auquel une identité se rapporte, en utilisant les valeurs de la colonne Symbole d’identité :

![Vue de l’interface utilisateur des espaces de noms](../assets/identity/edge_namespaceUI_identity-symbol.png)

En tant que client d’Audience Manager, toutes vos sources de données existantes qui utilisent le type d’ID : Cross-Device (Interappareil) disposent automatiquement d’un espace de noms d’identité correspondant. Pour trouver l’espace de noms d’identité correspondant à votre source de données d’Audience Manager, connectez-vous à Adobe Experience Platform et accédez à la section Identités .

Tout nouveau [!DNL Audience Manager] Source de données qui utilise le type d’ID : Cross-Device génère un espace de noms d’identité correspondant. Types d’ID de source de données Le cookie et l’ID de publicité du périphérique ne sont actuellement pas pris en charge. En outre, tout espace de noms d’identité créé dans Adobe Experience Platform génère un [!DNL Audience Manager] Source de données, mais notez que la méthode syncIdentity ne prend en charge que les symboles d’identité de l’espace de noms.

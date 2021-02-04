---
title: Synchronisation des identités avec l’Audience Manager et le Adobe Experience Platform
seo-title: Synchronisation des identités avec l’Audience Manager et Adobe Experience Platform avec Adobe Experience Platform Web SDK
description: Découvrez comment synchroniser les identités avec Adobe Audience Manager avec le SDK Web Experience Platform
seo-description: Découvrez comment synchroniser les identités avec Adobe Audience Manager avec le SDK Web Experience Platform
keywords: gestionnaire d'audiences ; aam ; identités ; identités synchronisées ; espace de nommage ;
translation-type: tm+mt
source-git-commit: 0928dd3eb2c034fac14d14d6e53ba07cdc49a6ea
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Synchronisation des identités

Adobe Experience Platform Web SDK prend en charge la possibilité de déclarer les ID de client et leurs états d’authentification via la commande [sendEvent](./overview.md#syncing-identities).

Choisissez vos espaces de nommage dans les [Espaces de nommage du service d&#39;identité](../../identity/../identity-service/namespaces.md) pour indiquer le contexte auquel une identité se rapporte, en utilisant les valeurs de la colonne Symbole d&#39;identité :

![Vue de l’interface utilisateur Espaces de nommage](../../assets/edge_namespaceUI_identity-symbol.png)

En tant que client d’Audience Manager, toutes vos sources de données existantes qui utilisent le type d’ID : L&#39;Espace de nommage d&#39;identité est automatiquement associé à plusieurs périphériques. Pour trouver l&#39;Espace de nommage d&#39;identité correspondant à votre source de données d&#39;Audience Manager, connectez-vous à Adobe Experience Platform et accédez à la section Identités.

Toute nouvelle source de données [!DNL Audience Manager] utilisant le type d’ID : Un Espace de nommage d&#39;identité est généré sur plusieurs périphériques. Les types d’ID de source de données Cookie et ID de publicité de périphérique ne sont pas pris en charge actuellement. De plus, tout Espace de nommage d&#39;identité créé dans Adobe Experience Platform génère une source de données [!DNL Audience Manager] correspondante, mais notez que la méthode syncIdentity ne prend en charge que les symboles d&#39;identité d&#39;Espace de nommage.

---
title: Envoi de données à Adobe Audience Manager
seo-title: Envoi de données à Adobe Audience Manager avec le SDK Web d’Adobe Experience Platform
description: Découvrez comment envoyer des données à Adobe Audience Manager avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données à Adobe Audience Manager avec le SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: 4bea14d18ce119bdec0d428f885d240f92244cfc
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager sur Experience Platform Edge Network

Le SDK Web d’Adobe Experience Platform est intégré à Adobe Audience Manager et prend en charge l’envoi et la réception de données à partir d’Audience Manager, des destinations de cookies et d’URL et la synchronisation des identifiants.

## Activation d’Audience Manager

Pour activer Audience Manager, vous devez effectuer les opérations suivantes :

- Activez Audience Manager dans votre configuration [de](../../fundamentals/edge-configuration.md)bord.
- Activez ou désactivez les destinations de cookie et d’URL.
- Spécifiez votre Conteneur de synchronisation des identifiants pour les synchronisations de partenaires externes (facultatif).

## Synchronisation des identités

Le SDK Web d’Adobe Experience Platform prend en charge la possibilité de déclarer les ID de client et leurs états d’authentification via la commande [SyncIdentity](../../fundamentals/identity.md) .

La méthode syncIdentity utilise des Espaces de nommage [](../../../identity/../identity-service/namespaces.md) Identity Service pour indiquer le contexte auquel une identité se rapporte. En tant que client Audience Manager, toutes vos sources de données existantes qui utilisent le type d’ID : Un Espace de nommage d&#39;identité est automatiquement ajouté pour les périphériques croisés. Pour trouver l’Espace de nommage d’identité correspondant à votre source de données Audience Manager, connectez-vous à Adobe Experience Platform et accédez à la section Identités.

![Vue de l’interface utilisateur Espaces de nommage](../../../assets/edge_configuration_identity.png)

Ici, vous pouvez rechercher la source de données de votre Gestionnaire d’Audiences par nom. La méthode syncIdentity utilise le symbole d&#39;identité pour indiquer l&#39;Espace de nommage.

Toute nouvelle source de données Audience Manager utilisant le type d’ID : Un Espace de nommage d&#39;identité est généré sur plusieurs périphériques. Les types d’ID de source de données Cookie et ID de publicité de périphérique ne sont pas pris en charge actuellement. De plus, tout Espace de nommage d’identité créé dans Adobe Experience Platform génère une source de données Audience Manager correspondante, mais notez que la méthode syncIdentity ne prend en charge que les symboles d’identité d’Espace de nommage.

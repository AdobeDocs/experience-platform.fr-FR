---
title: Envoi de données à l'Adobe Audience Manager
seo-title: Envoi de données à l'Adobe Audience Manager avec le SDK Web Adobe Experience Platform
description: Découvrez comment envoyer des données à l'Adobe Audience Manager avec le SDK Web Experience Platform
seo-description: Découvrez comment envoyer des données à l'Adobe Audience Manager avec le SDK Web Experience Platform
translation-type: tm+mt
source-git-commit: 6a83ab1c6405f45700f4f8899139010d50010b0c
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Audience Manager sur le réseau Edge Experience Platform Network

L’Adobe Experience Platform Web SDK est intégré à l’Adobe Audience Manager et prend en charge l’envoi et la réception de données provenant des destinations d’Audience Manager, de cookie et d’URL, ainsi que la synchronisation des identifiants.

## Activation de l&#39;Audience Manager

Pour activer l’Audience Manager, vous devez effectuer les opérations suivantes :

- Activez l’Audience Manager dans la configuration [de votre](../../fundamentals/edge-configuration.md)bord.
- Activez ou désactivez les destinations de cookie et d’URL.
- Spécifiez votre Conteneur de synchronisation des identifiants pour les synchronisations de partenaires externes (facultatif).

## Synchronisation des identités

Le Adobe Experience Platform Web SDK prend en charge la possibilité de déclarer les ID de client et leurs états d&#39;authentification via la commande [SyncIdentity](../../fundamentals/identity.md) .

La méthode syncIdentity utilise des Espaces de nommage [](../../../identity/../identity-service/namespaces.md) Identity Service pour indiquer le contexte auquel une identité se rapporte. En tant que client d’Audience Manager, toutes vos sources de données existantes qui utilisent le type d’ID : Un Espace de nommage d&#39;identité est automatiquement ajouté pour les périphériques croisés. Pour trouver l&#39;Espace de nommage d&#39;identité correspondant à votre source de données d&#39;Audience Manager, connectez-vous à l&#39;Adobe Experience Platform et accédez à la section Identités.

![Vue de l’interface utilisateur Espaces de nommage](../../../assets/edge_configuration_identity.png)

Ici, vous pouvez rechercher votre source de données d’Audience Manager par nom. La méthode syncIdentity utilise le symbole d&#39;identité pour indiquer l&#39;Espace de nommage.

Toute nouvelle source de données d’Audience Manager utilisant le type d’ID : Un Espace de nommage d&#39;identité est généré sur plusieurs périphériques. Les types d’ID de source de données Cookie et ID de publicité de périphérique ne sont pas pris en charge actuellement. De plus, tout Espace de nommage d&#39;identité créé dans l&#39;Adobe Experience Platform génère une source de données d&#39;Audience Manager correspondante, mais notez que la méthode syncIdentity ne prend en charge que les symboles d&#39;identité de l&#39;Espace de nommage.

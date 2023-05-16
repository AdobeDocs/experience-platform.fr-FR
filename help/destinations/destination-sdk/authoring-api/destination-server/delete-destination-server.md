---
description: Cette page illustre l’appel API utilisé pour supprimer une configuration de serveur de destination existante en Adobe Experience Platform Destination SDK.
title: Suppression d’une configuration de serveur de destination
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 33%

---


# Suppression d’une configuration de serveur de destination

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour supprimer une configuration de serveur de destination existante, à l’aide de la variable `/authoring/destination-servers` Point d’entrée de l’API.

Pour une description détaillée des fonctionnalités que vous pouvez supprimer via ce point de terminaison, consultez les articles suivants :

* [Spécifications de serveur pour les destinations créées avec Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Spécifications de modèle pour les destinations créées avec Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Format des messages](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuration du formatage des fichiers](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API du serveur de destination {#get-started}

Avant de poursuivre, veuillez consulter la section [Guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

## Suppression d’une configuration de serveur de destination {#delete}

Vous pouvez supprimer une [existant](create-destination-server.md) configuration du serveur de destination en effectuant une `DELETE` à la fonction `/authoring/destination-servers` point de terminaison avec la fonction `{INSTANCE_ID}`de la configuration du serveur de destination que vous souhaitez supprimer.

>[!TIP]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destination-servers`

Pour obtenir la configuration d’un serveur de destination existant et ses `{INSTANCE_ID}`, voir l’article sur [récupération d’une configuration de serveur de destination](retrieve-destination-server.md).

**Format d’API**

```http
DELETE /authoring/destination-servers/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | `ID` de la configuration de serveur de destination que vous souhaitez supprimer. |

+++Requête

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment supprimer un serveur de destination existant via la Destination SDK `/authoring/destination-servers` Point d’entrée de l’API.

Pour en savoir plus sur ce que vous pouvez faire avec ce point de terminaison, consultez les articles suivants :

* [Création d’une configuration de serveur de destination](create-destination-server.md)
* [Récupération de la configuration d’un serveur de destination](retrieve-destination-server.md)
* [Mise à jour de la configuration d’un serveur de destination](update-destination-server.md)


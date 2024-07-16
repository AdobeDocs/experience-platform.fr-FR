---
description: Cette page illustre comment l’appel API est utilisé pour supprimer une configuration de serveur de destination existante avec Adobe Experience Platform Destination SDK.
title: Suppression d’une configuration de serveur de destination
exl-id: 2322a2ce-220e-4590-a553-b15152412752
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 100%

---

# Suppression d’une configuration de serveur de destination

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour supprimer une configuration de serveur de destination existante à l’aide du point d’entrée `/authoring/destination-servers` de l’API.

Pour obtenir une description détaillée des fonctionnalités que vous pouvez supprimer depuis ce point d’entrée, consultez les articles suivants :

* [Spécifications de serveur pour les destinations créées avec Destination SDK](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [Spécifications de modèle pour les destinations créées avec Destination SDK](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [Format des messages](../../../destination-sdk/functionality/destination-server/message-format.md)
* [Configuration du formatage des fichiers](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API du serveur de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Suppression d’une configuration de serveur de destination {#delete}

Vous pouvez supprimer une configuration de serveur de destination [existante](create-destination-server.md) en effectuant une requête `DELETE` au point d’entrée `/authoring/destination-servers` avec la fonction `{INSTANCE_ID}` de la configuration de serveur de destination que vous souhaitez supprimer.

>[!TIP]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destination-servers`

Pour obtenir une configuration de serveur de destination existante et son `{INSTANCE_ID}` correspondant, consultez l’article sur la [récupération d’une configuration de serveur de destination](retrieve-destination-server.md).

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

Une réponse réussie renvoie le statut HTTP 200 avec une réponse HTTP vide.

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment supprimer un serveur de destination existant avec le point d’entrée `/authoring/destination-servers` Destination SDK de l’API.

Pour en savoir plus sur les fonctionnalités offertes par ce point d’entrée, consultez les articles suivants :

* [Création d’une configuration de serveur de destination](create-destination-server.md)
* [Récupération d’une configuration de serveur de destination](retrieve-destination-server.md)
* [Mise à jour d’une configuration de serveur de destination](update-destination-server.md)

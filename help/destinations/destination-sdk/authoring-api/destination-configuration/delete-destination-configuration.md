---
description: Cette page illustre l’appel API utilisé pour supprimer une configuration de destination existante en Adobe Experience Platform Destination SDK.
title: Suppression d’une configuration de destination
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 35%

---


# Suppression d’une configuration de destination

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour supprimer une configuration de destination existante, à l’aide de la variable `/authoring/destinations` Point d’entrée de l’API.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API de configuration de destination {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Suppression d’une configuration de destination {#delete}

Vous pouvez supprimer une [existant](create-destination-configuration.md) configuration du serveur de destination en effectuant une `DELETE` à la fonction `/authoring/destinations` point de terminaison avec la fonction `{INSTANCE_ID}`de la configuration de destination que vous souhaitez supprimer.

>[!TIP]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations`

Pour obtenir une configuration de destination existante et sa `{INSTANCE_ID}`, voir l’article sur [récupération d’une configuration de destination](retrieve-destination-configuration.md).

**Format d’API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Valeur `ID` de la configuration de destination à supprimer. |

+++Requête

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.


## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment supprimer une configuration de destination existante via la Destination SDK `/authoring/destinations` Point d’entrée de l’API.

Pour en savoir plus sur ce que vous pouvez faire avec ce point de terminaison, consultez les articles suivants :

* [Création d’une configuration de destination](create-destination-configuration.md)
* [Récupération d’une configuration de destination](retrieve-destination-configuration.md)
* [Mise à jour d’une configuration de destination](update-destination-configuration.md)


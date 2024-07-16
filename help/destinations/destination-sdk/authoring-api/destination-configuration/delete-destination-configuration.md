---
description: Cette page illustre comment l’appel API est utilisé pour supprimer une configuration de destination existante avec Adobe Experience Platform Destination SDK.
title: Suppression d’une configuration de destination
exl-id: c7309ab7-1b8d-46d4-8017-fd4aa5918cdd
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 100%

---

# Suppression d’une configuration de destination

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour supprimer une configuration de destination existante à l’aide du point d’entrée `/authoring/destinations` de l’API.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations dʼAPI de configuration de destinations {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Suppression d’une configuration de destination {#delete}

Vous pouvez supprimer une configuration de serveur de destination [existante](create-destination-configuration.md) en effectuant une requête `DELETE` au point d’entrée `/authoring/destinations` avec la fonction `{INSTANCE_ID}` de la configuration de destination que vous souhaitez supprimer.

>[!TIP]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations`

Pour obtenir une configuration de destination existante et son `{INSTANCE_ID}` correspondant, consultez l’article sur la [récupération d’une configuration de destination](retrieve-destination-configuration.md).

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

Une réponse réussie renvoie le statut HTTP 200 avec une réponse HTTP vide.


## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment supprimer une configuration de destination existante avec le point d’entrée `/authoring/destinations` Destination SDK de l’API.

Pour en savoir plus sur les fonctionnalités offertes par ce point d’entrée, consultez les articles suivants :

* [Création d’une configuration de destination](create-destination-configuration.md)
* [Récupération d’une configuration de destination](retrieve-destination-configuration.md)
* [Mise à jour d’une configuration de destination](update-destination-configuration.md)

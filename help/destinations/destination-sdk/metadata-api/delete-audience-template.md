---
description: Cette page illustre l’appel API utilisé pour supprimer un modèle d’audience existant par le biais de l’Adobe Experience Platform Destination SDK.
title: Suppression d’un modèle d’audience
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 42%

---


# Suppression d’un modèle d’audience

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/audience-templates`

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour supprimer un modèle d’audience, en utilisant la variable `/authoring/audience-templates` Point d’entrée de l’API.

Pour une description détaillée des fonctionnalités que vous pouvez configurer via ce point de terminaison, voir [gestion des métadonnées d’audience](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API de modèle d’audience {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Suppression d’un modèle d’audience {#delete}

Vous pouvez supprimer une [existant](create-audience-template.md) modèle d’audience en effectuant une `DELETE` à la fonction `/authoring/audience-templates` point de terminaison avec la fonction `{INSTANCE_ID}`du modèle d’audience que vous souhaitez supprimer.

Pour obtenir un modèle d&#39;audience existant et son `{INSTANCE_ID}`, voir l’article sur [récupération d’un modèle d’audience](retrieve-audience-template.md).

**Format d’API**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Valeur `ID` du modèle d’audience à supprimer. |

+++Requête

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Réponse

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

+++

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment supprimer un modèle d’audience à l’aide du `/authoring/audience-templates` Point d’entrée de l’API. Poursuivez votre apprentissage dans la section [Comment utiliser Destination SDK pour configurer votre destination](../guides/configure-destination-instructions.md) et obtenez une vue dʼensemble du processus de configuration de votre destination.

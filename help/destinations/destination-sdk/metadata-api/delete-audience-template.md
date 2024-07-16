---
description: Cette page illustre comment l’appel API est utilisé pour supprimer un modèle d’audience existant avec Adobe Experience Platform Destination SDK.
title: Suppression d’un modèle d’audience
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 100%

---

# Suppression d’un modèle d’audience

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/audience-templates`

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour supprimer un modèle d’audience à l’aide du point d’entrée de l’API `/authoring/audience-templates`.

Pour obtenir une description détaillée des fonctionnalités configurables avec ce point d’entrée, consultez l’article sur la [gestion des métadonnées d’audience](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API des modèles d’audience {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Suppression d’un modèle d’audience {#delete}

Vous pouvez supprimer un modèle d’audience [existant](create-audience-template.md) en effectuant une requête `DELETE` au point d’entrée `/authoring/audience-templates` avec la fonction `{INSTANCE_ID}` du modèle d’audience que vous souhaitez supprimer.

Pour obtenir un modèle d’audience existant et son `{INSTANCE_ID}` correspondant, consultez l’article sur la [récupération d’un modèle d’audience](retrieve-audience-template.md).

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

Une réponse réussie renvoie le statut HTTP 200 avec une réponse HTTP vide.

+++

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment supprimer un modèle d’audience à l’aide du point d’entrée `/authoring/audience-templates` de l’API. Consultez la documentation [Comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.

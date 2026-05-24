---
description: Cette page illustre comment l’appel API est utilisé pour supprimer un modèle d’audience existant avec Adobe Experience Platform Destination SDK.
title: Suppression d’un modèle d’audience
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
TQID: https://experienceleague.adobe.com/21vqU20Eb2eVv-6qFWc5BiAZX7ap0W6aErl4uEGvGhY
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 286
ht-degree: 82%

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

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de destination requise et les en-têtes requis.

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

{style="table-layout:auto"}

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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Voir [Codes d’état API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment supprimer un modèle d’audience à l’aide du point d’entrée `/authoring/audience-templates` de l’API. Consultez la documentation [Comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.

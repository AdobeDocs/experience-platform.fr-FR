---
description: Cette page illustre comment l’appel API est utilisé pour supprimer une configuration d’informations d’identification Adobe Experience Platform Destination SDK.
title: Suppression d’une configuration d’informations d’identification
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 86%

---

# Suppression d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la payload que vous pouvez utiliser pour supprimer une configuration d’informations d’identification à l’aide du point d’entrée `/authoring/credentials` de l’API.

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous ***ne devez pas*** utiliser le point d’entrée de l’API `/credentials`. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`.
> 
>Pour en savoir plus sur les types d’authentification pris en charge, consultez la documentation [Configuration de l’authentification du client](../functionality/destination-configuration/customer-authentication.md).

Utilisez ce point d’entrée de l’API pour créer une configuration d’informations d’identification uniquement s’il existe un système d’authentification global entre Adobe et votre plateforme de destination et si le client [!DNL Experience Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à la destination. Dans ce cas, vous devez créer une configuration d’informations d’identification à l’aide du point d’entrée `/credentials` de l’API.

Lors de l’utilisation d’un système d’authentification global, vous devez définir les `"authenticationRule":"PLATFORM_AUTHENTICATION"` dans la configuration [diffusion de destination](../functionality/destination-configuration/destination-delivery.md) lors de la [création d’une configuration de destination](../authoring-api/destination-configuration/create-destination-configuration.md). Ensuite, vous devez créer une [configuration des informations d’identification](../credentials-api/create-credential-configuration.md) et transmettre l’identifiant de l’objet d’identification dans le paramètre `authenticationId` de la configuration [diffusion de destination](/help/destinations/destination-sdk/functionality/destination-configuration/destination-delivery.md#platform-authentication).

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API des informations d’identification {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

## Suppression d’une configuration d’informations d’identification {#delete}

Vous pouvez supprimer une configuration d’informations d’identification [existante](create-credential-configuration.md) en effectuant une requête `DELETE` au point d’entrée `/authoring/credentials` avec la fonction `{INSTANCE_ID}` de la configuration des informations d’identification que vous souhaitez supprimer.

Pour obtenir une configuration de destination existante et son `{INSTANCE_ID}` correspondant, consultez l’article sur la [récupération d’une configuration d’informations d’identification](retrieve-credential-configuration.md).

**Format d’API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Valeur `ID` de la configuration d’informations d’identification que vous souhaitez supprimer. |

La requête suivante supprime une configuration d’informations d’identification définie par le paramètre `{INSTANCE_ID}`.

+++Requête

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes d’état API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs d’en-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage d’Experience Platform.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce document. À présent, vous savez comment supprimer une configuration d’informations d’identification à l’aide du point d’entrée `/authoring/credentials` de l’API. Consultez la documentation [Comment utiliser Destination SDK pour configurer la destination](../guides/configure-destination-instructions.md) afin de comprendre la place de cette étape dans le processus de configuration de la destination.

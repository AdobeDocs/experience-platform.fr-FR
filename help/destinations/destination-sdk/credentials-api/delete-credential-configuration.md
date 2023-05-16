---
description: Cette page illustre l’appel API utilisé pour supprimer un Adobe Experience Platform Destination SDK de configuration des informations d’identification.
title: Suppression d’une configuration d’informations d’identification
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 38%

---


# Suppression d’une configuration d’informations d’identification

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/credentials`

Cette page illustre la requête d’API et la charge utile que vous pouvez utiliser pour supprimer une configuration d’informations d’identification à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API.

## Quand utiliser le point d’entrée de l’API `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>Dans la plupart des cas, vous ***ne devez pas*** utiliser le point d’entrée de l’API `/credentials`. Au lieu de cela, vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`.
> 
>Lecture [Configuration de l’authentification du client](../functionality/destination-configuration/customer-authentication.md) pour plus d’informations sur les types d’authentification pris en charge.

Utilisez ce point de terminaison d’API pour créer une configuration d’informations d’identification uniquement s’il existe un système d’authentification global entre l’Adobe et votre plateforme de destination, et que la variable [!DNL Platform] Le client n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer une configuration d’informations d’identification à l’aide de la fonction `/credentials` Point d’entrée de l’API.

Lorsque vous utilisez un système d’authentification global, vous devez définir `"authenticationRule":"PLATFORM_AUTHENTICATION"` dans le [diffusion de destination](../functionality/destination-configuration/destination-delivery.md) lors de la configuration [création d’une configuration de destination](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations de l’API de des informations d’identification {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Suppression d’une configuration d’informations d’identification {#delete}

Vous pouvez supprimer une [existant](create-credential-configuration.md) configuration des informations d’identification en effectuant une `DELETE` à la fonction `/authoring/credentials` point de terminaison avec la fonction `{INSTANCE_ID}`de la configuration des informations d’identification que vous souhaitez supprimer.

Pour obtenir une configuration de destination existante et sa `{INSTANCE_ID}`, voir l’article sur [récupération d’une configuration des informations d’identification](retrieve-credential-configuration.md).

**Format d’API**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{INSTANCE_ID}` | Le `ID` de la configuration des informations d’identification que vous souhaitez supprimer. |

La requête suivante supprime une configuration d’informations d’identification définie par la variable `{INSTANCE_ID}` .

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

Une réponse réussie renvoie un état HTTP 200 avec une réponse HTTP vide.

+++

## Gestion des erreurs d’API {#error-handling}

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes {#next-steps}

Après avoir lu ce document, vous savez maintenant comment supprimer une configuration d’informations d’identification à l’aide de la variable `/authoring/credentials` Point d’entrée de l’API. Poursuivez votre apprentissage dans la section [Comment utiliser Destination SDK pour configurer votre destination](../guides/configure-destination-instructions.md) et obtenez une vue dʼensemble du processus de configuration de votre destination.

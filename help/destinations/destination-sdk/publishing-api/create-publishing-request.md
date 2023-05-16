---
description: Découvrez comment formater un appel API pour envoyer une demande de publication de destination via l’Adobe Experience Platform Destination SDK.
title: Création d’une requête de publication de destination
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 56%

---


# Création d’une requête de publication de destination

>[!IMPORTANT]
>
>Vous ne devez utiliser ce point de terminaison d’API que si vous envoyez une destination productisée (publique), à utiliser par d’autres clients Experience Platform. Si vous créez une destination privée pour votre propre utilisation, vous n’avez pas besoin d’envoyer officiellement la destination à l’aide de l’API de publication.

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Une fois votre destination configurée et testée, vous pouvez l’envoyer à Adobe pour révision et publication. Lecture [Envoyer pour révision d’une destination créée dans Destination SDK](../guides/submit-destination.md) pour toutes les autres étapes, vous devez effectuer dans le cadre du processus d’envoi de destination.

Utilisez le point d’entrée de lʼAPI de publication des destinations pour envoyer une demande de publication dans les cas suivants :

* En tant que partenaire du Destination SDK, vous souhaitez que votre destination personnalisée soit disponible dans toutes les organisations Experience Platform, afin que tous les clients Experience Platform puissent l’utiliser ;
* Vous faites *toutes les mises à jour* à vos configurations. Les mises à jour de configuration ne sont répercutées dans la destination qu’après l’envoi d’une nouvelle demande de publication, qui est approuvée par l’équipe Experience Platform.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations dʼAPI de publication de destinations {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes requis.

## Envoyer une configuration de destination pour publication {#create}

Vous pouvez envoyer une configuration de destination pour publication en réalisant une requête POST au point d’entrée `/authoring/destinations/publish`.

**Format d’API**

```http
POST /authoring/destinations/publish
```

+++Requête

La requête suivante envoie une destination pour publication dans les organisations configurées par les paramètres fournis dans la payload. La payload ci-dessous inclut tous les paramètres acceptés par le point dʼentrée `/authoring/destinations/publish`.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `destinationId` | Chaîne | Identifiant de destination de la configuration de destination que vous envoyez pour publication. Obtention de l’identifiant de destination d’une configuration de destination à l’aide de la variable [récupération d’une configuration de destination](../authoring-api/destination-configuration/retrieve-destination-configuration.md) appel API. |
| `destinationAccess` | Chaîne | Utilisation `ALL` pour que votre destination apparaisse dans le catalogue pour tous les clients Experience Platform. |

{style="table-layout:auto"}

+++Réponse

Une réponse réussie renvoie un état HTTP 201 avec les détails de la requête de publication de destination.

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après la lecture de ce document, vous savez désormais comment envoyer une demande de publication pour votre destination. L’équipe dʼAdobe Experience Platform examinera votre demande de publication et vous recontactera dans un délai de cinq jours ouvrables.
---
description: Découvrez comment formater un appel API pour soumettre une requête de publication de destination avec Adobe Experience Platform Destination SDK.
title: Création d’une requête de publication de destination
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 100%

---

# Création d’une requête de publication de destination

>[!IMPORTANT]
>
>Vous ne devez utiliser ce point d’entrée de l’API que si vous soumettez une destination personnalisée (publique), qui sera utilisée par d’autres clients et clientes d’Experience Platform. Si vous créez une destination privée destinée à votre propre usage, vous n’avez pas besoin de soumettre officiellement la destination avec l’API de publication.

>[!IMPORTANT]
>
>**Point d’entrée de l’API** : `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Une fois la destination configurée et testée, vous pouvez l’envoyer à Adobe pour révision et publication. Consultez la documentation [Envoyer pour révision une destination créée dans Destination SDK](../guides/submit-destination.md) pour découvrir les autres étapes à suivre dans le cadre du processus de soumission d’une destination.

Utilisez le point d’entrée de lʼAPI de publication des destinations pour envoyer une demande de publication dans les cas suivants :

* En tant que partenaire du Destination SDK, vous souhaitez que votre destination personnalisée soit disponible dans toutes les organisations Experience Platform, afin que tous les clients et clientes Experience Platform puissent l’utiliser ;
* Vous *mettez à jour* vos configurations. Les mises à jour de configuration sont prises en compte dans la destination uniquement après la soumission d’une nouvelle requête de publication, qui est approuvée par l’équipe d’Experience Platform.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Prise en main des opérations dʼAPI de publication de destinations {#get-started}

Avant de poursuivre, consultez le [guide de prise en main](../getting-started.md) pour obtenir des informations importantes à connaître avant d’effectuer des appels vers l’API, notamment sur la manière d’obtenir l’autorisation de création de la destination et les en-têtes obligatoires.

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
| `destinationId` | Chaîne | Identifiant de destination de la configuration de destination que vous envoyez pour publication. Obtenez l’identifiant de destination d’une configuration de destination à l’aide de l’appel API [récupération d’une configuration de destination](../authoring-api/destination-configuration/retrieve-destination-configuration.md). |
| `destinationAccess` | Chaîne | Utilisez `ALL` pour rendre la destination accessible dans le catalogue à l’ensemble de la clientèle d’Experience Platform. |

{style="table-layout:auto"}

+++

+++Réponse

Une réponse réussie renvoie le statut HTTP 201 avec les détails de la requête de publication de destination.

+++

## Gestion des erreurs d’API

Les points d’entrée de l’API Destination SDK suivent les principes généraux des messages d’erreur de l’API Experience Platform. Consultez les sections [Codes dʼétat d’API](../../../landing/troubleshooting.md#api-status-codes) et [Erreurs dʼen-tête de requête](../../../landing/troubleshooting.md#request-header-errors) dans le guide de dépannage de Platform.

## Étapes suivantes

Après la lecture de ce document, vous savez désormais comment envoyer une demande de publication pour votre destination. L’équipe dʼAdobe Experience Platform examinera votre demande de publication et vous recontactera dans un délai de cinq jours ouvrables.

---
title: Point d’entrée de l’API Content
description: Découvrez comment récupérer vos données d’accès à l’aide de l’API du Privacy Service.
role: Developer
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: ac54398ae8e9e06ea3581baf867ab1cf650042a2
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 5%

---

# Point d’entrée de contenu

Utilisez le point d’entrée `/content` pour récupérer en toute sécurité *les informations d’accès* (les informations qu’un titulaire de confidentialité peut légitimement demander à accéder) pour vos clients. L’URL de téléchargement fournie dans la réponse à une requête de GET `/jobs/{JOB_ID}` pointe vers un point d’entrée de service Adobe. Vous pouvez ensuite envoyer une requête de GET à `/jobs/:JOB_ID/content` pour renvoyer vos données client au format JSON. Cette méthode d’accès met en œuvre plusieurs couches d’authentification et de contrôle d’accès pour améliorer la sécurité.

Avant d’utiliser ce guide, reportez-vous au [ guide de prise en main ](./getting-started.md) pour plus d’informations sur les en-têtes d’authentification requis présentés dans l’exemple d’appel API ci-dessous.

>[!TIP]
>
>Si vous ne connaissez pas l’ID de tâche pour les informations d’accès dont vous avez besoin, appelez le point d’entrée `/jobs` et utilisez des paramètres de requête supplémentaires pour filtrer les résultats. Vous trouverez une liste complète des paramètres de requête disponibles dans le [guide des points d’entrée des tâches de confidentialité](./privacy-jobs.md).

## Récupération des informations de tâche relatives à la confidentialité

Pour récupérer des informations sur une tâche spécifique, telles que son statut de traitement actuel, incluez la `jobId` de cette tâche dans le chemin d’accès d’une requête de GET vers le point d’entrée `/jobs`.

**Format d’API**

```http
GET /jobs/{JOB_ID}
```

**Requête**

La requête suivante récupère les détails de la tâche dont `jobId` est fourni dans le chemin d’accès de requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie les détails de la tâche spécifiée.

>[!NOTE]
>
>Les tâches relatives à la confidentialité doivent avoir le statut `complete` pour contenir les `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Propriété | Description |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Identifiant unique de la tâche de confidentialité. |
| `requestId` | Identifiant unique de la requête spécifique envoyée au Privacy Service. |
| `userKey` | `userKey` est la valeur `key` que vous avez fournie lors de l’envoi de la demande d’accès à des informations personnelles. La valeur `key` est votre possibilité de fournir un identifiant qui vous semble logique pour le titulaire de données. Il s’agit généralement d’un identifiant unique créé par votre système pour suivre ce titulaire de données. CONSEIL : vous pouvez répertorier toutes les tâches de confidentialité actives et comparer vos `key` à chaque tâche. |
| `action` | Type d’action demandé. Les valeurs acceptées sont `access` et `delete`. |
| `status` | Statut actuel de la tâche de confidentialité. |
| `submittedBy` | Adresse e-mail de la personne qui a envoyé la tâche de confidentialité. |
| `createdDate` | Date et heure de création de la tâche de confidentialité. |
| `lastModifiedDate` | Date et heure de la dernière modification de la tâche de confidentialité. |
| `userIds` | Tableau contenant les identifiants d’utilisateur et les informations associées. |
| `userIds.namespace` | Espace de noms utilisé pour l’identifiant utilisateur. |
| `userIds.value` | Valeur réelle de l’identifiant utilisateur. |
| `userIds.type` | Type d’identifiant (par exemple `standard` ou `custom`). |
| `userIds.namespaceId` | Identifiant de l’espace de noms utilisé pour classer et gérer les identités utilisateur. |
| `userIds.isDeletedClientSide` | Valeur booléenne indiquant si l’identifiant a été supprimé côté client. |
| `productResponses` | Un tableau contenant les réponses de différents produits ou services liés à la tâche de confidentialité. |
| `productResponses.product` | Nom du produit ou du service utilisé pour obtenir des informations sur le titulaire de données. |
| `productResponses.retryCount` | Nombre de reprises de la demande. |
| `productResponses.processedDate` | Date et heure auxquelles la réponse du produit a été traitée. |
| `productResponses.productStatusResponse` | Un objet contenant le statut de la réponse du produit. |
| `productResponses.productStatusResponse.status` | Statut de la réponse du produit. |
| `downloadURL` | Cet attribut fournit un point d’entrée, que vous pouvez appeler pendant 60 jours après la fin de la tâche. Le statut du traitement doit être `complete` et le `action` doit être `access`. Dans le cas contraire, ce champ est absent. |
| `regulation` | Le cadre réglementaire dans lequel la demande d’accès à des informations personnelles est traitée, tel que `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`, etc. |

{style="table-layout:auto"}

## Récupération des informations d’accès client {#retrieve-access-data}

Pour obtenir les « informations d’accès » générées en réponse à la requête de votre titulaire de données, envoyez une requête de GET au point d’entrée `/jobs/{JOB_ID}/content`. La réponse est un fichier zip (*.zip) qui contient un dossier avec des sous-dossiers pour chaque produit qui contient des données sur le titulaire de données.

>[!TIP]
>
>Vous avez besoin d’un ID de tâche spécifique pour effectuer cette requête. Si vous devez récupérer l’identifiant de tâche spécifique, envoyez d’abord une requête de GET au point d’entrée `/jobs` et utilisez des paramètres de requête supplémentaires pour filtrer les résultats. Vous trouverez des informations détaillées, y compris les paramètres de requête autorisés, dans le guide [Privacy jobs endpoint guide](./privacy-jobs.md).

**Format d’API**

```http
GET /jobs/{JOB_ID}/content
```

**Requête**

La requête suivante renvoie « informations d’accès » pour l’ID de tâche fourni dans la requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Réponse**

La réponse est un fichier zip (*.zip). Les informations sont généralement renvoyées au format JSON, bien que cela ne puisse pas être garanti. Les données extraites peuvent être renvoyées dans n’importe quel format.


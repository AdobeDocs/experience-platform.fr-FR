---
title: Point de terminaison de l’API de contenu
description: Découvrez comment récupérer vos données d’accès à l’aide de l’API Privacy Service.
role: Developer
badgePrivateBeta: label="Beta privée" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c527771e051d39032642afae33945a45e5183a5f
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 6%

---

# Point de terminaison du contenu

>[!IMPORTANT]
>
>La variable `/content` Le point de terminaison est actuellement en version bêta et votre entreprise n’y a peut-être pas encore accès. Les fonctionnalités et la documentation sont susceptibles d’être modifiées.

<!-- Q) Should this be called 'access information' or 'customer content'? -->

Profitez d’une sécurité améliorée lors de la récupération des &quot;informations d’accès&quot; (les informations auxquelles un sujet de la confidentialité peut légitimement demander l’accès). URL de téléchargement fournie dans la réponse à une `/jobs/{JOB_ID}` La demande de GET pointe désormais vers un point d’entrée de service Adobe. Vous pouvez ensuite envoyer une demande de GET à `/jobs/:JOB_ID/content` pour renvoyer vos données client au format JSON. Cette méthode d’accès met en oeuvre plusieurs couches d’authentification et de contrôle d’accès afin d’améliorer la sécurité.

Avant d’utiliser ce guide, reportez-vous au [guide de prise en main](./getting-started.md) pour plus d’informations sur les en-têtes d’authentification requis présentés dans l’exemple d’appel API ci-dessous.

>[!TIP]
>
>Si vous ne connaissez pas actuellement l’ID de la tâche pour les informations d’accès dont vous avez besoin, appelez la fonction `/jobs`et utiliser des paramètres de requête supplémentaires pour filtrer les résultats. Vous trouverez une liste complète des paramètres de requête disponibles dans le [guide de point de terminaison des tâches de confidentialité](./privacy-jobs.md).

## Récupération des informations sur les tâches de confidentialité

Pour récupérer des informations sur une tâche spécifique, comme son état de traitement actuel, incluez la fonction `jobId` dans le chemin d’une requête de GET à la fonction `/jobs` point de terminaison .

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
>Les tâches de confidentialité doivent avoir la propriété `complete` pour contenir l’état `downloadUrl`.

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
    "downloadUrl":"https://platform-stage.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Propriété | Description |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Identifiant unique de la tâche de confidentialité. |
| `requestId` | Identifiant unique de la requête spécifique envoyée au Privacy Service. |
| `userKey` | `userKey` est la valeur `key` valeur que vous avez fournie lors de l’envoi de la demande d’accès à des informations personnelles. La variable `key` est l’opportunité que vous avez de fournir un identifiant du sujet de données qui vous semble logique. Il s’agit généralement d’un identifiant unique créé par votre système pour effectuer le suivi de ce sujet de données. CONSEIL : vous pouvez répertorier toutes les tâches de confidentialité actives et comparer vos `key` à chaque tâche. |
| `action` | Type d’action demandée. Les valeurs acceptées sont `access` et `delete`. |
| `status` | État actuel de la tâche de confidentialité. |
| `submittedBy` | Adresse électronique de la personne qui a envoyé la tâche de confidentialité. |
| `createdDate` | Date et heure de création de la tâche de confidentialité. |
| `lastModifiedDate` | Date et heure de la dernière modification de la tâche de confidentialité. |
| `userIds` | Tableau contenant les identifiants d’utilisateur et les informations connexes. |
| `userIds.namespace` | Espace de noms utilisé pour l’identifiant de l’utilisateur. |
| `userIds.value` | La valeur réelle de l’identifiant de l’utilisateur. |
| `userIds.type` | Le type d’identifiant (par exemple `standard` ou `custom`). |
| `userIds.namespaceId` | Identifiant de l’espace de noms utilisé pour classer et gérer les identités utilisateur. |
| `userIds.isDeletedClientSide` | Valeur booléenne indiquant si l’identifiant a été supprimé du côté client. |
| `productResponses` | Tableau contenant les réponses de différents produits ou services liés à la tâche de confidentialité. |
| `productResponses.product` | Nom du produit ou du service qui a été utilisé pour acquérir des informations sur le sujet des données. |
| `productResponses.retryCount` | Nombre de tentatives pour la requête. |
| `productResponses.processedDate` | Date et heure auxquelles la réponse du produit a été traitée. |
| `productResponses.productStatusResponse` | Objet contenant l’état de la réponse du produit. |
| `productResponses.productStatusResponse.status` | État de la réponse du produit. |
| `downloadURL` | Cet attribut fournit un point de terminaison qui peut être appelé pendant 60 jours après la fin de la tâche. L’état de la tâche doit être `complete` et la variable `action` must `access`. Sinon, ce champ est absent. |
| `regulation` | Cadre réglementaire dans lequel la demande d’accès à des informations personnelles est en cours de traitement, tel que `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`, etc. |

{style="table-layout:auto"}

## Récupération des informations d’accès client {#retrieve-access-data}

Pour obtenir les &quot;informations d’accès&quot; produites en réponse à la requête de votre sujet de données, envoyez une demande de GET à la variable `/jobs/{JOB_ID}/content` point de terminaison . La réponse est un fichier zip (*.zip) qui contient un dossier avec des sous-dossiers pour chaque produit contenant des données sur le sujet de données.

>[!TIP]
>
>Pour effectuer cette requête, vous avez besoin d’un identifiant de tâche spécifique. Si vous devez récupérer l’identifiant de tâche spécifique, envoyez d’abord une demande de GET à la fonction `/jobs` et utiliser des paramètres de requête supplémentaires pour filtrer les résultats. Vous trouverez des informations détaillées, notamment les paramètres de requête autorisés, dans la section [guide de point de terminaison des tâches de confidentialité](./privacy-jobs.md).

**Format d’API**

```http
GET /jobs/{JOB_ID}/content
```

**Requête**

La requête suivante renvoie &quot;informations d’accès&quot; pour l’ID de tâche fourni dans la requête.

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

<!-- ## Constraints {#constraints}

During this private beta, the following constraints apply when using the `/content` endpoint:

- The new `/content` download URL is only available in STAGE environments. It is not yet available in PROD environments
- The `downloadUrl` should not be present in the JSON response unless the job has a `complete` status. Within the beta, the `downloadUrl` appears before a privacy job is complete.
- The `downloadUrl` is also currently provided for `delete` jobs (which should never have a download URL). -->

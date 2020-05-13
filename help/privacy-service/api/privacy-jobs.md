---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tâches
topic: developer guide
translation-type: tm+mt
source-git-commit: a3178ab54a7ab5eacd6c5f605b8bd894779f9e85
workflow-type: tm+mt
source-wordcount: '1669'
ht-degree: 2%

---


# Tâches de confidentialité

Les sections suivantes décrivent les appels que vous pouvez effectuer à l’aide du `/jobs` point de terminaison dans l’API de Privacy Service. Chaque appel comprend le format général de l’API, un exemple de requête indiquant les en-têtes requis et un exemple de réponse.

## Création d’une tâche de confidentialité {#create-job}

Avant de créer une nouvelle demande de travail, vous devez d&#39;abord collecter des informations d&#39;identification sur les personnes dont vous voulez accéder aux données, les supprimer ou les opt-out de vente. Une fois que vous disposez des données requises, elles doivent être fournies dans la charge utile d’une requête POST au point de terminaison racine.

>[!NOTE] Les applications Adobe Experience Cloud compatibles utilisent des valeurs différentes pour identifier les personnes concernées. Consultez le guide sur les applications [](../experience-cloud-apps.md) Privacy Service et Experience Cloud pour en savoir plus sur les identifiants requis pour vos applications.

L’API Privacy Service prend en charge deux types de demandes d’emploi pour les données personnelles :

* [Accès et/ou suppression](#access-delete): Accéder (lire) ou supprimer des données personnelles.
* [Opt-out de vente](#opt-out): Marquer que les données personnelles ne doivent pas être vendues.

>[!IMPORTANT] Bien que les demandes d’accès et de suppression puissent être combinées en un seul appel d’API, les demandes d’exclusion doivent être effectuées séparément.

### Créer une tâche d’accès/de suppression {#access-delete}

Cette section explique comment effectuer une demande d’accès/de suppression de travail à l’aide de l’API.

**Format d’API**

```http
POST /jobs
```

**Requête**

La demande suivante crée une nouvelle demande de travail, configurée par les attributs fournis dans la charge utile, comme décrit ci-dessous.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Propriété | Description |
| --- | --- |
| `companyContexts` **(Obligatoire)** | Tableau contenant des informations d&#39;authentification pour votre organisation. Chaque identifiant répertorié comprend les attributs suivants : <ul><li>`namespace`: espace de nommage d’un identifiant.</li><li>`value`: Valeur de l’identifiant.</li></ul>Il est **nécessaire** qu’un des identifiants utilise `imsOrgId` comme son `namespace`nom, avec son `value` identifiant unique pour votre organisation IMS. <br/><br/>D’autres identifiants peuvent être des qualificatifs de société spécifiques au produit (par exemple `Campaign`), qui identifient une intégration à une application Adobe appartenant à votre organisation. Les valeurs potentielles sont les noms de compte, les codes client, les ID de client ou d’autres identifiants d’application. |
| `users` **(Obligatoire)** | Tableau contenant une collection d&#39;au moins un utilisateur dont vous souhaitez accéder ou supprimer les informations. Un maximum de 1 000 identifiants d’utilisateur peuvent être fournis dans une seule requête. Chaque objet utilisateur contient les informations suivantes : <ul><li>`key`: Identificateur d’un utilisateur utilisé pour définir les ID de tâche distincts dans les données de réponse. Il est recommandé de choisir une chaîne unique et facilement identifiable pour cette valeur afin qu’elle puisse être facilement référencée ou consultée ultérieurement.</li><li>`action`: Tableau qui liste les actions souhaitées pour exécuter les données de l&#39;utilisateur. En fonction des actions que vous souhaitez entreprendre, ce tableau doit inclure `access`, `delete`ou les deux.</li><li>`userIDs`: Ensemble d’identités pour l’utilisateur. Le nombre d’identités qu’un utilisateur peut posséder est limité à neuf. Chaque identité se compose d&#39;un `namespace`, d&#39;un `value`et d&#39;un qualificatif d&#39;espace de nommage (`type`). Consultez l’ [annexe](appendix.md) pour plus de détails sur ces propriétés requises.</li></ul> Pour une explication plus détaillée de `users` et `userIDs`, consultez le guide [de](../troubleshooting-guide.md#user-ids)dépannage. |
| `include` **(Obligatoire)** | Tableau de produits Adobe à inclure dans votre traitement. Si cette valeur est manquante ou est vide, la demande est rejetée. Incluez uniquement les produits avec lesquels votre entreprise est intégrée. Pour plus d’informations, consultez la section relative aux valeurs [de produit](appendix.md) acceptées dans l’annexe. |
| `expandIDs` | Propriété facultative qui, lorsqu’elle est définie sur `true`, représente une optimisation pour le traitement des ID dans les applications (actuellement uniquement prise en charge par Analytics). If omitted, this value defaults to `false`. |
| `priority` | Propriété facultative utilisée par Adobe Analytics qui définit la priorité des demandes de traitement. Les valeurs acceptées sont `normal` et `low`. Si `priority` est omis, le comportement par défaut est `normal`. |
| `analyticsDeleteMethod` | Propriété facultative qui spécifie comment Adobe Analytics doit traiter les données personnelles. Deux valeurs possibles sont acceptées pour cet attribut : <ul><li>`anonymize`: Toutes les données référencées par la collection donnée d’ID d’utilisateur sont rendues anonymes. Si `analyticsDeleteMethod` cette option est omise, il s’agit du comportement par défaut.</li><li>`purge`: Toutes les données sont complètement supprimées.</li></ul> |
| `regulation` **(Obligatoire)** | Le règlement de la demande. Doit être l’une des trois valeurs suivantes : <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Réponse**

Une réponse positive renvoie les détails des tâches nouvellement créées.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076be029f3",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "access"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd023j1",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "delete"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 3
}
```

| Propriété | Description |
| --- | --- |
| `jobId` | ID généré par le système en lecture seule pour une tâche. Cette valeur est utilisée à l’étape suivante de la recherche d’une tâche spécifique. |

Une fois que vous avez soumis la demande de travail avec succès, vous pouvez passer à l’étape suivante de [vérification de l’état](#check-status)de la tâche.

### Créer une tâche d’exclusion de la vente {#opt-out}

Cette section explique comment effectuer une demande de travail d’exclusion de la vente à l’aide de l’API.

**Format d’API**

```http
POST /jobs
```

**Requête**

La demande suivante crée une nouvelle demande de travail, configurée par les attributs fournis dans la charge utile, comme décrit ci-dessous.

```shell
curl -X POST \
  https://platform.adobe.io/data/privacy/gdpr/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "DavidSmith",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "443636576799758681021090721276",
            "isDeletedClientSide": false
          }
        ]
      },
      {
        "key": "user12345",
        "action": ["opt-out-of-sale"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "loyaltyAccount",
            "value": "12AD45FE30R29",
            "type": "integrationCode"
          }
        ]
      }
    ],
    "include": ["Analytics", "AudienceManager"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

| Propriété | Description |
| --- | --- |
| `companyContexts` **(Obligatoire)** | Tableau contenant des informations d&#39;authentification pour votre organisation. Chaque identifiant répertorié comprend les attributs suivants : <ul><li>`namespace`: espace de nommage d’un identifiant.</li><li>`value`: Valeur de l’identifiant.</li></ul>Il est **nécessaire** qu’un des identifiants utilise `imsOrgId` comme son `namespace`nom, avec son `value` identifiant unique pour votre organisation IMS. <br/><br/>D’autres identifiants peuvent être des qualificatifs de société spécifiques au produit (par exemple `Campaign`), qui identifient une intégration à une application Adobe appartenant à votre organisation. Les valeurs potentielles sont les noms de compte, les codes client, les ID de client ou d’autres identifiants d’application. |
| `users` **(Obligatoire)** | Tableau contenant une collection d&#39;au moins un utilisateur dont vous souhaitez accéder ou supprimer les informations. Un maximum de 1 000 identifiants d’utilisateur peuvent être fournis dans une seule requête. Chaque objet utilisateur contient les informations suivantes : <ul><li>`key`: Identificateur d’un utilisateur utilisé pour définir les ID de tâche distincts dans les données de réponse. Il est recommandé de choisir une chaîne unique et facilement identifiable pour cette valeur afin qu’elle puisse être facilement référencée ou consultée ultérieurement.</li><li>`action`: Tableau qui liste les actions souhaitées pour exécuter les données. Pour les demandes d&#39;exclusion de la vente, le tableau ne doit contenir que la valeur `opt-out-of-sale`.</li><li>`userIDs`: Ensemble d’identités pour l’utilisateur. Le nombre d’identités qu’un utilisateur peut posséder est limité à neuf. Chaque identité se compose d&#39;un `namespace`, d&#39;un `value`et d&#39;un qualificatif d&#39;espace de nommage (`type`). Consultez l’ [annexe](appendix.md) pour plus de détails sur ces propriétés requises.</li></ul> Pour une explication plus détaillée de `users` et `userIDs`, consultez le guide [de](../troubleshooting-guide.md#user-ids)dépannage. |
| `include` **(Obligatoire)** | Tableau de produits Adobe à inclure dans votre traitement. Si cette valeur est manquante ou est vide, la demande est rejetée. Incluez uniquement les produits avec lesquels votre entreprise est intégrée. Pour plus d’informations, consultez la section relative aux valeurs [de produit](appendix.md) acceptées dans l’annexe. |
| `expandIDs` | Propriété facultative qui, lorsqu’elle est définie sur `true`, représente une optimisation pour le traitement des ID dans les applications (actuellement uniquement prise en charge par Analytics). If omitted, this value defaults to `false`. |
| `priority` | Propriété facultative utilisée par Adobe Analytics qui définit la priorité des demandes de traitement. Les valeurs acceptées sont `normal` et `low`. Si `priority` est omis, le comportement par défaut est `normal`. |
| `analyticsDeleteMethod` | Propriété facultative qui spécifie comment Adobe Analytics doit traiter les données personnelles. Deux valeurs possibles sont acceptées pour cet attribut : <ul><li>`anonymize`: Toutes les données référencées par la collection donnée d’ID d’utilisateur sont rendues anonymes. Si `analyticsDeleteMethod` cette option est omise, il s’agit du comportement par défaut.</li><li>`purge`: Toutes les données sont complètement supprimées.</li></ul> |
| `regulation` **(Obligatoire)** | Le règlement de la demande. Doit être l’une des trois valeurs suivantes : <ul><li>gdpr</li><li>ccpa</li><li>pdpa_tha</li></ul> |

**Réponse**

Une réponse positive renvoie les détails des tâches nouvellement créées.

```json
{
    "jobs": [
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bd9vjs0",
            "customer": {
                "user": {
                    "key": "DavidSmith",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        },
        {
            "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076bes0ewj2",
            "customer": {
                "user": {
                    "key": "user12345",
                    "action": [
                        "opt-out-of-sale"
                    ]
                }
            }
        }
    ],
    "requestStatus": 1,
    "totalRecords": 2
}
```

| Propriété | Description |
| --- | --- |
| `jobId` | ID généré par le système en lecture seule pour une tâche. Cette valeur est utilisée pour rechercher une tâche spécifique à l’étape suivante. |

Une fois que vous avez soumis la demande de travail avec succès, vous pouvez passer à l’étape suivante de vérification de l’état de la tâche.

## Vérifier l&#39;état d&#39;une tâche {#check-status}

En utilisant l’une des `jobId` valeurs renvoyées à l’étape précédente, vous pouvez récupérer des informations sur cette tâche, telles que son état de traitement actuel.

>[!IMPORTANT] Les données relatives aux tâches précédemment créées ne peuvent être récupérées que dans les 30 jours suivant la date de fin de la tâche.

**Format d’API**

```http
GET /jobs/{JOB_ID}
```

| Paramètre | Description |
| --- | --- |
| `{JOB_ID}` | ID de la tâche à rechercher, renvoyé sous `jobId` dans la réponse de l’étape [](#create-job)précédente. |

**Requête**

La requête suivante récupère les détails de la tâche dont `jobId` le chemin d&#39;accès est fourni.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Une réponse réussie renvoie les détails de la tâche spécifiée.

```json
{
    "jobId": "527ef92d-6cd9-45cc-9bf1-477cfa1e2ca2",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "error",
    "submittedBy": "02b38adf-6573-401e-b4cc-6b08dbc0e61c@techacct.adobe.com",
    "createdDate": "10/02/2019 08:25 PM GMT",
    "lastModifiedDate": "10/02/2019 08:25 PM GMT",
    "userIds": [
        {
            "namespace": "email",
            "value": "dsmith@acme.com",
            "type": "standard",
            "namespaceId": 6,
            "isDeletedClientSide": false
        },
        {
            "namespace": "ECID",
            "value": "1123A4D5690B32A",
            "type": "standard",
            "namespaceId": 4,
            "isDeletedClientSide": false
        }
    ],
    "productResponses": [
        {
            "product": "Analytics",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "submitted",
                "message": "processing"
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Propriété | Description |
| --- | --- |
| `productStatusResponse` | Statut actuel de la tâche. Le tableau ci-dessous fournit des détails sur chaque état possible. |
| `downloadURL` | Si le statut de la tâche est `complete`défini, cet attribut fournit une URL pour télécharger les résultats de la tâche sous la forme d’un fichier ZIP. Ce fichier peut être téléchargé pendant 60 jours après la fin de la tâche. |

### Réponses d’état de la tâche

Le tableau suivant liste les différents statuts de travail possibles et leur signification correspondante :

| Code de statut | Message d&#39;état | Signification |
| ----------- | -------------- | -------- |
| 1 | Complete | La tâche est terminée et (si nécessaire) des fichiers sont téléchargés à partir de chaque application. |
| 2 | Le traitement | Les demandes ont reconnu la tâche et sont en cours de traitement. |
| 3 | Envoyé | L&#39;emploi est soumis à chaque demande applicable. |
| 4 | Erreur | Une erreur s&#39;est produite dans le traitement de la tâche. Des informations plus précises peuvent être obtenues en récupérant les détails de la tâche. |

>[!NOTE] Une tâche envoyée peut rester dans un état de traitement si elle a une tâche enfant à charge qui est toujours en cours de traitement.

## Liste de toutes les tâches

Vous pouvez vue une liste de toutes les demandes de travaux disponibles au sein de votre organisation en envoyant une demande GET au point de terminaison racine (`/`).

**Format d’API**

Ce format de requête utilise un paramètre de `regulation` requête sur le point de terminaison racine (`/`), de sorte qu’il commence par un point d’interrogation (`?`) comme illustré ci-dessous. La réponse est paginée, ce qui vous permet d&#39;utiliser d&#39;autres paramètres de requête (`page` et `size`) pour filtrer la réponse. Vous pouvez séparer plusieurs paramètres à l’aide d’esperluettes (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Paramètre | Description |
| --- | --- |
| `{REGULATION}` | Type de réglementation à requête. Les valeurs acceptées sont `gdpr`, `ccpa`et `pdpa_tha`. |
| `{PAGE}` | Page de données à afficher, à l’aide d’une numérotation basée sur 0. La valeur par défaut est de `0` |
| `{SIZE}` | Nombre de résultats à afficher sur chaque page. La valeur par défaut est `1` et la valeur maximale est `100`. Si le nombre maximal est dépassé, l’API renvoie une erreur de code 400. |

**Requête**

La requête suivante récupère une liste paginée de toutes les tâches d’une organisation IMS, à partir de la troisième page avec un format de page de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Une réponse positive renvoie une liste de tâches, chaque tâche contenant des détails tels que son `jobId`nom. Dans cet exemple, la réponse contiendrait une liste de 50 tâches, en commençant par la troisième page de résultats.

### Accès aux pages suivantes

Pour récupérer l&#39;ensemble de résultats suivant dans une réponse paginée, vous devez effectuer un autre appel d&#39;API vers le même point de terminaison tout en augmentant le paramètre de `page` requête de 1.

## Étapes suivantes

Vous savez maintenant comment créer et contrôler des tâches de confidentialité à l’aide de l’API Privacy Service. Pour plus d’informations sur la façon d’exécuter les mêmes tâches à l’aide de l’interface utilisateur, voir la présentation [de l’interface utilisateur de](../ui/overview.md)Privacy Service.

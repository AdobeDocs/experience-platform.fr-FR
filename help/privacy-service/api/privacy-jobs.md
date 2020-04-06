---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tâches
topic: developer guide
translation-type: tm+mt
source-git-commit: cde7acc2fd112b9a5d0b86b40b3bc712c6505064

---


# Tâches de confidentialité

Les sections suivantes passent en revue les appels que vous pouvez effectuer à l’aide du point de terminaison racine (`/`) dans l’API de Privacy Service. Chaque appel comprend le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

## Création d’une tâche de confidentialité

Avant de créer une nouvelle demande de travail, vous devez d’abord collecter des informations d’identification sur les personnes de données dont vous souhaitez accéder, supprimer ou opt-out de vente. Une fois que vous disposez des données requises, elles doivent être fournies dans la charge utile d’une requête POST au point de terminaison racine.

>[!NOTE] Les applications Adobe Experience Cloud compatibles utilisent des valeurs différentes pour identifier les personnes de données. Pour plus d’informations sur les identifiants requis pour vos applications, consultez le guide sur les applications [](../experience-cloud-apps.md) Privacy Service et Experience Cloud.

L’API Privacy Service prend en charge deux types de demandes de tâches pour les données personnelles :

* [Accès et/ou suppression](#access-delete): Accéder (lire) ou supprimer des données personnelles.
* [Opt-out de vente](#opt-out): Marquez que les données personnelles ne doivent pas être vendues.

>[!IMPORTANT] Bien que les demandes d’accès et de suppression puissent être combinées en tant qu’appel d’API unique, les demandes d’exclusion doivent être effectuées séparément.

### Création d’une tâche d’accès/de suppression {#access-delete}

Cette section explique comment effectuer une demande d’accès/de suppression de tâche à l’aide de l’API.

**Format API**

```http
POST /
```

**Requête**

La requête suivante crée une nouvelle requête de tâche, configurée par les attributs fournis dans la charge utile, comme décrit ci-dessous.

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
| `companyContexts` **(Obligatoire)** | Tableau contenant des informations d&#39;authentification pour votre entreprise. Chaque identifiant répertorié comprend les attributs suivants : <ul><li>`namespace`:  d’un identifiant.</li><li>`value`: Valeur de l’identifiant.</li></ul>Il est **obligatoire** qu’un des identifiants utilise `imsOrgId` comme son `namespace`, avec son `value` identifiant unique pour votre organisation IMS. <br/><br/>Les identifiants supplémentaires peuvent être des qualificateurs de spécifiques au produit (par exemple `Campaign`), qui identifient une intégration à une application Adobe appartenant à votre organisation. Les valeurs potentielles sont les noms de compte, les codes client, les ID de client ou d’autres identifiants d’application. |
| `users` **(Obligatoire)** | Tableau contenant une collection d’au moins un utilisateur dont vous souhaitez accéder ou supprimer les informations. Un maximum de 1 000 identifiants utilisateur peuvent être fournis dans une seule requête. Chaque objet utilisateur contient les informations suivantes : <ul><li>`key`: Identifiant utilisé pour qualifier les ID de tâche distincts dans les données de réponse. Il est recommandé de choisir une chaîne unique facilement identifiable pour cette valeur afin qu’elle puisse être facilement référencée ou consultée ultérieurement.</li><li>`action`: Tableau  actions souhaitées pour traiter les données. Selon les actions que vous souhaitez effectuer, ce tableau doit inclure `access`, `delete`ou les deux.</li><li>`userIDs`: Collection d’identités pour un utilisateur particulier. Le nombre d’identités qu’un utilisateur peut posséder est limité à neuf. Chaque identité se compose d’un `namespace`, d’un `value`et d’un  qualificatif de  (`type`). Voir l’ [annexe](appendix.md) pour plus d’informations sur ces propriétés requises.</li></ul> |
| `include` **(Obligatoire)** | Tableau de produits Adobe à inclure dans votre traitement. Si cette valeur est manquante ou vide, la requête est rejetée. Incluez uniquement les produits avec lesquels votre entreprise est intégrée. Pour plus d’informations, consultez la section sur les valeurs [de produit](appendix.md) acceptées dans l’annexe. |
| `expandIDs` | Propriété facultative qui, lorsqu’elle est définie sur `true`, représente une optimisation pour le traitement des ID dans les applications (actuellement uniquement prise en charge par Analytics). If omitted, this value defaults to `false`. |
| `priority` | Propriété facultative utilisée par Adobe Analytics qui définit la priorité pour le traitement des requêtes. Les valeurs acceptées sont `normal` et `low`. Si `priority` elle est omise, le comportement par défaut est `normal`. |
| `analyticsDeleteMethod` | Propriété facultative qui spécifie la manière dont Adobe Analytics doit traiter les données personnelles. Deux valeurs possibles sont acceptées pour cet attribut : <ul><li>`anonymize`: Toutes les données référencées par la collection donnée d’ID d’utilisateur sont rendues anonymes. S’ `analyticsDeleteMethod` il est omis, il s’agit du comportement par défaut.</li><li>`purge`: Toutes les données sont complètement supprimées.</li></ul> |
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

Une fois que vous avez envoyé la demande de tâche avec succès, vous pouvez passer à l’étape suivante de [vérification de l’état](#check-the-status-of-a-job)de la tâche.

### Création d’une tâche d’exclusion de la vente {#opt-out}

Cette section explique comment effectuer une demande de travail d’exclusion de la vente à l’aide de l’API.

**Format API**

```http
POST /
```

**Requête**

La requête suivante crée une nouvelle requête de tâche, configurée par les attributs fournis dans la charge utile, comme décrit ci-dessous.

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
| `companyContexts` **(Obligatoire)** | Tableau contenant des informations d&#39;authentification pour votre entreprise. Chaque identifiant répertorié comprend les attributs suivants : <ul><li>`namespace`:  d’un identifiant.</li><li>`value`: Valeur de l’identifiant.</li></ul>Il est **obligatoire** qu’un des identifiants utilise `imsOrgId` comme son `namespace`, avec son `value` identifiant unique pour votre organisation IMS. <br/><br/>Les identifiants supplémentaires peuvent être des qualificateurs de spécifiques au produit (par exemple `Campaign`), qui identifient une intégration à une application Adobe appartenant à votre organisation. Les valeurs potentielles sont les noms de compte, les codes client, les ID de client ou d’autres identifiants d’application. |
| `users` **(Obligatoire)** | Tableau contenant une collection d’au moins un utilisateur dont vous souhaitez accéder ou supprimer les informations. Un maximum de 1 000 identifiants utilisateur peuvent être fournis dans une seule requête. Chaque objet utilisateur contient les informations suivantes : <ul><li>`key`: Identifiant utilisé pour qualifier les ID de tâche distincts dans les données de réponse. Il est recommandé de choisir une chaîne unique facilement identifiable pour cette valeur afin qu’elle puisse être facilement référencée ou consultée ultérieurement.</li><li>`action`: Tableau  actions souhaitées pour traiter les données. Pour les demandes d’exclusion de la vente, le tableau ne doit contenir que la valeur `opt-out-of-sale`.</li><li>`userIDs`: Collection d’identités pour un utilisateur particulier. Le nombre d’identités qu’un utilisateur peut posséder est limité à neuf. Chaque identité se compose d’un `namespace`, d’un `value`et d’un  qualificatif de  (`type`). Voir l’ [annexe](appendix.md) pour plus d’informations sur ces propriétés requises.</li></ul> |
| `include` **(Obligatoire)** | Tableau de produits Adobe à inclure dans votre traitement. Si cette valeur est manquante ou vide, la requête est rejetée. Incluez uniquement les produits avec lesquels votre entreprise est intégrée. Pour plus d’informations, consultez la section sur les valeurs [de produit](appendix.md) acceptées dans l’annexe. |
| `expandIDs` | Propriété facultative qui, lorsqu’elle est définie sur `true`, représente une optimisation pour le traitement des ID dans les applications (actuellement uniquement prise en charge par Analytics). If omitted, this value defaults to `false`. |
| `priority` | Propriété facultative utilisée par Adobe Analytics qui définit la priorité pour le traitement des requêtes. Les valeurs acceptées sont `normal` et `low`. Si `priority` elle est omise, le comportement par défaut est `normal`. |
| `analyticsDeleteMethod` | Propriété facultative qui spécifie la manière dont Adobe Analytics doit traiter les données personnelles. Deux valeurs possibles sont acceptées pour cet attribut : <ul><li>`anonymize`: Toutes les données référencées par la collection donnée d’ID d’utilisateur sont rendues anonymes. S’ `analyticsDeleteMethod` il est omis, il s’agit du comportement par défaut.</li><li>`purge`: Toutes les données sont complètement supprimées.</li></ul> |
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

Une fois que vous avez bien envoyé la demande de tâche, vous pouvez passer à l’étape suivante de vérification de l’état de la tâche.

## Vérification de l’état d’une tâche

A l’aide de l’une des `jobId` valeurs renvoyées à l’étape précédente, vous pouvez récupérer des informations sur cette tâche, telles que son état de traitement actuel.

>[!IMPORTANT] Les données relatives aux tâches précédemment créées ne peuvent être récupérées que dans les 30 jours suivant la date d’achèvement de la tâche.

**Format API**

```http
GET /{JOB_ID}
```

| Paramètre | Description |
| --- | --- |
| `{JOB_ID}` | ID de la tâche que vous souhaitez rechercher, renvoyé sous `jobId` dans la réponse de l’étape [](#create-a-job-request)précédente. |

**Requête**

La requête suivante récupère les détails de la tâche dont `jobId` le chemin d’accès est fourni.

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
| `downloadURL` | Si l’état de la tâche est `complete`, cet attribut fournit une URL pour télécharger les résultats de la tâche sous forme de fichier ZIP. Ce fichier peut être téléchargé pendant 60 jours après la fin de la tâche. |

### Réponses d’état de tâche

Le tableau suivant  les différents états possibles des tâches et leur signification correspondante :

| Code d’état | Message d’état | Signification |
| ----------- | -------------- | -------- |
| 1 | Terminer | La tâche est terminée et (si nécessaire) les fichiers sont téléchargés à partir de chaque application. |
| 2 | Le traitement | Les demandes ont reconnu la tâche et sont en cours de traitement. |
| 3 | Envoyé | La tâche est soumise à chaque demande applicable. |
| 4 | Erreur | Une erreur s’est produite lors du traitement de la tâche. Des informations plus spécifiques peuvent être obtenues en récupérant les détails de la tâche. |

>[!NOTE] Une tâche envoyée peut rester dans un état de traitement si elle a une tâche enfant à charge en cours de traitement.

##  toutes les tâches

Vous pouvez  un de toutes les demandes de tâche disponibles au sein de votre organisation en envoyant une requête GET au point de terminaison racine (`/`).

**Format API**

Ce format de requête utilise un paramètre `regulation` sur le point de terminaison racine (`/`). Il commence donc par un point d’interrogation (`?`) comme illustré ci-dessous. La réponse est paginée, ce qui vous permet d’utiliser d’autres paramètres de  de (`page` et `size`) pour filtrer la réponse. Vous pouvez séparer plusieurs paramètres à l’aide d’esperluettes (`&`).

```http
GET ?regulation={REGULATION}
GET ?regulation={REGULATION}&page={PAGE}
GET ?regulation={REGULATION}&size={SIZE}
GET ?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Paramètre | Description |
| --- | --- |
| `{REGULATION}` | Le type de réglementation à  pour lequel vous voulez. Les valeurs acceptées sont `gdpr`, `ccpa`et `pdpa_tha`. |
| `{PAGE}` | Page de données à afficher, à l’aide d’une numérotation basée sur 0. La valeur par défaut est de `0` |
| `{SIZE}` | Nombre de résultats à afficher sur chaque page. La valeur par défaut est `1` et la valeur maximale est `100`. Si le nombre maximal est dépassé, l’API renvoie une erreur de code 400. |

**Requête**

La requête suivante récupère un  paginé de toutes les tâches d’une organisation IMS, à partir de la troisième page avec un format de page de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Une réponse réussie renvoie un  de tâches, chaque tâche contenant des détails tels que son `jobId`nom. Dans cet exemple, la réponse contient un de 50 tâches, à partir de la troisième page de résultats.

### Accès aux pages suivantes

Pour récupérer l’ensemble de résultats suivant dans une réponse paginée, vous devez effectuer un autre appel d’API vers le même point de terminaison tout en augmentant le paramètre  `page` de 1.

## Étapes suivantes

Vous savez maintenant comment créer et surveiller des tâches de confidentialité à l’aide de l’API de Privacy Service. Pour plus d’informations sur la manière d’effectuer le même à l’aide de l’interface utilisateur, voir la présentation [de l’interface utilisateur de](../ui/overview.md)Privacy Service.

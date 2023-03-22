---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point de terminaison de l’API Privacy Jobs
description: Découvrez comment gérer les tâches de confidentialité pour les applications Experience Cloud à l’aide de l’API Privacy Service.
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: 21347074ed6160511888d4b543133dfd1ec4d35c
workflow-type: tm+mt
source-wordcount: '1549'
ht-degree: 59%

---

# Point de terminaison des tâches de confidentialité

Ce document explique comment utiliser les tâches de confidentialité à l’aide d’appels API. Plus précisément, il couvre l’utilisation de la variable `/job` du point de terminaison [!DNL Privacy Service] API. Avant de lire ce guide, reportez-vous à la section [guide de prise en main](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels à l’API, notamment les en-têtes requis et la lecture d’exemples d’appels API.

>[!NOTE]
>
>Si vous essayez de gérer les demandes de consentement ou d’exclusion des clients, reportez-vous à la section [guide de point de fin de consentement](./consent.md).

## Liste de toutes les tâches {#list}

Vous pouvez afficher une liste de toutes les tâches de confidentialité disponibles au sein de votre organisation en adressant une demande de GET à la fonction `/jobs` point de terminaison .

**Format d’API**

Ce format de requête utilise une `regulation` le paramètre de requête sur le `/jobs` point de fin, par conséquent, il commence par un point d’interrogation (`?`), comme illustré ci-dessous. La réponse est paginée, ce qui vous permet d’utiliser d’autres paramètres de requête (`page` et `size`) pour filtrer la réponse. Vous pouvez séparer plusieurs paramètres à l’aide d’esperluettes (`&`).

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
```

| Paramètre | Description |
| --- | --- |
| `{REGULATION}` | Le type de réglementation pour lequel vous souhaitez effectuer une requête. Les valeurs acceptées sont les suivantes : <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consultez la présentation sur [réglementations prises en charge](../regulations/overview.md) pour plus d’informations sur les réglementations de confidentialité que représentent les valeurs ci-dessus. |
| `{PAGE}` | La page de données à afficher à l’aide d’une numérotation basée sur 0. La valeur par défaut est de `0`. |
| `{SIZE}` | Le nombre de résultats à afficher sur chaque page. `1` est la valeur par défaut et `100` est le maximum. Dépasser le maximum entraîne le code d’erreur 400 dans l’API. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une liste paginée de toutes les tâches d’une organisation IMS, en commençant à la troisième page avec un format de page de 50.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs?regulation=gdpr&page=2&size=50 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie une liste des tâches dont chaque tâche contient des détails comme son `jobId`. Dans cet exemple, la réponse contiendrait une liste de 50 tâches commençant sur la troisième page des résultats.

### Accès aux pages suivantes

Pour récupérer le jeu suivant de résultats dans une réponse paginée, vous devez effectuer un autre appel API vers le même point de terminaison tout en augmentant le paramètre de requête `page` de 1.

## Création d’une tâche de confidentialité {#create-job}

>[!IMPORTANT]
>
>Le Privacy Service est destiné uniquement aux demandes relatives aux titulaires de données et aux droits des consommateurs. Toute autre utilisation de Privacy Service pour le nettoyage ou la maintenance des données n’est ni prise en charge ni autorisée. L&#39;Adobe a l&#39;obligation légale de les remplir dans les délais impartis. Par conséquent, le test de chargement sur Privacy Service n’est pas autorisé, car il s’agit d’un environnement de production uniquement et crée un journal inutile de demandes d’accès à des informations personnelles valides.
>
>Une limite de chargement quotidienne stricte est maintenant en place pour prévenir les abus du service. Les utilisateurs qui abusent du système verront leur accès désactivé. Une réunion ultérieure sera ensuite organisée avec eux afin d&#39;aborder leurs actions et de discuter de l&#39;utilisation acceptable pour le Privacy Service.

Avant de créer une nouvelle requête de tâche, vous devez d’abord collecter des informations d’identification concernant les titulaires des données auxquelles vous souhaitez accéder, supprimer ou exclure de la vente. Une fois que vous disposez des données requises, elles doivent être fournies dans le payload d’une requête de POST à la variable `/jobs` point de terminaison .

>[!NOTE]
>
>Les applications Adobe Experience Cloud compatibles utilisent des valeurs d’identification des titulaires de données différentes. Pour plus d’informations sur les identifiants requis pour votre ou vos applications, consultez le guide sur [les applications Privacy Service et Experience Cloud](../experience-cloud-apps.md). Pour obtenir des instructions plus générales sur la détermination des ID à envoyer [!DNL Privacy Service], voir le document sur [données d’identité dans les demandes d’accès à des informations personnelles](../identity-data.md).

Le [!DNL Privacy Service] L’API prend en charge deux types de requêtes de tâche pour les données personnelles :

* [Accès et/ou suppression](#access-delete) : accédez (lisez) ou supprimez les données personnelles.
* [Exclusion de la vente](#opt-out) : marquez les données personnelles comme ne pouvant pas être vendues.

>[!IMPORTANT]
>
>Bien qu’il soit possible d’associer les requêtes d’accès et de suppression dans un appel API unique, les demandes d’exclusion doivent être effectuées séparément.

### Création d’une tâche d’accès ou de suppression {#access-delete}

Cette section explique comment effectuer une requête de tâche d’accès ou de suppression à l’aide de l’API.

**Format d’API**

```http
POST /jobs
```

**Requête**

La requête suivante crée une nouvelle requête de tâche configurée par les attributs fournis dans le payload comme décrit ci-dessous.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["Analytics", "AudienceManager","profileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Propriété | Description |
| --- | --- |
| `companyContexts` **(Obligatoire)** | Un tableau contenant des informations d’authentification pour votre organisation. Chaque identifiant répertorié inclut les attributs suivants : <ul><li>`namespace` : l’espace de noms d’un identifiant.</li><li>`value` : la valeur de l’identifiant.</li></ul>Il est **obligatoire** que l’un des identifiants utilise `imsOrgId` en tant que `namespace` avec son `value` contenant l’ID unique pour votre organisation IMS. <br/><br/>Les identifiants supplémentaires peuvent être des qualificateurs d’entreprise spécifiques aux produits (par exemple, `Campaign`) qui identifient une intégration avec une application Adobe appartenant à votre organisation. Les valeurs potentielles incluent des noms de compte, des codes client, des identifiants du client ou d’autres identifiants d’application. |
| `users` **(Obligatoire)** | Un tableau contenant une collection d’au moins un utilisateur pour lequel vous souhaitez accéder aux informations ou les supprimer. Vous pouvez fournir un maximum de 1 000 identifiants d’utilisateur dans une seule requête. Chaque objet d’utilisateur contient les informations suivantes : <ul><li>`key` : un identifiant pour un utilisateur utilisé pour exécuter les identifiants de tâches distincts dans les données de réponse. Nous vous recommandons de choisir une chaîne unique et facilement identifiable pour cette valeur afin de pouvoir facilement la référencer ou la rechercher ultérieurement.</li><li>`action` : un tableau répertoriant les actions souhaitées pouvant être effectuées sur les données de l’utilisateur. En fonction des actions que vous souhaitez entreprendre, ce tableau peut inclure `access`, `delete` ou les deux.</li><li>`userIDs` : une collection d’identités pour cet utilisateur. Le nombre d’identités qu’un utilisateur unique peut posséder est limité à neuf. Chaque identité se compose d’un `namespace`, d’un `value`et d’un qualificateur d’espace de noms (`type`). Consultez l’[annexe](appendix.md) pour en savoir plus sur les propriétés requises.</li></ul> Consultez le [guide de dépannage](../troubleshooting-guide.md#user-ids) pour une explication plus détaillée de `users` et de `userIDs`. |
| `include` **(Obligatoire)** | Un tableau de produits Adobe à inclure dans votre traitement. Si cette valeur manque ou est vide, la requête sera rejetée. N’incluez que les produits pour lesquels votre organisation possède une intégration. Pour plus d’informations, consultez la section [Valeurs de produits acceptés](appendix.md) de l’annexe. |
| `expandIDs` | Une propriété facultative qui, lorsqu’elle est définie sur `true`, représente une optimisation du traitement des identifiants dans les applications (actuellement pris en charge uniquement par [!DNL Analytics]). Cette valeur est définie par défaut sur `false` si vous l’ignorez. |
| `priority` | Une propriété facultative utilisée par Adobe Analytics qui définit la priorité de traitement des requêtes. Les valeurs acceptées sont `normal` et `low`. Si la valeur `priority` est omise, le comportement par défaut est `normal`. |
| `analyticsDeleteMethod` | Une propriété facultative qui précise la façon dont Adobe Analytics doit traiter les données personnelles. Deux valeurs possibles sont acceptées pour cet attribut : <ul><li>`anonymize` : toutes les données référencées par la collection donnée des identifiants d’utilisateur sont anonymes. Il s’agit du comportement par défaut si `analyticsDeleteMethod` est omis.</li><li>`purge` : l’ensemble des données est complètement supprimé.</li></ul> |
| `mergePolicyId` | Lors de l’exécution de demandes d’accès à des informations personnelles pour Real-time Customer Profile (`profileService`), vous pouvez éventuellement fournir l’identifiant de la variable [stratégie de fusion](../../profile/merge-policies/overview.md) que vous souhaitez utiliser pour la combinaison d’identifiants. En spécifiant une stratégie de fusion, les demandes d’accès à des informations personnelles peuvent inclure des informations de segment lors du renvoi de données sur un client. Une seule stratégie de fusion peut être spécifiée par requête. Si aucune stratégie de fusion n’est fournie, les informations de segmentation ne sont pas incluses dans la réponse. |
| `regulation` **(Obligatoire)** | La réglementation de la tâche de confidentialité. Les valeurs suivantes sont acceptées : <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consultez la présentation sur [réglementations prises en charge](../regulations/overview.md) pour plus d’informations sur les réglementations de confidentialité que représentent les valeurs ci-dessus. |

{style="table-layout:auto"}

**Réponse**

Une réponse réussie renvoie les détails des tâches créées.

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
| `jobId` | Un identifiant généré par le système unique et en lecture seule pour une tâche. Cette valeur est utilisée à l’étape suivante pour rechercher une tâche spécifique. |

{style="table-layout:auto"}

Lorsque vous avez réussi à soumettre la requête de tâche, vous pouvez passer à l’étape suivante de [vérification de l’état de la tâche](#check-status).

## Vérification de l’état d’une tâche {#check-status}

Vous pouvez récupérer des informations sur une tâche spécifique, telles que son état de traitement actuel, en incluant le `jobId` dans le chemin d’une requête de GET à la fonction `/jobs` point de terminaison .

>[!IMPORTANT]
>
>Les données relatives aux tâches créées précédemment en sont disponibles à la récupération que pendant les 30 jours à compter de la date d’achèvement de la tâche.

**Format d’API**

```http
GET /jobs/{JOB_ID}
```

| Paramètre | Description |
| --- | --- |
| `{JOB_ID}` | L’identifiant de la tâche que vous souhaitez rechercher. Cet identifiant est renvoyé sous `jobId` dans les réponses d’API réussies pour [création d’une tâche](#create-job) et [liste de toutes les tâches](#list). |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère les détails de la tâche dont `jobId` est fourni dans le chemin d’accès de requête.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/6fc09b53-c24f-4a6c-9ca2-c6076b0842b6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Réponse**

Une réponse réussie renvoie les détails de la tâche spécifiée.

```json
{
    "jobId": "6fc09b53-c24f-4a6c-9ca2-c6076b0842b6",
    "requestId": "15700479082313109RX-899",
    "userKey": "David Smith",
    "action": "access",
    "status": "complete",
    "submittedBy": "{ACCOUNT_ID}",
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
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Finished successfully."
            }
        },
        {
            "product": "Profile",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6000-200",
                "responseMsgDetail": "Success dataSetIds = [5dbb87aad37beb18a96feb61], Failed dataSetIds = []"
            }
        },
        {
            "product": "AudienceManager",
            "retryCount": 0,
            "processedDate": "10/02/2019 08:25 PM GMT",
            "productStatusResponse": {
                "status": "complete",
                "message": "Success",
                "responseMsgCode": "PRVCY-6054-200",
                "responseMsgDetail": "PARTIALLY COMPLETED- Data not found for some requests, check results for more info.",
                "results": {
                  "processed": ["1123A4D5690B32A"],
                  "ignored": ["dsmith@acme.com"]
                }
            }
        }
    ],
    "downloadURL": "http://...",
    "regulation": "ccpa"
}
```

| Propriété | Description |
| --- | --- |
| `productStatusResponse` | Chaque objet dans la variable `productResponses` contient des informations sur l’état actuel de la tâche par rapport à un [!DNL Experience Cloud] application. |
| `productStatusResponse.status` | Catégorie d’état actuelle de la tâche. Consultez le tableau ci-dessous pour obtenir une liste des [catégories d’état disponibles](#status-categories) et leur signification correspondante. |
| `productStatusResponse.message` | État spécifique de la tâche, correspondant à la catégorie d’état. |
| `productStatusResponse.responseMsgCode` | Un code standard pour les messages de réponse de produit reçus par [!DNL Privacy Service]. Les détails du message sont fournis sous `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Une explication plus détaillée de l’état de la tâche. Les messages pour des statuts similaires peuvent varier d’un produit à l’autre. |
| `productStatusResponse.results` | Pour certains statuts, certains produits peuvent renvoyer une `results` qui fournit des informations supplémentaires non couvertes par `responseMsgDetail`. |
| `downloadURL` | Si l’état de la tâche est `complete`, cet attribut fournit une URL pour télécharger les résultats de la tâche sous la forme d’un fichier ZIP. Vous pouvez télécharger ce fichier pendant 60 jours à compter de l’achèvement de la tâche. |

{style="table-layout:auto"}

### Catégories d’état des tâches {#status-categories}

Le tableau suivant répertorie les différentes catégories d’état des tâches possibles et leur signification correspondante :

| Catégorie d’état | Signification |
| -------------- | -------- |
| `complete` | La tâche est terminée et les fichiers (si nécessaire) sont chargés depuis toutes les applications. |
| `processing` | Les applications ont reconnu la tâche et sont actuellement en train de la traiter. |
| `submitted` | La tâche est envoyée vers chaque application nécessaire. |
| `error` | Une erreur s’est produite lors du traitement de la tâche. Vous pouvez obtenir de plus amples informations en récupérant les détails individuels de la tâche. |

{style="table-layout:auto"}

>[!NOTE]
>
>Une tâche envoyée peut rester dans une `processing` indique si une tâche enfant dépendante est toujours en cours de traitement.

## Étapes suivantes

Vous savez maintenant comment créer et surveiller des tâches de confidentialité à l’aide du [!DNL Privacy Service] API. Pour plus d’informations sur la manière de réaliser les mêmes tâches à l’aide de l’interface utilisateur, consultez la [présentation de l’interface utilisateur Privacy Service](../ui/overview.md).

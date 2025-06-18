---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Point d’entrée de l’API des tâches de confidentialité
description: Découvrez comment gérer les tâches de confidentialité pour les applications Experience Cloud à l’aide de l’API Privacy Service.
role: Developer
exl-id: 74a45f29-ae08-496c-aa54-b71779eaeeae
source-git-commit: c2394035dd6bd4fe6dbb443e4db13934a27066a6
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 44%

---

# Point d’entrée des tâches de confidentialité

>[!IMPORTANT]
>
>Pour prendre en charge le nombre croissant de lois sur la protection de la vie privée aux États-Unis, Privacy Service modifie ses valeurs `regulation_type`. Utilisez les nouvelles valeurs qui incluent des abréviations d’état (par exemple, `ucpa_ut_usa`) à partir du 12 juin **2025**. Les anciennes valeurs (par exemple, `ucpa_usa`) ne fonctionnent plus après le 28 juillet 2025 **&#x200B;**.
>
>Mettez à jour vos intégrations avant cette date limite pour éviter les échecs de requête.

Ce document explique comment utiliser les tâches de confidentialité à l’aide d’appels API. Plus précisément, il couvre l’utilisation du point d’entrée `/job` dans l’API [!DNL Privacy Service]. Avant de lire ce guide, reportez-vous au [ guide de prise en main ](./getting-started.md) pour obtenir des informations importantes à connaître afin d’effectuer avec succès des appels vers l’API , y compris les en-têtes requis et la manière de lire des exemples d’appels API.

>[!NOTE]
>
>Si vous essayez de gérer les requêtes de consentement ou d’exclusion des clients, reportez-vous au guide [point d’entrée de consentement](./consent.md).

## Liste de toutes les tâches {#list}

Vous pouvez afficher une liste de toutes les tâches de confidentialité disponibles au sein de votre organisation en envoyant une requête GET au point d’entrée `/jobs`.

**Format d’API**

Ce format de requête utilise un paramètre de requête `regulation` sur le point d’entrée `/jobs`. Par conséquent, il commence par un point d’interrogation (`?`), comme illustré ci-dessous. Lors de l’énumération des ressources, l’API Privacy Service renvoie jusqu’à 1 000 tâches et pagine la réponse. Utilisez d’autres paramètres de requête (`page`, `size` et filtres de date) pour filtrer la réponse. Vous pouvez séparer plusieurs paramètres à l’aide d’esperluettes (`&`).

>[!TIP]
>
>Utilisez des paramètres de requête supplémentaires pour filtrer davantage les résultats pour des requêtes spécifiques. Vous pouvez, par exemple, déterminer le nombre de tâches relatives à la confidentialité qui ont été envoyées sur une période donnée et leur statut à l’aide des paramètres de requête `status`, `fromDate` et `toDate`.

```http
GET /jobs?regulation={REGULATION}
GET /jobs?regulation={REGULATION}&page={PAGE}
GET /jobs?regulation={REGULATION}&size={SIZE}
GET /jobs?regulation={REGULATION}&page={PAGE}&size={SIZE}
GET /jobs?regulation={REGULATION}&fromDate={FROMDATE}&toDate={TODATE}&status={STATUS}
```

| Paramètre | Description |
| --- | --- |
| `{REGULATION}` | Le type de réglementation pour lequel vous souhaitez effectuer une requête. Les valeurs acceptées sont les suivantes : <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpa_co_usa`</li><li>`cpra_ca_usa`</li><li>`ctdpa_ct_usa`</li><li>`dpdpa_de_usa`</li><li>`fdbr_fl_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`icdpa_ia_usa`</li><li>`lgpd_bra`</li><li>`mcdpa_mn_usa`</li><li>`mcdpa_mt_usa`</li><li>`mhmda_wa_usa`</li><li>`ndpa_ne_usa`</li><li>`nhpa_nh_usa`</li><li>`njdpa_nj_usa`</li><li>`nzpa_nzl`</li><li>`ocpa_or_usa`</li><li>`pdpa_tha`</li><li>`ql25_qc_can`</li><li>`tdpsa_tx_usa`</li><li>`tipa_tn_usa`</li><li>`ucpa_ut_usa`</li><li>`vcdpa_va_usa`</li></ul><br>Consultez la présentation des [réglementations prises en charge](../regulations/overview.md) pour plus d’informations sur les réglementations de confidentialité que représentent les valeurs ci-dessus. |
| `{PAGE}` | La page de données à afficher à l’aide d’une numérotation basée sur 0. La valeur par défaut est de `0`. |
| `{SIZE}` | Le nombre de résultats à afficher sur chaque page. `100` est la valeur par défaut et `1000` est le maximum. Dépasser le maximum entraîne le code d’erreur 400 dans l’API. |
| `{status}` | Le comportement par défaut consiste à inclure tous les statuts. Si vous spécifiez un type de statut, la requête renvoie uniquement les tâches de confidentialité correspondant à ce type de statut. Les valeurs acceptées sont les suivantes : <ul><li>`processing`</li><li>`complete`</li><li>`error`</li></ul> |
| `{toDate}` | Ce paramètre limite les résultats à ceux traités avant une date spécifiée. À partir de la date de la demande, le système peut revenir 45 jours en arrière. Toutefois, la plage ne peut pas être supérieure à 30 jours.<br>Il accepte le format AAAA-MM-JJ. La date que vous indiquez est interprétée comme la date de fin exprimée en heure de Greenwich (GMT).<br>Si vous ne fournissez pas ce paramètre (et une `fromDate` correspondante), le comportement par défaut renvoie les tâches qui contiennent les données des sept derniers jours. Si vous utilisez `toDate`, vous devez également utiliser le paramètre de requête `fromDate`. Si vous n’utilisez pas les deux, l’appel renvoie une erreur 400. |
| `{fromDate}` | Ce paramètre limite les résultats à ceux traités après une date spécifiée. À partir de la date de la demande, le système peut revenir 45 jours en arrière. Toutefois, la plage ne peut pas être supérieure à 30 jours.<br>Il accepte le format AAAA-MM-JJ. La date que vous indiquez est interprétée comme la date d’origine de la demande exprimée en heure de Greenwich (GMT).<br>Si vous ne fournissez pas ce paramètre (et une `toDate` correspondante), le comportement par défaut renvoie les tâches qui contiennent les données des sept derniers jours. Si vous utilisez `fromDate`, vous devez également utiliser le paramètre de requête `toDate`. Si vous n’utilisez pas les deux, l’appel renvoie une erreur 400. |
| `{filterDate}` | Ce paramètre limite les résultats à ceux traités à une date spécifiée. Il accepte le format AAAA-MM-JJ. Le système peut revenir sur les 45 derniers jours. |

{style="table-layout:auto"}

**Requête**

La requête suivante récupère une liste paginée de toutes les tâches d’une organisation, en commençant par la troisième page avec une taille de page de 50.

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

Pour récupérer le jeu suivant de résultats dans une réponse paginée, vous devez effectuer un autre appel API vers le même point d’entrée tout en augmentant le paramètre de requête `page` de 1.

## Création d’une tâche de confidentialité {#create-job}

>[!IMPORTANT]
>
>Privacy Service est destiné uniquement aux requêtes relatives aux titulaires de données et aux droits des clientes et clients. Toute autre utilisation de Privacy Service pour le nettoyage ou la maintenance des données n’est ni prise en charge ni autorisée. Adobe a l’obligation légale d’y répondre dans les délais impartis. Par conséquent, le test de chargement sur Privacy Service n’est pas autorisé, car il s’agit d’un environnement de production uniquement qui crée une liste d’attente inutile de requêtes d’accès à des informations personnelles valides.
>
>Une limite de chargement quotidienne stricte est maintenant en place pour prévenir les abus du service. Les utilisateurs et utilisatrices qui abusent du système verront leur accès au service désactivé. Une réunion ultérieure sera ensuite organisée avec ces utilisateurs et utilisatrices afin d’aborder leurs actions et de discuter de l’utilisation acceptable de Privacy Service.

Avant de créer une nouvelle demande de tâche, vous devez collecter des informations d’identification concernant les titulaires des données auxquelles vous souhaitez accéder, que vous voulez supprimer ou dont vous souhaitez refuser la vente. Une fois que vous disposez des données requises, elles doivent être fournies dans la payload d’une requête POST au point d’entrée `/jobs`.

>[!NOTE]
>
>Les applications Adobe Experience Cloud compatibles utilisent des valeurs d’identification des titulaires de données différentes. Pour plus d’informations sur les identifiants requis pour votre ou vos applications[&#128279;](../experience-cloud-apps.md) consultez le guide sur les applications Privacy Service et Experience Cloud . Pour des instructions plus générales sur la détermination des identifiants à envoyer à [!DNL Privacy Service], consultez le document sur les [données d’identité dans les demandes d’accès à des informations personnelles](../identity-data.md).

L’API [!DNL Privacy Service] prend en charge deux types de requêtes de tâche pour les données personnelles :

* [Accès et/ou suppression](#access-delete) : accédez (lisez) ou supprimez les données personnelles.
* [Opt-out de la vente](#opt-out) : marquez les données personnelles comme ne pouvant pas être vendues.

>[!IMPORTANT]
>
>Bien que les requêtes d’accès et de suppression puissent être combinées en un seul appel API, les requêtes d’opt-out doivent être effectuées séparément.

### Création d’un traitement d’accès/de suppression {#access-delete}

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
    "mergePolicyId": 124,
    "regulation": "ccpa"
}'
```

| Propriété | Description |
| --- | --- |
| `companyContexts` **(Obligatoire)** | Un tableau contenant des informations d’authentification pour votre organisation. Chaque identifiant répertorié inclut les attributs suivants : <ul><li>`namespace` : l’espace de noms d’un identifiant.</li><li>`value` : la valeur de l’identifiant.</li></ul>Il est **obligatoire** que l’un des identifiants utilise `imsOrgId` comme `namespace`, avec son `value` contenant l’ID unique de votre organisation. <br/><br/>Les identifiants supplémentaires peuvent être des qualificateurs d’entreprise spécifiques aux produits (par exemple, `Campaign`) qui identifient une intégration avec une application Adobe appartenant à votre organisation. Les valeurs potentielles incluent des noms de compte, des codes client, des identifiants du client ou d’autres identifiants d’application. |
| `users` **(Obligatoire)** | Un tableau contenant une collection d’au moins un utilisateur pour lequel vous souhaitez accéder aux informations ou les supprimer. Un maximum de 1 000 utilisateurs peut être fourni dans une seule demande. Chaque objet d’utilisateur contient les informations suivantes : <ul><li>`key` : un identifiant pour un utilisateur utilisé pour exécuter les identifiants de tâches distincts dans les données de réponse. Nous vous recommandons de choisir une chaîne unique et facilement identifiable pour cette valeur afin de pouvoir facilement la référencer ou la rechercher ultérieurement.</li><li>`action` : un tableau répertoriant les actions souhaitées pouvant être effectuées sur les données de l’utilisateur. En fonction des actions que vous souhaitez entreprendre, ce tableau peut inclure `access`, `delete` ou les deux.</li><li>`userIDs` : une collection d’identités pour cet utilisateur. Le nombre d’identités qu’un utilisateur unique peut posséder est limité à neuf. Chaque identité se compose d’un `namespace`, d’un `value`et d’un qualificateur d’espace de noms (`type`). Consultez l’[annexe](appendix.md) pour en savoir plus sur les propriétés requises.</li></ul> Consultez le [guide de dépannage](../troubleshooting-guide.md#user-ids) pour une explication plus détaillée de `users` et de `userIDs`. |
| `include` **(Obligatoire)** | Un tableau de produits Adobe à inclure dans votre traitement. Si cette valeur manque ou est vide, la requête sera rejetée. N’incluez que les produits pour lesquels votre organisation possède une intégration. Pour plus d’informations, consultez la section [Valeurs de produits acceptés](appendix.md) de l’annexe. |
| `expandIDs` | Une propriété facultative qui, lorsqu’elle est définie sur `true`, représente une optimisation du traitement des identifiants dans les applications (actuellement uniquement pris en charge par [!DNL Analytics]). Cette valeur est définie par défaut sur `false` si vous l’ignorez. |
| `priority` | Une propriété facultative utilisée par Adobe Analytics qui définit la priorité de traitement des requêtes. Les valeurs acceptées sont `normal` et `low`. Si la valeur `priority` est omise, le comportement par défaut est `normal`. |
| `mergePolicyId` | Lors de l’exécution de demandes d’accès à des informations personnelles pour le profil client en temps réel (`profileService`), vous pouvez éventuellement fournir l’identifiant de la [politique de fusion](../../profile/merge-policies/overview.md) spécifique que vous souhaitez utiliser pour l’assemblage des identifiants. En spécifiant une politique de fusion, les demandes d’accès à des informations personnelles peuvent inclure des informations d’audience lors du renvoi de données sur un client. Une seule politique de fusion peut être spécifiée par requête. Si aucune politique de fusion n’est fournie, les informations de segmentation ne sont pas incluses dans la réponse. |
| `regulation` **(Obligatoire)** | La réglementation pour la tâche de confidentialité. Les valeurs suivantes sont acceptées : <ul><li>`apa_aus`</li><li>`ccpa`</li><li>`cpra_usa`</li><li>`gdpr`</li><li>`hipaa_usa`</li><li>`lgpd_bra`</li><li>`nzpa_nzl`</li><li>`pdpa_tha`</li><li>`vcdpa_usa`</li></ul><br>Consultez la présentation des [réglementations prises en charge](../regulations/overview.md) pour plus d’informations sur les réglementations de confidentialité que représentent les valeurs ci-dessus. |

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

Vous pouvez récupérer des informations sur une tâche spécifique, telles que son statut de traitement actuel, en incluant le `jobId` de cette tâche dans le chemin d’accès d’une requête GET au point d’entrée `/jobs`.

>[!IMPORTANT]
>
>Les données des tâches créées précédemment ne peuvent être récupérées que dans les 30 jours suivant la date d’achèvement de la tâche.

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
| `productStatusResponse` | Chaque objet du tableau de `productResponses` contient des informations sur le statut actuel de la tâche par rapport à une application de [!DNL Experience Cloud] spécifique. |
| `productStatusResponse.status` | Catégorie de statut actuelle du traitement. Consultez le tableau ci-dessous pour obtenir la liste des [catégories de statut disponibles](#status-categories) et leur signification correspondante. |
| `productStatusResponse.message` | Statut spécifique du traitement, correspondant à la catégorie de statut. |
| `productStatusResponse.responseMsgCode` | Code standard pour les messages de réponse de produit reçus par [!DNL Privacy Service]. Les détails du message sont fournis sous `responseMsgDetail`. |
| `productStatusResponse.responseMsgDetail` | Une explication plus détaillée du statut de la tâche. Les messages avec des statuts similaires peuvent varier d’un produit à l’autre. |
| `productStatusResponse.results` | Pour certains états, certains produits peuvent renvoyer un objet `results` qui fournit des informations supplémentaires non couvertes par `responseMsgDetail`. |
| `downloadURL` | Si l’état de la tâche est `complete`, cet attribut fournit une URL pour télécharger les résultats de la tâche sous la forme d’un fichier ZIP. Vous pouvez télécharger ce fichier pendant 60 jours à compter de l’achèvement de la tâche. |

{style="table-layout:auto"}

### Catégories de statut de la tâche {#status-categories}

Le tableau suivant répertorie les différentes catégories de statut de tâche possibles et leur signification correspondante :

| Catégorie de statut | Signification |
| -------------- | -------- |
| `complete` | La tâche est terminée et les fichiers (si nécessaire) sont chargés depuis toutes les applications. |
| `processing` | Les applications ont reconnu la tâche et sont actuellement en train de la traiter. |
| `submitted` | La tâche est envoyée vers chaque application nécessaire. |
| `error` | Une erreur s’est produite lors du traitement de la tâche. Vous pouvez obtenir de plus amples informations en récupérant les détails individuels de la tâche. |

{style="table-layout:auto"}

>[!NOTE]
>
>Une tâche envoyée peut rester dans un état `processing` si elle a une tâche enfant dépendante en cours de traitement.

## Étapes suivantes

Vous savez désormais comment créer et surveiller les tâches de confidentialité à l’aide de l’API [!DNL Privacy Service]. Pour plus d’informations sur la manière de réaliser les mêmes tâches à l’aide de l’interface utilisateur, consultez la [présentation de l’interface utilisateur Privacy Service](../ui/overview.md).

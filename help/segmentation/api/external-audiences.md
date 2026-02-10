---
title: Point d’entrée de l’API Audiences externes
description: Découvrez comment utiliser l’API des audiences externes pour créer, mettre à jour, activer et supprimer vos audiences externes de Adobe Experience Platform.
exl-id: eaa83933-d301-48cb-8a4d-dfeba059bae1
source-git-commit: ff58324446f28cbdca369ecbb58d8261614ae684
workflow-type: tm+mt
source-wordcount: '2340'
ht-degree: 9%

---

# Point d’entrée des audiences externes

Les audiences externes vous permettent de charger des données de profil à partir de vos sources externes dans Adobe Experience Platform. Vous pouvez utiliser le point d’entrée `/external-audience` dans l’API Segmentation Service pour ingérer une audience externe vers Experience Platform, afficher les détails et mettre à jour vos audiences externes, ainsi que supprimer vos audiences externes.

## Mécanismes de sécurisation

À compter de la version de mars, les mécanismes de sécurisation suivants seront appliqués lors de l’utilisation du point d’entrée d’audiences externes :

| Mécanisme de sécurisation | Limite | Type de limite | Description |
| --------- | ----- | ---------- | ----------- |
| Nombre d’exécutions d’ingestion d’audience par jour | 100 | Mécanisme de sécurisation mis en œuvre par le système | Nombre maximal d’exécutions d’ingestion d’audience autorisées par jour. Cette limite est de au niveau **sandbox**. |
| Nombre d’ingestions par audience | 10 | Mécanisme de sécurisation mis en œuvre par le système | Nombre d’ingestions pouvant être effectuées sur une audience spécifiée. |
| Taille de l’audience externe | 10 GO | Mécanisme de sécurisation des performances | La taille totale recommandée de l’audience externe est de 10 Go. |

## Prise en main

>[!IMPORTANT]
>
>Les points d’entrée de ce guide sont précédés du préfixe `/core/ais`, par opposition à `/core/ups`.

Pour utiliser les API Experience Platform, vous devez avoir suivi le tutoriel [authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels API Experience Platform, comme illustré ci-dessous :

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id : `{ORG_ID}`

Dans [!DNL Experience Platform], toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes envoyées aux API [!DNL Experience Platform] nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération sera effectuée :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur l’utilisation des sandbox dans [!DNL Experience Platform], consultez la [documentation de présentation des sandbox](../../sandboxes/home.md).

## Créer une audience externe {#create-audience}

Vous pouvez créer une audience externe en effectuant une requête POST vers le point d’entrée `/external-audience/`.

**Format d’API**

```http
POST /external-audience/
```

**Requête**

+++ Exemple de requête pour créer une audience externe.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": "40",
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }'
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `name` | Chaîne | Nom de l’audience externe. |
| `description` | Chaîne | Description facultative de l’audience externe. |
| `customAudienceId` | Chaîne | Identifiant facultatif de votre audience externe. |
| `fields` | Tableau d’objets | La liste des champs et leurs types de données. Lors de la création de la liste des champs, vous pouvez ajouter les éléments suivants : <ul><li>`name` : **Obligatoire** nom du champ qui fait partie de la spécification de l’audience externe.</li><li>`type` : **Obligatoire** type de données qui entre dans le champ. Les valeurs prises en charge sont les suivantes : `string`, `number`, `long`, `integer`, `date` (`2025-05-13`), `datetime` (`2025-05-23T20:19:00+00:00`) et `boolean`.</li><li>`identityNs` : **Obligatoire pour le champ d’identité** Espace de noms utilisé par le champ d’identité. Les valeurs prises en charge incluent tous les espaces de noms valides, tels que `ECID` ou `email`.</li><li>`labels` : *facultatif* tableau de libellés de contrôle d’accès pour le champ. Vous trouverez plus d’informations sur les libellés de contrôle d’accès disponibles dans le [glossaire des libellés d’utilisation des données](/help/data-governance/labels/reference.md). </li></ul> |
| `sourceSpec` | Objet | Objet contenant les informations sur l’emplacement de l’audience externe. Lors de l’utilisation de cet objet, vous **devez** inclure les informations suivantes : <ul><li>`path` : **Obligatoire** : emplacement de l’audience externe ou du dossier contenant l’audience externe dans la source. Le chemin d’accès au fichier **ne peut pas** contenir d’espaces. Par exemple, si votre chemin d’accès est `activation/sample-source/Example CSV File.csv`, définissez-le sur `activation/sample-source/ExampleCSVFile.csv`. Le chemin d’accès à votre source se trouve dans la colonne **Données Source** de la section des flux de données.</li><li>`type`: **Obligatoire** type de l’objet que vous récupérez à partir de la source. Cette valeur peut être `file` ou `folder`.</li><li>`sourceType` : *facultatif* type de source à partir de laquelle vous effectuez une récupération. Actuellement, la seule valeur prise en charge est `Cloud Storage`.</li><li>`cloudType` : **obligatoire** type d’espace de stockage dans le cloud, basé sur le type de source. Les valeurs prises en charge sont `S3`, `DLZ`, `GCS`, `Azure` et `SFTP`.</li><li>`baseConnectionId` : identifiant de la connexion de base. Il est fourni par votre fournisseur source. Cette valeur est **obligatoire** si vous utilisez une valeur `cloudType` de `S3`, `GCS` ou `SFTP`. Dans le cas contraire **vous n’avez** besoin d’inclure ce paramètre. Pour plus d’informations, consultez la [présentation des connecteurs source](../../sources/home.md).</li></ul> |
| `ttlInDays` | Entier | Expiration des données de l’audience externe, en jours. Cette valeur peut être définie de 1 à 90. Par défaut, l’expiration des données est définie sur 30 jours. |
| `audienceType` | Chaîne | Type d’audience pour l’audience externe. Actuellement, seul `people` est pris en charge. |
| `originName` | Chaîne | **Obligatoire** Origine de l’audience. Cette information indique d’où vient l’audience. Pour les audiences externes, vous devez utiliser `CUSTOM_UPLOAD`. |
| `namespace` | Chaîne | Espace de noms de l’audience. Par défaut, cette valeur est définie sur `CustomerAudienceUpload`. |
| `labels` | Tableau de chaînes | Libellés de contrôle d’accès qui s’appliquent à l’audience externe. Vous trouverez plus d’informations sur les libellés de contrôle d’accès disponibles dans le [glossaire des libellés d’utilisation des données](/help/data-governance/labels/reference.md). |
| `tags` | Tableau de chaînes | Balises à appliquer à l’audience externe. Vous trouverez plus d’informations sur les balises dans le [guide de gestion des balises](/help/administrative-tags/ui/managing-tags.md). |

+++

**Réponse**

Une réponse réussie renvoie le statut HTTP 202 avec les détails de votre audience externe nouvellement créée.

+++ Exemple de réponse lors de la création d’une audience externe.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    }   
}
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `operationId` | Chaîne | Identifiant de l’opération. Vous pouvez ensuite utiliser cet identifiant pour récupérer le statut de la création de votre audience. |
| `operationDetails` | Objet | Objet contenant les détails de la demande que vous avez envoyée pour créer l’audience externe. |
| `name` | Chaîne | Nom de l’audience externe. |
| `description` | Chaîne | Description de l’audience externe. |
| `fields` | Tableau d’objets | La liste des champs et leurs types de données. Ce tableau détermine les champs dont vous avez besoin dans votre audience externe. |
| `sourceSpec` | Objet | Objet contenant les informations sur l’emplacement de l’audience externe. |
| `ttlInDays` | Entier | Expiration des données de l’audience externe, en jours. Cette valeur peut être définie de 1 à 90. Par défaut, l’expiration des données est définie sur 30 jours. |
| `audienceType` | Chaîne | Type d’audience pour l’audience externe. |
| `originName` | Chaîne | **Obligatoire** Origine de l’audience. Indique d’où provient l’audience. |
| `namespace` | Chaîne | Espace de noms de l’audience. |
| `labels` | Tableau de chaînes | Libellés de contrôle d’accès qui s’appliquent à l’audience externe. Vous trouverez plus d’informations sur les libellés de contrôle d’accès disponibles dans le [glossaire des libellés d’utilisation des données](/help/data-governance/labels/reference.md). |


+++

## Récupérer le statut de création de l’audience {#retrieve-status}

Vous pouvez récupérer le statut de l’envoi de votre audience externe en adressant une requête GET au point d’entrée `/external-audiences/operations` et en fournissant l’identifiant de l’opération que vous avez reçu de la réponse de création d’audience externe.

**Format d’API**

```http
GET /external-audiences/operations/{OPERATION_ID}
```

| Paramètre | Description |
| --------- | ----------- |
| `{OPERATION_ID}` | Valeur `id` de l’opération que vous souhaitez récupérer. |

**Requête**

+++ Exemple de requête pour récupérer le statut d’opération d’une audience externe.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/operations/df8cd82f-a214-4b72-b549-d6ee23f1ff1a \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un statut HTTP 200 avec les détails du statut de la tâche de l’audience externe.

+++ Exemple de réponse lorsque vous récupérez le statut de la tâche d’une audience externe.

```json
{
    "operationId": "df8cd82f-a214-4b72-b549-d6ee23f1ff1a",
    "status": "SUCCESS",
    "operationDetails": {
        "name": "Sample external audience",
        "description": "A sample version of an external audience",
        "fields": [
            {
                "name": "ppid",
                "type": "string",
                "identityNs": "Email"
            },
            {
                "name": "list_id",
                "type": "string",
                "labels": ["core/C2", "custom/deep"]
            },
            {
                "name": "delete",
                "type": "number"
            },
            {
                "name": "process_consent",
                "type": "string"
            }
        ],
        "sourceSpec": {
            "params": {
                "path": "activation/sample-source/example.csv",
                "type": "file",
                "sourceType": "Cloud Storage",
                "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
            }
        },
        "ttlInDays": 40,
        "labels": ["core/C1"],
        "audienceType": "people",
        "originName": "CUSTOM_UPLOAD"
    },
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `operationId` | Chaîne | Identifiant de l’opération que vous récupérez. |
| `status` | Chaîne | Statut de l’opération. Il peut s’agir de l’une des valeurs suivantes : `SUCCESS`, `FAILED`, `PROCESSING`. |
| `operationDetails` | Objet | Un objet contenant les détails de l’audience. |
| `audienceId` | Chaîne | Identifiant de l’audience externe qui est envoyée par l’opération. |
| `createdBy` | Chaîne | Identifiant de l’utilisateur qui a créé l’audience externe. |
| `createdAt` | Date et heure de l’époque longue | Date et heure, en secondes, auxquelles la demande de création de l’audience externe a été envoyée. |
| `updatedBy` | Chaîne | ID de la dernière personne à avoir mis à jour l’audience. |
| `updatedAt` | Date et heure de l’époque longue | Date et heure, en secondes, de la dernière mise à jour de l’audience. |

+++

## Mise à jour d’une audience externe {#update-audience}

>[!NOTE]
>
>Pour utiliser le point d’entrée suivant, vous devez disposer de la `audienceId` de votre audience externe. Vous pouvez obtenir votre `audienceId` d’un appel réussi au point d’entrée `GET /external-audiences/operations/{OPERATION_ID}`.

Vous pouvez mettre à jour les champs de votre audience externe en adressant une requête PATCH au point d’entrée `/external-audience` et en fournissant l’identifiant de l’audience dans le chemin de requête.

Lors de l’utilisation de ce point d’entrée, vous pouvez mettre à jour les champs suivants :

- Description de l&#39;audience
- Libellés de contrôle d’accès au niveau du champ
- Libellés de contrôle d’accès au niveau de l’audience
- Expiration des données de l’audience

La mise à jour du champ à l’aide de ce point d’entrée **remplace** le contenu du champ que vous avez demandé.

**Format d’API**

```http
PATCH /external-audience/{AUDIENCE_ID}
```

**Requête**

+++ Exemple de requête pour mettre à jour la description de l’audience externe.

```shell
curl -X PATCH https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab\
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "description": "New sample description"
 }'
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `description` | Chaîne | Description mise à jour de l’audience externe. |

De plus, vous pouvez mettre à jour les paramètres suivants :

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `labels` | Tableau | Un tableau contenant la liste mise à jour des libellés d’accès pour l’audience. Vous trouverez plus d’informations sur les libellés de contrôle d’accès disponibles dans le [glossaire des libellés d’utilisation des données](/help/data-governance/labels/reference.md). |
| `fields` | Tableau d’objets | Tableau contenant les champs et leurs libellés associés pour l’audience externe. Seuls les champs répertoriés dans la demande PATCH seront mis à jour. Vous trouverez plus d’informations sur les libellés de contrôle d’accès disponibles dans le [glossaire des libellés d’utilisation des données](/help/data-governance/labels/reference.md). |
| `ttlInDays` | Entier | Expiration des données de l’audience externe, en jours. Cette valeur peut être définie de 1 à 90. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de l’audience externe mise à jour.

+++ Exemple de réponse lors de la mise à jour de la description de l’audience externe.

```json
{
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "audienceName": "Sample external audience",
    "description": "New sample description",
    "fields": [
        {
            "name": "ppid",
            "type": "string",
            "identityNs": "Email"
        },
        {
            "name": "list_id",
            "type": "string",
            "labels": ["core/C2", "custom/deep"]
        },
        {
            "name": "delete",
            "type": "number"
        },
        {
            "name": "process_consent",
            "type": "string"
        }
    ],
    "sourceSpec": {
        "path": "activation/sample-source/example.csv",
        "type": "file",
        "sourceType": "Cloud Storage",
        "baseConnectionId": "1d1d4bc5-b527-46a3-9863-530246a61b2b"
        },
    "ttlInDays": 40,
    "labels": ["core/C1"],
    "audienceType": "people",
    "originName": "CUSTOM_UPLOAD",
    "createdBy": "{USER_ID}",
    "createdAt": 1749324248,
    "updatedBy": "{USER_ID}",
    "updatedAt": 1749624273
}
```

+++

## Démarrer l’ingestion de l’audience {#start-audience-ingestion}

>[!IMPORTANT]
>
>Vous ne pourrez **pas** démarrer une nouvelle ingestion pour l’audience externe si une ingestion d’audience précédente est déjà en cours.

>[!NOTE]
>
>Pour utiliser le point d’entrée suivant, vous devez disposer de la `audienceId` de votre audience externe. Vous pouvez obtenir votre `audienceId` d’un appel réussi au point d’entrée `GET /external-audiences/operations/{OPERATION_ID}`.

Vous pouvez démarrer une ingestion d’audience en adressant une requête POST au point d’entrée suivant tout en fournissant l’identifiant d’audience.

**Format d’API**

```http
POST /external-audience/{AUDIENCE_ID}/runs
```

**Requête**

La requête suivante déclenche une exécution d’ingestion pour l’audience externe.

+++ Exemple de requête pour démarrer une ingestion d’audience.

```shell
curl -X POST https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "dataFilterStartTime": 764245635
 }' 
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `dataFilterStartTime` | Date et heure de l’époque | **Obligatoire** Plage spécifiant l’heure de début pour déterminer les fichiers à traiter. Cela signifie que les fichiers sélectionnés seront des fichiers **après** l’heure spécifiée. |
| `dataFilterEndTime` | Date et heure de l’époque | La plage spécifiant l’heure de fin à laquelle le flux s’exécutera pour sélectionner les fichiers à traiter. Cela signifie que les fichiers sélectionnés seront des fichiers **avant** l’heure spécifiée. |

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec des détails sur l’exécution de l’ingestion.

+++ Exemple de réponse lors du démarrage de l’ingestion de l’audience.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 4565657575,
    "createdAt": 4565657575,
    "createdBy:" "{USER_ID}"
}
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `audienceName` | Chaîne | Nom de l’audience pour laquelle vous démarrez une exécution d’ingestion. |
| `audienceId` | Chaîne | Identifiant de l’audience. |
| `runId` | Chaîne | Identifiant de l’exécution d’ingestion que vous avez démarrée. |
| `differentialIngestion` | Booléen | Champ qui détermine si l’ingestion est une ingestion partielle en fonction de la différence depuis la dernière ingestion ou une ingestion d’audience complète. |
| `dataFilterStartTime` | Date et heure de l’époque | La plage spécifiant l’heure de début d’exécution du flux pour sélectionner les fichiers traités. |
| `dataFilterEndTime` | Date et heure de l’époque | La plage spécifiant l’heure de fin à laquelle le flux s’exécute pour sélectionner les fichiers traités. |
| `createdAt` | Date et heure de l’époque longue | Date et heure, en secondes, auxquelles la demande de création de l’audience externe a été envoyée. |
| `createdBy` | Chaîne | Identifiant de l’utilisateur qui a créé l’audience externe. |

+++

## Récupération du statut d’ingestion d’audience spécifique {#retrieve-ingestion-status}

>[!NOTE]
>
>Pour utiliser le point d’entrée suivant, vous devez disposer à la fois du `audienceId` de votre audience externe et du `runId` de votre identifiant d’exécution d’ingestion. Vous pouvez obtenir votre `audienceId` à partir d’un appel réussi au point d’entrée `GET /external-audiences/operations/{OPERATION_ID}` et votre `runId` à partir d’un appel réussi précédent du point d’entrée `POST /external-audience/{AUDIENCE_ID}/runs`.

Vous pouvez récupérer le statut d’une ingestion d’audience en adressant une requête GET au point d’entrée suivant tout en fournissant les identifiants d’audience et d’exécution.

**Format d’API**

```http
GET /external-audience/{AUDIENCE_ID}/runs/{RUN_ID}
```

**Requête**

La requête suivante récupère le statut de l’ingestion pour l’audience externe.

+++ Exemple de requête pour récupérer le statut d’ingestion de l’audience externe.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs/fb342311-725d-4b48-ab7d-c6105fbc2b8b \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec les détails de l’ingestion de l’audience externe.

+++ Exemple de réponse lors de la récupération de l’ingestion de l’audience externe.

```json
{
    "audienceName": "Sample external audience",
    "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
    "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
    "status": "SUCCESS",
    "differentialIngestion": true,
    "dataFilterStartTime": 764245635,
    "dataFilterEndTime": 3456788568,
    "createdAt": 1749324248,
    "createdBy": "{USER_ID}",
    "details": [
        {
            "stage": "DATASET_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        },
        {
            "stage": "PROFILE_STORE_INGEST",
            "status": "SUCCESS",
            "flowRunId": "{FLOW_RUN_ID}"
        }
    ]
}
```

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `audienceName` | Chaîne | Nom de l’audience. |
| `audienceId` | Chaîne | Identifiant de l’audience. |
| `runId` | Chaîne | Identifiant de l’exécution d’ingestion. |
| `status` | Chaîne | Statut de l’exécution de l’ingestion. Les statuts possibles incluent `SUCCESS` et `FAILED`. |
| `differentialIngestion` | Booléen | Champ qui détermine si l’ingestion est une ingestion partielle en fonction de la différence depuis la dernière ingestion ou une ingestion d’audience complète. |
| `dataFilterStartTime` | Date et heure de l’époque | La plage spécifiant l’heure de début d’exécution du flux pour sélectionner les fichiers traités. |
| `dataFilterEndTime` | Date et heure de l’époque | La plage spécifiant l’heure de fin à laquelle le flux s’exécute pour sélectionner les fichiers traités. |
| `createdAt` | Date et heure de l’époque longue | Date et heure, en secondes, auxquelles la demande de création de l’audience externe a été envoyée. |
| `createdBy` | Chaîne | Identifiant de l’utilisateur qui a créé l’audience externe. |
| `details` | Tableau d’objets | Objet contenant les détails de l’exécution de l’ingestion. <ul><li>`stage` : étape de l’exécution de l’ingestion. Il peut s’agir de `DATASET_INGEST` ou `PROFILE_STORE_INGEST`, qui représentent l’ingestion du lac de données et l’ingestion du profil.</li><li>`status` : statut de l’ingestion sur l’étape. Les statuts possibles incluent `SUCCESS` et `FAILED`.</li><li>`flowRunId` : ID de l’exécution du flux d’ingestion de l’étape.</li></ul> |

+++

## Liste des exécutions d’ingestion d’audience {#list-ingestion-runs}

>[!NOTE]
>
>Pour utiliser le point d’entrée suivant, vous devez disposer de la `audienceId` de votre audience externe. Vous pouvez obtenir votre `audienceId` d’un appel réussi au point d’entrée `GET /external-audiences/operations/{OPERATION_ID}`.

Vous pouvez récupérer toutes les exécutions d’ingestion pour l’audience externe sélectionnée en envoyant une requête GET au point d’entrée suivant tout en fournissant l’identifiant d’audience. Plusieurs paramètres peuvent être inclus et séparés par des esperluettes (`&`).

**Format d’API**

<!-- The following endpoint supports several query parameters to help filter your results. While these parameters are optional, their use is strongly recommended to help focus your results. -->

```http
GET /external-audience/{AUDIENCE_ID}/runs
```

<!-- **Query parameters**

+++ A list of available query parameters. 

| Parameter | Description | Example |
| --------- | ----------- | ------- |
| `limit` | The maximum number of items returned in the response. This value can range from 1 to 40. By default, the limit is set to 20. | `limit=30` |
| `sortBy` | The order in which the returned items are sorted. You can sort by either `name` or by `createdAt`. Additionally, you can add a `-` sign to sort by **descending** order instead of **ascending** order. By default, the items are sorted by `createdAt` in descending order. | `sortBy=name` |
| `property` | A filter to determine which audience ingestion runs are displayed. You can filter on the following properties: <ul><li>`name`: Lets you filter by the audience name. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li><li>`createdAt`: Lets you filter by the ingestion time. If using this property, you can compare by using `>=` or `<=`.</li><li>`status`: Lets you filter by the ingestion run's status. If using this property, you can compare by using `=`, `!=`, `=contains`, or `!=contains`. </li></ul>  | `property=createdAt<1683669114845`<br/>`property=name=demo_audience`<br/>`property=status=SUCCESS` |

+++ -->

**Requête**

La requête suivante récupère toutes les exécutions d’ingestion pour l’audience externe.

+++ Un exemple de requête pour obtenir une liste des exécutions d’ingestion d’audience.

```shell
curl -X GET https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/runs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 200 avec une liste d’exécutions d’ingestion pour l’audience externe spécifiée.

+++ Un exemple de réponse lorsque vous récupérez une liste des exécutions d’ingestion d’audience.

```json
{
    "runs": [
        {
            "audienceName": "Sample external audience",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "fb342311-725d-4b48-ab7d-c6105fbc2b8b",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1785678909,
            "createdBy": "{USER_NAME}"
        },
        {
            "audienceName": "Sample external audience 2",
            "audienceId": "60ccea95-1435-4180-97a5-58af4aa285ab",
            "runId": "406e38e4-fbd5-43e1-8d0c-01ccb3f9ad10",
            "status": "SUCCESS",
            "differentialIngestion": true,
            "dataFilterStartTime": 764245635,
            "dataFilterEndTime": 3456788568,
            "createdAt": 1749324248,
            "createdBy": "{USER_ID}"
        }
    ]
}
```

<!-- ,
    "_page": {
        "limit": 20,
        "count": 2,
        "totalCount": 2
    }
    
| `_page` | Object | An object that contains the pagination information about the list of results. |
     -->

| Propriété | Type | Description |
| -------- | ---- | ----------- |
| `runs` | Objet | Objet contenant la liste des exécutions d’ingestion appartenant à l’audience. Vous trouverez plus d’informations sur cet objet dans la section [récupérer le statut de l’ingestion](#retrieve-ingestion-status). |

+++

## Suppression d’une audience externe {#delete-audience}

>[!NOTE]
>
>Pour utiliser le point d’entrée suivant, vous devez disposer de la `audienceId` de votre audience externe. Vous pouvez obtenir votre `audienceId` d’un appel réussi au point d’entrée `GET /external-audiences/operations/{OPERATION_ID}`.

Vous pouvez supprimer une audience externe en effectuant une requête DELETE au point d’entrée suivant tout en fournissant l’identifiant d’audience.

**Format d’API**

```http
DELETE /external-audience/{AUDIENCE_ID}
```

**Requête**

La requête suivante supprime l’audience externe spécifiée.

+++ Exemple de requête pour supprimer l’audience externe.

```shell
curl -X DELETE https://platform.adobe.io/data/core/ais/external-audience/60ccea95-1435-4180-97a5-58af4aa285ab/ \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Réponse**

Une réponse réussie renvoie un état HTTP 204 avec un corps de réponse vide.

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de ce guide. À présent, vous comprenez mieux comment créer, gérer et supprimer vos audiences externes à l’aide des API d’Experience Platform. Pour savoir comment utiliser des audiences externes avec l’interface utilisateur d’Experience Platform, consultez la [documentation du portail Audience](../ui/audience-portal.md).

## Annexe {#appendix}

La section suivante répertorie les codes d’erreur disponibles lors de l’utilisation de l’API des audiences externes.

| Code d’erreur de la plateforme | Code d’état | Message | Description |
| ------------------- | ----------- | ------- | ----------- |
| 100910-400 | 400 | `BAD_REQUEST` | Une requête incorrecte s’est produite en raison d’un échec lors de la validation des requêtes. |
| 100911-400 | 400 | `BAD_REQUEST` | Un jeton non valide est fourni. |
| 100920-401 | 401 | `UNAUTHORIZED` | Un en-tête est manquant. |
| 100921-401 | 401 | `UNAUTHORIZED` | Un `imsOrgId` non valide est fourni. |
| 100922-401 | 401 | `UNAUTHORIZED` | Vous n’êtes pas autorisé à utiliser les API d’audiences externes. |
| 100940-404 | 404 | `NOT_FOUND` | L’audience demandée est introuvable. |
| 100950-409 | 409 | `DUPLICATE_RESOURCE` | L’audience existe déjà. |
| 100960-422 | 422 | `UNPROCESSABLE_ENTITY` | La structure de la requête est valide, mais elle ne peut pas être traitée en raison d’erreurs logiques ou sémantiques. |
| 100970-500 | 500 | `INTERNAL_SERVER_ERROR` | Un problème est survenu lors du traitement de la demande dans le système. |
| 100970-502 | 502 | `BAD_GATEWAY` | Il y a des problèmes de dépendance en aval. |

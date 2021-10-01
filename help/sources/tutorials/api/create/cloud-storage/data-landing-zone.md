---
keywords: Experience Platform;accueil;rubriques populaires;
solution: Experience Platform
title: Connexion d’une zone d’entrée de données à Adobe Experience Platform à l’aide de l’API Flow Service
topic-legacy: overview
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Data Landing Zone à l’aide de l’API Flow Service.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: ca7197036283ee15dbf60c113d361a5ea34d65c1
workflow-type: tm+mt
source-wordcount: '951'
ht-degree: 8%

---

# Connecter [!DNL Data Landing Zone] à Adobe Experience Platform à l’aide de l’API Flow Service

[!DNL Data Landing Zone] est une fonctionnalité de stockage de données dans le cloud pour le stockage de fichiers temporaire configurée avec Adobe Experience Platform. [!DNL Data Landing Zone] est utilisé uniquement pour l’entrée et la sortie de vos données dans et hors de Platform. Les données sont automatiquement supprimées de [!DNL Data Landing Zone] au bout de sept jours.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion source [!DNL Data Landing Zone] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Ce tutoriel fournit également des instructions sur la manière de récupérer votre [!DNL Data Landing Zone], ainsi que d’afficher et d’actualiser vos informations d’identification.

## Prise en main

Ce guide nécessite une compréhension pratique des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données à partir de diverses sources tout en vous permettant de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services Platform.
* [Environnements de test](../../../../../sandboxes/home.md) : Experience Platform fournit des environnements de test virtuels qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour créer une connexion source [!DNL Data Landing Zone] à l’aide de l’API [!DNL Flow Service].

Ce tutoriel nécessite également de lire le guide sur la [prise en main des API Platform](../../../../../landing/api-guide.md) pour apprendre à vous authentifier auprès des API Platform et interpréter les exemples d’appels fournis dans la documentation.

## Récupération d’une zone d’entrée utilisable

La première étape de l’utilisation des API pour accéder à [!DNL Data Landing Zone] consiste à envoyer une requête de GET au point de terminaison `/landingzone` de l’API [!DNL Connectors] tout en fournissant `type=user_drop_zone` dans le cadre de l’en-tête de votre requête.

**Format d&#39;API**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| En-têtes | Description |
| --- | --- |
| `user_drop_zone` | Le type `user_drop_zone` permet à l’API de distinguer un conteneur de zone d’entrée des autres types de conteneurs disponibles. |

**Requête**

La requête suivante récupère une zone d’entrée existante.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Réponse**

La réponse suivante renvoie des informations sur une zone d’entrée, y compris les `containerName` et `containerTTL` correspondants.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Nom de la zone d’entrée que vous avez récupérée. |
| `containerTTL` | Le paramètre de durée de vie appliqué à vos données dans la zone d’entrée. Tout ce qui se trouve dans une zone d’entrée donnée est supprimé au bout de sept jours. |

## Récupération des [!DNL Data Landing Zone] informations d’identification

Pour récupérer les informations d’identification d’une API [!DNL Data Landing Zone], envoyez une demande de GET au point de terminaison `/credentials` de l’API [!DNL Connectors].

**Format d’API**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**Requête**

L’exemple de requête suivant récupère les informations d’identification d’une zone d’entrée existante.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

La réponse suivante renvoie les informations d’identification pour votre zone d’entrée, y compris votre `SASToken` et `SASUri` actuel, ainsi que la balise `storageAccountName` correspondant au conteneur de votre zone d’entrée.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Nom de votre zone d’entrée. |
| `SASToken` | Jeton de signature d’accès partagé pour votre zone d’entrée. Cette chaîne contient toutes les informations nécessaires pour autoriser une requête. |
| `SASUri` | URI de signature d’accès partagé pour votre zone d’entrée. Cette chaîne est une combinaison de l’URI de la zone d’entrée pour laquelle vous êtes authentifié et de son jeton SAS correspondant, |


## Mise à jour des informations d’identification [!DNL Data Landing Zone]

Vous pouvez mettre à jour votre `SASToken` en envoyant une requête de POST au point de terminaison `/credentials` de l’API [!DNL Connectors].

**Format d&#39;API**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| En-têtes | Description |
| --- | --- |
| `user_drop_zone` | Le type `user_drop_zone` permet à l’API de distinguer un conteneur de zone d’entrée des autres types de conteneurs disponibles. |
| `refresh` | L’action `refresh` vous permet de réinitialiser les informations d’identification de votre zone d’entrée et de générer automatiquement une nouvelle `SASToken`. |

**Requête**

La requête suivante met à jour les informations d’identification de votre zone d’entrée.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

La réponse suivante renvoie des valeurs mises à jour pour vos `SASToken` et `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Explorez la structure et le contenu des fichiers de la zone d’entrée

Vous pouvez explorer la structure des fichiers et le contenu de votre zone d’entrée en adressant une requête de GET au point de terminaison `connectionSpecs` de l’API [!DNL Flow Service].

**Format d’API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | L’identifiant de spécification de connexion qui correspond à [!DNL Data Landing Zone]. Cet ID fixe est : `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de fichiers et de dossiers trouvés dans le répertoire interrogé. Prenez note de la propriété `path` du fichier que vous souhaitez charger, car vous devez la fournir à l’étape suivante pour examiner sa structure.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## Prévisualiser la structure et le contenu des fichiers de la zone d&#39;entrée

Pour inspecter la structure d’un fichier dans votre zone d’entrée, effectuez une requête de GET tout en fournissant le chemin d’accès du fichier et saisissez comme paramètre de requête.

**Format d’API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | L’identifiant de spécification de connexion qui correspond à [!DNL Data Landing Zone]. Cet ID fixe est : `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Type de l’objet auquel vous souhaitez accéder. | `file` |
| `{OBJECT}` | Chemin et nom de l’objet auquel vous souhaitez accéder. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Type du fichier. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Une valeur boolean qui définit si l’aperçu du fichier est pris en charge. | </ul><li>`true`</li><li>`false`</li></ul> |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du fichier interrogé, y compris les noms de table et les types de données.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

## Création d’une connexion source

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et l’identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation IMS.

Pour créer une connexion source, envoyez une requête de POST au point de terminaison `/sourceConnections` de l’API [!DNL Flow Service].


**Format d’API**

```http
POST /sourceConnections
```

**Requête**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| Propriété | Description |
| --- | --- |
| `name` | Nom de la connexion source [!DNL Data Landing Zone]. |
| `data.format` | Le format des données que vous souhaitez importer dans Platform. |
| `params.path` | Le chemin d’accès au fichier que vous souhaitez apporter à Platform. |
| `connectionSpec.id` | L’identifiant de spécification de connexion qui correspond à [!DNL Data Landing Zone]. Cet ID fixe est : `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la connexion source nouvellement créée. Cet identifiant est requis dans le tutoriel suivant pour créer un flux de données.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez récupéré vos [!DNL Data Landing Zone] informations d’identification, exploré sa structure de fichiers pour trouver le fichier que vous souhaitez importer dans Platform et créé une connexion source pour commencer à apporter vos données à Platform. Vous pouvez maintenant passer au tutoriel suivant, dans lequel vous apprendrez à [créer un flux de données pour importer les données de stockage dans le cloud vers Platform à l’aide de l’ [!DNL Flow Service] API](../../collect/cloud-storage.md).

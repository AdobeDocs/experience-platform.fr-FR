---
keywords: Experience Platform;accueil;rubriques populaires;
solution: Experience Platform
title: Connexion d’une zone d’entrée de données à Adobe Experience Platform à l’aide de l’API Flow Service
type: Tutorial
description: Découvrez comment connecter Adobe Experience Platform à Data Landing Zone à l’aide de l’API Flow Service.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 20%

---

# Connexion [!DNL Data Landing Zone] vers Adobe Experience Platform à l’aide de l’API Flow Service

[!DNL Data Landing Zone] est une fonctionnalité sécurisée de stockage de fichiers dans le cloud pour importer des fichiers dans Adobe Experience Platform. Les données sont automatiquement supprimées de la variable [!DNL Data Landing Zone] après sept jours.

Ce tutoriel vous guide tout au long des étapes de création d’un [!DNL Data Landing Zone] connexion source à l’aide de la fonction [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Ce tutoriel fournit également des instructions sur la manière de récupérer votre [!DNL Data Landing Zone], ainsi que d’afficher et d’actualiser vos informations d’identification.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuelles qui divisent une instance de plateforme unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience numérique.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour créer une [!DNL Data Landing Zone] connexion source à l’aide de la fonction [!DNL Flow Service] API.

Ce tutoriel nécessite également que vous lisiez le guide sur [Prise en main des API Platform](../../../../../landing/api-guide.md) pour apprendre à s’authentifier auprès des API de Platform et interpréter les exemples d’appels fournis dans la documentation.

## Récupération d’une zone d’entrée utilisable

La première étape de l’utilisation des API pour accéder à [!DNL Data Landing Zone] est d’effectuer une requête de GET à la variable `/landingzone` point d’entrée du [!DNL Connectors] API lors de la fourniture `type=user_drop_zone` dans l’en-tête de votre requête.

**Format d’API**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| En-têtes | Description |
| --- | --- |
| `user_drop_zone` | Le `user_drop_zone` type permet à l’API de distinguer un conteneur de zone d’entrée des autres types de conteneurs disponibles. |

**Requête**

La requête suivante récupère une zone d’entrée existante.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Réponse**

La réponse suivante renvoie des informations sur une zone d’entrée, y compris sur la zone correspondante. `containerName` et `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Nom de la zone d’entrée que vous avez récupérée. |
| `containerTTL` | Délai d’expiration (en jours) appliqué à vos données dans la zone d’entrée. Tout ce qui se trouve dans une zone d’entrée donnée est supprimé au bout de sept jours. |

## Récupération [!DNL Data Landing Zone] informations

Pour récupérer les informations d’identification d’un [!DNL Data Landing Zone], effectuez une requête de GET à la fonction `/credentials` point d’entrée du [!DNL Connectors] API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

La réponse suivante renvoie les informations d’identification pour votre zone d’entrée, y compris votre `SASToken` et `SASUri`, ainsi que la variable `storageAccountName` qui correspond au conteneur de votre zone d’entrée.

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


## Mettre à jour [!DNL Data Landing Zone] informations

Vous pouvez mettre à jour votre `SASToken` en envoyant une requête de POST à la variable `/credentials` point d’entrée du [!DNL Connectors] API.

**Format d’API**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| En-têtes | Description |
| --- | --- |
| `user_drop_zone` | Le `user_drop_zone` type permet à l’API de distinguer un conteneur de zone d’entrée des autres types de conteneurs disponibles. |
| `refresh` | Le `refresh` vous permet de réinitialiser les informations d’identification de votre zone d’entrée et de générer automatiquement une nouvelle `SASToken`. |

**Requête**

La requête suivante met à jour les informations d’identification de votre zone d’entrée.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Réponse**

La réponse suivante renvoie les valeurs mises à jour pour votre `SASToken` et `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Explorez la structure et le contenu des fichiers de la zone d’entrée

Vous pouvez explorer la structure des fichiers et le contenu de votre zone d’entrée en adressant une demande de GET au `connectionSpecs` point d’entrée du [!DNL Flow Service] API.

**Format d’API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Paramètre | Description |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | Identifiant de spécification de connexion qui correspond à [!DNL Data Landing Zone]. Cet ID fixe est `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Requête**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie un tableau de fichiers et de dossiers trouvés dans le répertoire interrogé. Prenez note de la `path` du fichier que vous souhaitez charger, car vous devez le fournir à l’étape suivante pour examiner sa structure.

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
| `{CONNECTION_SPEC_ID}` | Identifiant de spécification de connexion qui correspond à [!DNL Data Landing Zone]. Cet ID fixe est `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du fichier interrogé, y compris les noms de fichier et les types de données.

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

### Utilisation `determineProperties` pour détecter automatiquement les informations de propriété de fichier d’une [!DNL Data Landing Zone]

Vous pouvez utiliser la variable `determineProperties` pour détecter automatiquement les informations de propriété du contenu du fichier de votre [!DNL Data Landing Zone] lors d’un appel de GET pour explorer le contenu et la structure de votre source.

#### `determineProperties` cas d’utilisation

Le tableau suivant décrit les différents scénarios que vous pouvez rencontrer lors de l’utilisation de la variable `determineProperties` paramètre de requête ou en fournissant manuellement des informations sur votre fichier.

| `determineProperties` | `queryParams` | Réponse |
| --- | --- | --- |
| True | S/O | If `determineProperties` est fourni en tant que paramètre de requête, puis la détection des propriétés du fichier se produit et la réponse renvoie un nouveau `properties` clé contenant des informations sur le type de fichier, le type de compression et le délimiteur de colonne. |
| S/O | True | Si les valeurs du type de fichier, du type de compression et du délimiteur de colonne sont fournies manuellement dans la variable `queryParams`, elles sont ensuite utilisées pour générer le schéma et les mêmes propriétés sont renvoyées dans le cadre de la réponse. |
| True | True | Si les deux options sont effectuées simultanément, une erreur est renvoyée. |
| S.O. | S.O. | Si aucune des deux options n’est fournie, une erreur est renvoyée, car il n’existe aucun moyen d’obtenir les propriétés de la réponse. |

**Format d’API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `determineProperties` | Ce paramètre de requête permet à la variable [!DNL Flow Service] API permettant de détecter des informations concernant les propriétés de votre fichier, notamment des informations sur le type de fichier, le type de compression et le délimiteur de colonne. | `true` |

**Requête**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

Une réponse réussie renvoie la structure du fichier interrogé, y compris les noms de fichier et les types de données, ainsi qu’un `properties` clé, contenant des informations sur `fileType`, `compressionType`, et `columnDelimiter`.

+++Cliquez sur moi

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| Propriété | Description |
| --- | --- |
| `properties.fileType` | Le type de fichier correspondant au fichier interrogé. Les types de fichiers pris en charge sont les suivants : `delimited`, `json`, et `parquet`. |
| `properties.compressionType` | Type de compression correspondant utilisé pour le fichier interrogé. Les types de compression pris en charge sont les suivants : <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Délimiteur de colonne correspondant utilisé pour le fichier interrogé. Toute valeur de caractère unique est un délimiteur de colonne autorisé. La valeur par défaut est une virgule. `(,)`. |


## Créer une connexion source

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et l’identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation IMS.

Pour créer une connexion source, envoyez une requête POST au point d’entrée `/sourceConnections` de l’API [!DNL Flow Service].


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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Le nom de votre [!DNL Data Landing Zone] connexion source. |
| `data.format` | Le format des données que vous souhaitez importer dans Platform. |
| `params.path` | Le chemin d’accès au fichier que vous souhaitez apporter à Platform. |
| `connectionSpec.id` | Identifiant de spécification de connexion qui correspond à [!DNL Data Landing Zone]. Cet ID fixe est `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Réponse**

Une réponse réussie renvoie l’identifiant unique (`id`) de la nouvelle connexion source. Le tutoriel suivant requiert cet ID pour créer un flux de données.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Étapes suivantes

En suivant ce tutoriel, vous avez récupéré votre [!DNL Data Landing Zone] informations d’identification, explorez sa structure de fichiers pour trouver le fichier que vous souhaitez importer dans Platform, et créez une connexion source pour commencer à importer vos données dans Platform. Vous pouvez maintenant passer au tutoriel suivant, dans lequel vous apprendrez à [créez un flux de données pour importer des données de stockage dans le cloud vers Platform à l’aide de la variable [!DNL Flow Service] API](../../collect/cloud-storage.md).

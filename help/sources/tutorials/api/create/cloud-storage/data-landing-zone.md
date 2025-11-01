---
title: Connecter Data Landing Zone à Adobe Experience Platform à l’aide de l’API Flow Service
description: Découvrez comment connecter Adobe Experience Platform à Data Landing Zone à l’aide de l’API Flow Service.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '1417'
ht-degree: 13%

---

# Connecter [!DNL Data Landing Zone] à Adobe Experience Platform à l’aide de l’API Flow Service

>[!IMPORTANT]
>
>Cette page est spécifique au connecteur [!DNL Data Landing Zone] *source* d’Experience Platform. Pour plus d’informations sur la connexion au connecteur [!DNL Data Landing Zone] *destination*, consultez la page de documentation [[!DNL Data Landing Zone] destination](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] est une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud permettant d’importer des fichiers dans Adobe Experience Platform. Les données sont automatiquement supprimées du [!DNL Data Landing Zone] au bout de sept jours.

Ce tutoriel vous guide tout au long des étapes nécessaires à la création d’une connexion source [!DNL Data Landing Zone] à l’aide de l’[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Ce tutoriel explique également comment récupérer vos [!DNL Data Landing Zone], ainsi qu’afficher et actualiser vos informations d’identification.

## Prise en main

Ce guide nécessite une compréhension professionnelle des composants suivants d’Experience Platform :

* [Sources](../../../../home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md) : Experience Platform fournit des sandbox virtuels qui divisent une instance Experience Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

Ce tutoriel nécessite également que vous lisiez le guide [Prise en main des API d’Experience Platform](../../../../../landing/api-guide.md) pour apprendre à vous authentifier auprès des API d’Experience Platform et à interpréter les exemples d’appels fournis dans la documentation.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin afin de créer une connexion source [!DNL Data Landing Zone] à l’aide de l’API [!DNL Flow Service].

## Récupération d’une zone d’atterrissage utilisable

>[!IMPORTANT]
>
>Vous devez disposer de l’autorisation de contrôle d’accès **[!UICONTROL Manage Sources]** pour utiliser les API [!DNL Data Landing Zone] et récupérer des `type=user_drop_zone`. Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../../../../access-control/home.md) ou contactez l’administrateur de votre produit pour obtenir les autorisations requises.

La première étape de l’utilisation des API pour accéder aux [!DNL Data Landing Zone] consiste à envoyer une requête GET au point d’entrée `/landingzone` de l’API [!DNL Connectors] tout en fournissant des `type=user_drop_zone` dans l’en-tête de votre requête.

**Format d’API**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| En-têtes | Description |
| --- | --- |
| `user_drop_zone` | Le type `user_drop_zone` permet à l’API de distinguer un conteneur de zone d’atterrissage des autres types de conteneurs disponibles. |

**Requête**

La requête suivante récupère une zone d’atterrissage existante.

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

Selon votre fournisseur, une requête réussie renvoie les éléments suivants :

>[!BEGINTABS]

>[!TAB Réponse sur Azure ]

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Nom de la zone d’atterrissage que vous avez récupéré. |
| `containerTTL` | Délai d’expiration (en jours) appliqué à vos données dans la zone d’atterrissage. Tout élément situé dans une zone d’atterrissage donnée est supprimé au bout de sept jours. |


>[!TAB Réponse sur AWS]

```json
{
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "dlz-adf-connectors"
  },
  "dataTTL": {
    "timeUnit": "days",
    "timeQuantity": 7
  },
  "dlzProvider": "Amazon S3"
}
```

>[!ENDTABS]


## Récupération des informations d’identification [!DNL Data Landing Zone]

Pour récupérer les informations d’identification d’un [!DNL Data Landing Zone], envoyez une requête GET au point d’entrée `/credentials` de l’API [!DNL Connectors].

**Format d’API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**Requête**

L’exemple de requête suivant récupère les informations d’identification d’une zone d’atterrissage existante.

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

Selon votre fournisseur, une requête réussie renvoie les éléments suivants :

>[!BEGINTABS]

>[!TAB Réponse sur Azure ]

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| Propriété | Description |
| --- | --- |
| `containerName` | Nom de votre [!DNL Data Landing Zone]. |
| `SASToken` | Jeton de signature d’accès partagé pour votre [!DNL Data Landing Zone]. Cette chaîne contient toutes les informations nécessaires pour autoriser une requête. |
| `storageAccountName` | Nom de votre compte de stockage. |
| `SASUri` | URI de signature d’accès partagé pour votre [!DNL Data Landing Zone]. Cette chaîne est une combinaison de l’URI du [!DNL Data Landing Zone] auquel vous êtes authentifié et de son jeton SAS correspondant. |
| `expiryDate` | Date d’expiration de votre jeton SAS. Vous devez actualiser votre jeton avant la date d’expiration pour continuer à l’utiliser dans votre application pour charger des données vers le [!DNL Data Landing Zone]. Si vous n’actualisez pas manuellement votre jeton avant la date d’expiration indiquée, il s’actualisera automatiquement et fournira un nouveau jeton lorsque l’appel des informations d’identification GET sera effectué. |

>[!TAB Réponse sur AWS]

```json
{
  "credentials": {
    "clientId": "example-client-id",
    "awsAccessKeyId": "example-access-key-id",
    "awsSecretAccessKey": "example-secret-access-key",
    "awsSessionToken": "example-session-token"
  },
  "dlzPath": {
    "bucketName": "dlz-prod-sandboxName",
    "dlzFolder": "user_drop_zone"
  },
  "dlzProvider": "Amazon S3",
  "expiryTime": 1735689599
}
```

| Propriété | Description |
| --- | --- |
| `credentials.clientId` | Identifiant client de votre [!DNL Data Landing Zone] dans AWS. |
| `credentials.awsAccessKeyId` | Identifiant de clé d’accès de votre [!DNL Data Landing Zone] dans AWS. |
| `credentials.awsSecretAccessKey` | Clé d’accès secrète de votre [!DNL Data Landing Zone] dans AWS. |
| `credentials.awsSessionToken` | Votre jeton de session AWS. |
| `dlzPath.bucketName` | Nom de votre compartiment AWS. |
| `dlzPath.dlzFolder` | Le dossier [!DNL Data Landing Zone] auquel vous accédez. |
| `dlzProvider` | Fournisseur [!DNL Data Landing Zone] que vous utilisez. Pour Amazon, cela sera [!DNL Amazon S3]. |
| `expiryTime` | Heure d’expiration en heure Unix. |

>[!ENDTABS]

### Récupérer les champs requis à l’aide d’API

Une fois que vous avez généré votre jeton, vous pouvez récupérer les champs requis par programmation à l’aide des exemples de requête ci-dessous :

>[!BEGINTABS]

>[!TAB Python]

```py
import requests
 
# API endpoint
url = "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone"
 
headers = {
    "Authorization": "{TOKEN}",
    "Content-Type": "application/json",
    "x-gw-ims-org-id": "{ORG_ID}",
    "x-api-key": "{API_KEY}"
}
 
# Send GET request to the API
response = requests.get(url, headers=headers)
 
# Check if the request was successful
if response.status_code == 200:
    # Parse the response as JSON (if applicable)
    data = response.json()
 
    # Print or work with the fetched data 
    print(" Sas Token:", data['SASToken'])
    print(" Container Name:",  data['containerName'])
    print("\n")
 
else:
    # Print an error message if the request failed
    print(f"Failed to fetch data. Status code: {response.status_code}")
    print(f"Response: {response.text}")
```

>[!TAB Java]


```java
package org.example;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
 
import org.apache.http.HttpResponse;
import org.apache.http.client.ClientProtocolException;
import org.apache.http.client.methods.HttpGet;
import org.apache.http.impl.client.DefaultHttpClient;
 
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;
 
public class Main {
    public static void main(String[] args) {
 
        ObjectMapper objectMapper = new ObjectMapper();
 
        try {
 
            DefaultHttpClient httpClient = new DefaultHttpClient();
            HttpGet getRequest = new HttpGet(
                "https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone");
            getRequest.addHeader("accept", "application/json");
            getRequest.addHeader("Authorization","<TOKEN>");
            getRequest.addHeader("Content-Type", "application/json");
            getRequest.addHeader("x-gw-ims-org-id", "<ORG_ID>");
            getRequest.addHeader("x-api-key", "<API_KEY>");
 
            HttpResponse response = httpClient.execute(getRequest);
 
            if (response.getStatusLine().getStatusCode() != 200) {
                throw new RuntimeException("Failed : HTTP error code : "
                    + response.getStatusLine().getStatusCode());
            }
 
            final JsonNode jsonResponse = objectMapper.readTree(response.getEntity().getContent());
 
            System.out.println("\nOutput from API Response .... \n");
            System.out.printf("ContainerName: %s%n", jsonResponse.at("/containerName").textValue());
            System.out.printf("SASToken: %s%n", jsonResponse.at("/SASToken").textValue());
 
            httpClient.getConnectionManager().shutdown();
 
        } catch (ClientProtocolException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

>[!ENDTABS]


## Mettre à jour les informations d’identification [!DNL Data Landing Zone]

Vous pouvez mettre à jour votre `SASToken` en effectuant une requête POST vers le point d’entrée `/credentials` de l’API [!DNL Connectors].

**Format d’API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| En-têtes | Description |
| --- | --- |
| `user_drop_zone` | Le type `user_drop_zone` permet à l’API de distinguer un conteneur de zone d’atterrissage des autres types de conteneurs disponibles. |
| `refresh` | L’action `refresh` vous permet de réinitialiser les informations d’identification de votre zone d’atterrissage et de générer automatiquement une nouvelle `SASToken`. |

**Requête**

La requête suivante met à jour vos informations d’identification de zone d’atterrissage.

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

La réponse suivante renvoie des valeurs mises à jour pour vos `SASToken` et `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## Explorer la structure et le contenu du fichier de zone d’atterrissage

Vous pouvez explorer la structure de fichiers et le contenu de votre zone d’atterrissage en envoyant une requête GET au point d’entrée `connectionSpecs` de l’API [!DNL Flow Service].

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

Une réponse réussie renvoie un tableau de fichiers et de dossiers trouvés dans le répertoire interrogé. Notez la propriété `path` du fichier que vous souhaitez charger, car vous devez la fournir à l’étape suivante pour examiner sa structure.

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

## Prévisualiser la structure et le contenu du fichier de zone d’atterrissage

Pour inspecter la structure d’un fichier dans votre zone d’atterrissage, effectuez une requête GET tout en fournissant le chemin d’accès au fichier et saisissez comme paramètre de requête.

**Format d’API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | Identifiant de spécification de connexion qui correspond à [!DNL Data Landing Zone]. Cet ID fixe est `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |  |
| `{OBJECT_TYPE}` | Type de l’objet auquel vous souhaitez accéder. | `file` |
| `{OBJECT}` | Chemin d’accès et nom de l’objet auquel vous souhaitez accéder. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Type du fichier. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Valeur booléenne qui définit si l’aperçu du fichier est pris en charge. | </ul><li>`true`</li><li>`false`</li></ul> |

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

### Utilisation de `determineProperties` pour détecter automatiquement les informations de propriété de fichier d’un [!DNL Data Landing Zone]

Vous pouvez utiliser le paramètre `determineProperties` pour détecter automatiquement les informations de propriété du contenu du fichier de votre [!DNL Data Landing Zone] lors d’un appel GET visant à explorer le contenu et la structure de votre source.

#### `determineProperties` cas d’utilisation

Le tableau suivant décrit les différents scénarios que vous pouvez rencontrer lors de l’utilisation du paramètre de requête `determineProperties` ou de la fourniture manuelle d’informations sur votre fichier .

| `determineProperties` | `queryParams` | Réponse |
| --- | --- | --- |
| True | S/O | Si `determineProperties` est fourni comme paramètre de requête, la détection des propriétés du fichier se produit et la réponse renvoie une nouvelle clé de `properties` qui inclut des informations sur le type de fichier, le type de compression et le délimiteur de colonne. |
| S/O | True | Si les valeurs du type de fichier, du type de compression et du délimiteur de colonne sont fournies manuellement dans le cadre de `queryParams`, elles sont utilisées pour générer le schéma et les mêmes propriétés sont renvoyées dans le cadre de la réponse. |
| True | True | Si les deux options sont effectuées simultanément, une erreur est renvoyée. |
| S.O. | S.O. | Si aucune des deux options n’est fournie, une erreur est renvoyée, car il n’existe aucun moyen d’obtenir des propriétés pour la réponse. |

**Format d’API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Paramètre | Description | Exemple |
| --- | --- | --- |
| `determineProperties` | Ce paramètre de requête permet à l’API [!DNL Flow Service] de détecter des informations concernant les propriétés de votre fichier , y compris des informations sur le type de fichier, le type de compression et le délimiteur de colonne. | `true` |

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

Une réponse réussie renvoie la structure du fichier interrogé, y compris les noms de fichier et les types de données, ainsi qu’une clé `properties`, contenant des informations sur les `fileType`, les `compressionType` et les `columnDelimiter`.

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
| `properties.fileType` | Type de fichier correspondant au fichier interrogé. Les types de fichiers pris en charge sont les suivants : `delimited`, `json` et `parquet`. |
| `properties.compressionType` | Type de compression correspondant utilisé pour le fichier interrogé. Les types de compression pris en charge sont les suivants : <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | Le délimiteur de colonne correspondant utilisé pour le fichier interrogé. Toute valeur de caractère unique est un délimiteur de colonne autorisé. La valeur par défaut est une `(,)`. |


## Créer une connexion source

Une connexion source crée et gère la connexion à la source externe à partir de laquelle les données sont ingérées. Une connexion source se compose d’informations telles que la source de données, le format de données et l’identifiant de connexion source nécessaires à la création d’un flux de données. Une instance de connexion source est spécifique à un client et à une organisation.

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
| `name` | Nom de votre connexion source [!DNL Data Landing Zone]. |
| `data.format` | Format des données à importer dans Experience Platform. |
| `params.path` | Chemin d’accès au fichier à importer dans Experience Platform. |
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

En suivant ce tutoriel, vous avez récupéré vos informations d’identification [!DNL Data Landing Zone], exploré sa structure de fichiers pour trouver le fichier que vous souhaitez importer dans Experience Platform et créé une connexion source pour commencer à importer vos données dans Experience Platform. Vous pouvez maintenant passer au tutoriel suivant, où vous apprendrez à [créer un flux de données pour importer des données d’espace de stockage dans Experience Platform à l’aide de l’API [!DNL Flow Service] &#x200B;](../../collect/cloud-storage.md).

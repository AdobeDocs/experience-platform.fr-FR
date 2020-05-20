---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Création d’intégrations ETL
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3
workflow-type: tm+mt
source-wordcount: '4227'
ht-degree: 0%

---


# Développement d’intégrations ETL pour Adobe Experience Platform

Le guide d’intégration ETL décrit les étapes générales à suivre pour créer des connecteurs sécurisés et hautes performances pour la plate-forme d’expérience et intégrer des données dans la plate-forme.


- [Catalogue](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [Accès aux données](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [Incorporation de données](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [API d’authentification et d’autorisation](../tutorials/authentication.md)
- [Registre des Schémas](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

Ce guide comprend également des exemples d’appels d’API à utiliser lors de la conception d’un connecteur ETL, ainsi que des liens vers la documentation qui décrit chaque service Experience Platform et l’utilisation de son API, de manière plus détaillée.

Un exemple d&#39;intégration est disponible sur GitHub via le code [de référence d&#39;intégration de l&#39;écosystème](https://github.com/adobe/acp-data-services-etl-reference) ETL sous Apache License Version 2.0.

## Workflow

Le diagramme de flux de travaux suivant présente un aperçu général de l’intégration des composants d’Adobe Experience Platform à une application et un connecteur ETL.

![](images/etl.png)

## Composants d’Adobe Experience Platform

Plusieurs composants Experience Platform sont impliqués dans les intégrations de connecteur ETL. La liste suivante présente plusieurs composants et fonctionnalités clés :

- **Adobe Identity Management System (IMS)** - Fournit une structure d’authentification des services Adobe.
- **Organisation** IMS - Entité corporative qui peut détenir ou concéder des licences sur des produits et services et permettre l&#39;accès à ses membres.
- **Utilisateur** IMS - Membres d&#39;une organisation IMS. La relation Organisation-utilisateur est multiple pour plusieurs.
- **Sandbox** - Une partition virtuelle une instance de plateforme unique, pour aider à développer et à développer des applications d&#39;expérience numérique.
- **Détection** des données : enregistre les métadonnées des données imbriquées et transformées dans la plate-forme d’expérience.
- **Accès aux** données : fournit aux utilisateurs une interface pour accéder à leurs données dans la plate-forme d’expérience.
- **Ingestion** des données : envoie les données vers la plate-forme d’expérience avec les API d’ingestion des données.
- **Registre** des Schémas : définit et stocke le schéma qui décrit la structure des données à utiliser dans la plateforme d’expérience.

## Prise en main des API de plateforme d’expérience

Les sections suivantes contiennent des informations supplémentaires que vous devez connaître ou connaître pour pouvoir invoquer les API de plateforme d’expérience.

### Lecture des exemples d’appels d’API

Ce guide fournit des exemples d’appels d’API pour montrer comment formater vos requêtes. Il s’agit notamment des chemins d’accès, des en-têtes requis et des charges de requête correctement formatées. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section sur [comment lire des exemples d’appels](../landing/troubleshooting.md#how-do-i-format-an-api-request) d’API dans le guide de dépannage d’Experience Platform.

### Rassembler les valeurs des en-têtes requis

Pour lancer des appels aux API de plateforme, vous devez d’abord suivre le didacticiel [d’](../tutorials/authentication.md)authentification. Le didacticiel d’authentification fournit les valeurs de chacun des en-têtes requis dans tous les appels d’API de plateforme d’expérience, comme indiqué ci-dessous :

- Autorisation : Porteur `{ACCESS_TOKEN}`
- x-api-key : `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Toutes les ressources de la plate-forme d’expérience sont isolées dans des sandbox virtuels spécifiques. Toutes les requêtes d’API de plateforme nécessitent un en-tête spécifiant le nom du sandbox dans lequel l’opération aura lieu :

- x-sandbox-name : `{SANDBOX_NAME}`

>[!NOTE] Pour plus d’informations sur les sandbox dans Platform, voir la documentation [d’aperçu de](../sandboxes/home.md)sandbox.

Toutes les requêtes qui contiennent une charge utile (POST, PUT, PATCH) nécessitent un en-tête supplémentaire :

- Content-Type : application/json

## Flux utilisateur général

Pour commencer, un utilisateur ETL se connecte à l’interface utilisateur de la plate-forme d’expérience et crée des jeux de données à assimiler à l’aide d’un connecteur standard ou d’un connecteur de service Push.

Dans l’interface utilisateur, l’utilisateur crée le jeu de données de sortie en sélectionnant un schéma de jeu de données. Le choix du schéma dépend du type de données (enregistrements ou séries chronologiques) ingérées dans la plate-forme. En cliquant sur l&#39;onglet Schémas de l&#39;interface utilisateur, l&#39;utilisateur peut vue tous les schémas disponibles, y compris le type de comportement pris en charge par le schéma.

Dans l’outil ETL, l’utilisateur début la conception de ses transformations de mappage après avoir configuré la connexion appropriée (à l’aide de ses informations d’identification). L’outil ETL est supposé disposer déjà de connecteurs Experience Platform installés (processus non défini dans ce guide d’intégration).

Des maquettes pour un exemple d’outil et de processus ETL ont été fournies dans le flux de travail [](./workflow.md)ETL. Bien que le format des outils ETL puisse être différent, la plupart présentent des fonctionnalités similaires.

>[!NOTE] Le connecteur ETL doit spécifier un filtre d&#39;horodatage marquant la date d&#39;assimilation des données et le décalage (c&#39;est-à-dire la fenêtre pour laquelle les données doivent être lues). L’outil ETL doit prendre en charge la prise en charge de ces deux paramètres dans cette interface utilisateur ou dans une autre interface utilisateur appropriée. Dans Adobe Experience Platform, ces paramètres sont associés à des dates disponibles (le cas échéant) ou à des dates capturées présentes dans l’objet batch du jeu de données.

### liste de Vue des jeux de données

En utilisant la source de données pour le mappage, une liste de tous les jeux de données disponibles peut être récupérée à l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalogue.

Vous pouvez émettre une seule requête d’API pour vue tous les jeux de données disponibles (ex. `GET /dataSets`), la meilleure pratique étant d’inclure des paramètres de requête qui limitent la taille de la réponse.

Dans les cas où des informations _complètes_ sur les jeux de données sont demandées, la charge utile de réponse peut dépasser 3 Go, ce qui peut ralentir les performances globales. Par conséquent, l’utilisation de paramètres de requête pour filtrer uniquement les informations nécessaires rendra les requêtes de catalogue plus efficaces.

#### Filtrage des Listes

Lors du filtrage des réponses, vous pouvez utiliser plusieurs filtres dans un seul appel en séparant les paramètres par une esperluette (`&`). Certains paramètres de requête acceptent des listes de valeurs séparées par des virgules, comme le filtre &quot;propriétés&quot; dans l’exemple de requête ci-dessous.

Les réponses du catalogue sont automatiquement mesurées en fonction des limites configurées, mais le paramètre de requête &quot;limite&quot; peut être utilisé pour personnaliser les contraintes et limiter le nombre d’objets renvoyés. Les limites de réponse du catalogue préconfiguré sont les suivantes :

- Si aucun paramètre de limite n’est spécifié, le nombre maximal d’objets par charge utile de réponse est de 20.
- La limite globale pour toutes les autres requêtes de catalogue est de 100 objets.
- Pour les requêtes de jeux de données, si observableSchema est demandé à l’aide du paramètre de requête de propriétés, le nombre maximal de jeux de données renvoyé est 20.
- Les paramètres de limite non valides (y compris `limit=0`) sont satisfaits avec une erreur HTTP 400 qui décrit les plages appropriées.
- Si des limites ou des décalages sont transmis en tant que paramètres de requête, ils sont prioritaires sur ceux transmis en tant qu’en-têtes.

Les paramètres de Requête sont traités plus en détail dans la présentation [du service de](../catalog/home.md)catalogue.

**Format d’API**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Consultez la présentation [du service de](../catalog/home.md) catalogue pour obtenir des exemples détaillés sur la manière d’appeler l’API [de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)catalogue.

**Réponse**

La réponse comprend trois (`limit=3`) jeux de données qui affichent &quot;name&quot;, &quot;description&quot; et &quot;schemaRef&quot;, comme indiqué par le paramètre `properties` de requête.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### schéma de jeu de données de Vue

La propriété &quot;schemaRef&quot; d’un jeu de données contient un URI référençant le schéma XDM sur lequel le jeu de données est basé. Le schéma XDM (&quot;schemaRef&quot;) représente tous les champs _potentiels_ qui pourraient être utilisés par le jeu de données, pas nécessairement les champs qui _sont_ utilisés (voir &quot;observableSchema&quot; ci-dessous).

Le schéma XDM est le schéma que vous utilisez lorsque vous devez présenter à l&#39;utilisateur une liste de tous les champs disponibles sur lesquels il est possible d&#39;écrire.

La première valeur &quot;schemaRef.id&quot; de l’objet de réponse précédent (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) est un URI qui pointe vers un schéma XDM spécifique dans le registre des Schémas. Le schéma peut être récupéré en adressant une demande de recherche (GET) à l&#39;API de registre du Schéma.

>[!NOTE] La propriété &quot;schemaRef&quot; remplace la propriété désormais obsolète &quot;schéma&quot;. Si &quot;schemaRef&quot; est absent du jeu de données ou ne contient pas de valeur, vous devez vérifier la présence d’une propriété &quot;schéma&quot;. Pour ce faire, remplacez &quot;schemaRef&quot; par &quot;schéma&quot; dans le paramètre de `properties` requête de l’appel précédent. Pour plus d&#39;informations sur la propriété &quot;schéma&quot;, consultez la section Propriétés [&quot;schéma&quot; du jeu de](#dataset-schema-property-deprecated---eol-2019-05-30) données qui suit.

**Format d’API**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Requête**

La requête utilise l’ `id` URI codée en URL du schéma (valeur de l’attribut &quot;schemaRef.id&quot;) et requiert un en-tête Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

Le format de réponse dépend du type d’en-tête Accepter envoyé dans la requête. Les requêtes de recherche doivent également `version` être incluses dans l’en-tête Accepter. Le tableau suivant présente les en-têtes Accepter disponibles pour les recherches :

| Accepter | Description |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Demandes, titres, identifiants et versions de Liste (GET) |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs et allOf résolus, avec titres et descriptions |
| `application/vnd.adobe.xed+json; version={major version}` | Brut avec $ref et allOf, avec titres et descriptions |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Brut avec $ref et allOf, sans titre ni description |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs et allOf résolus, aucun titre ou description |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs et allOf résolus, descripteurs inclus |

>[!NOTE] `application/vnd.adobe.xed-id+json` et `application/vnd.adobe.xed-full+json; version={major version}` sont les en-têtes Accept les plus couramment utilisés. `application/vnd.adobe.xed-id+json` est préférable pour la liste des ressources dans le registre des Schémas, car elle ne renvoie que les valeurs &quot;titre&quot;, &quot;id&quot; et &quot;version&quot;. `application/vnd.adobe.xed-full+json; version={major version}` est préférable pour l’affichage d’une ressource spécifique (par son &quot;id&quot;), car elle renvoie tous les champs (imbriqués sous &quot;properties&quot;), ainsi que les titres et descriptions.

**Réponse**

Le schéma JSON renvoyé décrit la structure et les informations au niveau du champ (&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot;, etc.) des données, sérialisées en tant que JSON. Si vous utilisez un format de sérialisation autre que JSON pour l’assimilation (tel que Parquet ou Scala), le Guide [du registre des](../xdm/tutorials/create-schema-api.md) Schémas contient un tableau présentant le type JSON souhaité (&quot;meta:xdmType&quot;) et sa représentation correspondante dans d’autres formats.

Outre ce tableau, le Guide du développeur du registre de Schéma contient des exemples détaillés de tous les appels possibles qui peuvent être effectués à l&#39;aide de l&#39;API du registre de Schéma.

### Propriété du jeu de données &quot;schéma&quot; (DEPRECATED - EOL 2019-05-30)

Les jeux de données peuvent contenir une propriété &quot;schéma&quot; qui est désormais obsolète et reste disponible temporairement pour une compatibilité ascendante. Par exemple, une demande de liste (GET) similaire à celle effectuée précédemment, où &quot;schéma&quot; a été remplacé par &quot;schemaRef&quot; dans le paramètre de `properties` requête, peut renvoyer les valeurs suivantes :

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Si la propriété &quot;schéma&quot; d’un jeu de données est renseignée, cela indique que le schéma est un `/xdms` schéma obsolète et, si elle est prise en charge, le connecteur ETL doit utiliser la valeur de la propriété &quot;schéma&quot; avec le point de terminaison `/xdms` (un point de terminaison obsolète dans l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog) pour récupérer le schéma hérité.

**Format d’API**

```http
GET /catalog/{"schema" property without the "@"}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE] Un paramètre de requête facultatif, `expansion=xdm`indique à l’API de développer entièrement et de mettre en ligne tous les schémas référencés. Pour ce faire, vous pouvez présenter à l’utilisateur une liste de tous les champs potentiels.

**Réponse**

Tout comme les étapes d’ [affichage du schéma](#view-dataset-schema)du jeu de données, la réponse contient un schéma JSON qui décrit la structure et les informations au niveau du champ des données, sérialisées en tant que JSON.

>[!NOTE] Lorsque le champ &quot;schéma&quot; est vide ou absent entièrement, le connecteur doit lire le champ &quot;schemaRef&quot; et utiliser l&#39;API [de registre de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) Schémas comme indiqué dans les étapes précédentes pour [vue d&#39;un schéma](#view-dataset-schema)de jeux de données.

### La propriété &quot;observableSchema&quot;

La propriété &quot;observableSchema&quot; d’un jeu de données possède une structure JSON correspondant à celle du JSON du schéma XDM. Le &quot;observableSchema&quot; contient les champs présents dans les fichiers d’entrée entrants. Lors de l’écriture de données sur la plateforme d’expérience, un utilisateur n’est pas tenu d’utiliser tous les champs du schéma de cible. Au lieu de cela, ils ne doivent fournir que les champs utilisés.

Le schéma observable est le schéma que vous utiliseriez si vous lisiez les données ou si vous présentiez une liste de champs disponibles pour lire/cartographier.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Données de Prévisualisation

L&#39;application ETL peut fournir une capacité de prévisualisation des données ([&quot;Figure 8&quot; dans le flux de travail](./workflow.md)ETL). L’API d’accès aux données propose plusieurs options pour les données de prévisualisation.

Vous trouverez des informations supplémentaires, notamment des instructions détaillées pour prévisualiser les données à l’aide de l’API d’accès aux données, dans le didacticiel [d’accès aux](../data-access/tutorials/dataset-data.md)données.

### Obtenir les détails d&#39;un jeu de données à l&#39;aide du paramètre de requête &quot;properties&quot;

Comme indiqué dans les étapes ci-dessus pour [vue d&#39;une liste de jeux de données](#view-list-of-datasets), vous pouvez demander des &quot;fichiers&quot; à l&#39;aide du paramètre de requête &quot;propriétés&quot;.

Pour obtenir des informations détaillées sur l’interrogation des jeux de données et des filtres de réponse disponibles, consultez la présentation [du service de](../catalog/home.md) catalogue.

**Format d’API**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Réponse**

La réponse comprend un jeu de données (`limit=1`) présentant la propriété &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Fichiers de jeu de données de Liste utilisant l’attribut &quot;files&quot;

Vous pouvez également utiliser une requête GET pour récupérer les détails des fichiers à l’aide de l’attribut &quot;files&quot;.

**Format d’API**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Réponse**

La réponse inclut l’ID de fichier de jeu de données en tant que propriété de niveau supérieur, avec les détails du fichier contenus dans l’objet ID de fichier de jeu de données.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Récupérer les détails du fichier

Les ID de fichier de jeu de données renvoyés dans la réponse précédente peuvent être utilisés dans une requête GET pour récupérer d&#39;autres détails de fichier via l&#39;API d&#39;accès aux données.

L’aperçu [de l’accès aux](../data-access/home.md) données contient des détails sur l’utilisation de l’API d’accès aux données.

**Format d’API**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Réponse**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Données du fichier de Prévisualisation

La propriété &quot;href&quot; peut être utilisée pour récupérer des données de prévisualisation via l’API [d’accès aux](../data-access/home.md)données.

**Format d’API**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

La réponse à la demande ci-dessus contient une prévisualisation du contenu du fichier.

Vous trouverez plus d’informations sur l’API d’accès aux données, y compris des demandes et réponses détaillées, dans l’aperçu [de l’accès aux](../data-access/home.md)données.

### Obtenir &quot;fileDescription&quot; du jeu de données

Le composant de destination comme sortie de données transformées, l’ingénieur de données choisira un jeu de données de sortie ([&quot;Figure 12&quot; dans le flux de travail](workflow.md)ETL). Le schéma XDM est associé au jeu de données de sortie. Les données à écrire seront identifiées par l&#39;attribut &quot;fileDescription&quot; de l&#39;entité de jeu de données des API de découverte de données. Ces informations peuvent être extraites à l’aide d’un ID de jeu de données (`{DATASET_ID}`). La propriété &quot;fileDescription&quot; de la réponse JSON fournit les informations demandées.

**Format d’API**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Propriété | Description |
| -------- | ----------- |
| `{DATASET_ID}` | Valeur `id` du jeu de données auquel vous tentez d’accéder. |

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Réponse**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

Les données seront écrites sur la plate-forme d’expérience à l’aide de l’API [d’administration de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)données.  L’écriture des données est un processus asynchrone. Lorsque des données sont écrites sur Adobe Experience Platform, un lot est créé et marqué comme une réussite uniquement une fois les données entièrement écrites.

Les données de la plate-forme Expérience doivent être écrites sous la forme de fichiers en parquet.

## Phase d’exécution

En tant que débuts d’exécution, le connecteur (tel que défini dans le composant source) lit les données de la plate-forme d’expérience à l’aide de l’API [d’accès aux](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)données. Le processus de transformation lit les données pour une certaine période. En interne, il requête des lots de jeux de données source. Lors de l’interrogation, il utilise des fichiers de date et de jeu de données de début paramétrés (variables pour les données de série chronologique ou incrémentielles) pour ces lots, ainsi que des débuts qui demandent des données pour ces fichiers de jeu de données.

### Exemples de transformations

L’ [exemple de document de transformations](./transformations.md) ETL contient un certain nombre d’exemples de transformations, notamment la gestion des identités et les mappages de type de données. Veuillez utiliser ces transformations à titre de référence.

### Lire les données de la plateforme d’expérience

A l’aide de l’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalogue, vous pouvez récupérer tous les lots entre une heure de début et une heure de fin spécifiées, puis les trier selon l’ordre dans lequel ils ont été créés.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Vous trouverez des informations détaillées sur le filtrage des lots dans le didacticiel [d’accès aux](../data-access/tutorials/dataset-data.md)données.

### Extraction de fichiers d’un lot

Une fois que vous disposez de l’ID du lot que vous recherchez (`{BATCH_ID}`), il est possible de récupérer une liste de fichiers appartenant à un lot spécifique via l’API [d’accès aux](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)données.  Pour plus d’informations, consultez le didacticiel [sur l’accès aux](../data-access/tutorials/dataset-data.md)données.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Accès aux fichiers à l’aide de l’ID de fichier

En utilisant l’identifiant unique d’un fichier (`{FILE_ID`), l’API [d’accès aux](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) données peut être utilisée pour accéder aux détails spécifiques du fichier, notamment son nom, sa taille en octets et un lien pour le télécharger.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

La réponse peut pointer vers un seul fichier ou un répertoire. Vous trouverez des informations détaillées sur chacun d&#39;eux dans le didacticiel [sur l&#39;accès aux](../data-access/tutorials/dataset-data.md)données.

### Accéder au contenu du fichier

L&#39;API [d&#39;accès aux](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) données permet d&#39;accéder au contenu d&#39;un fichier spécifique. Pour récupérer le contenu, une requête GET est effectuée à l’aide de la valeur renvoyée pour `_links.self.href` l’accès à un fichier à l’aide de l’ID de fichier.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

La réponse à cette demande contient le contenu du fichier. Pour plus d’informations, y compris des détails sur la pagination des réponses, voir le didacticiel [Comment Requête des données via l’API](../data-access/tutorials/dataset-data.md) d’accès aux données.

### Validation des enregistrements pour la conformité des schémas

Lors de l’écriture des données, les utilisateurs peuvent choisir de valider les données en fonction des règles de validation définies dans le schéma XDM. Pour plus d&#39;informations sur la validation de schéma, consultez le [ETL Ecosystem Integration Reference Code sur GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Si vous utilisez l&#39;implémentation de référence trouvée sur [GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), vous pouvez activer la validation de schéma dans cette implémentation à l&#39;aide de la propriété système `-DenableSchemaValidation=true`.

La validation peut être effectuée pour les types XDM logiques, à l’aide d’attributs tels que `minLength` et `maxlength` pour les chaînes, `minimum` et `maximum` pour les entiers, etc. Le guide [du développeur d&#39;API](../xdm/api/getting-started.md) Schéma Registry contient un tableau qui décrit les types XDM et les propriétés qui peuvent être utilisées pour la validation.

>[!NOTE] Les valeurs minimale et maximale fournies pour divers `integer` types sont les valeurs MIN et MAX que le type peut prendre en charge, mais ces valeurs peuvent être davantage limitées aux minimums et maximums de votre choix.

### Création d’un lot

Une fois les données traitées, l’outil ETL réécrit les données sur la plate-forme d’expérience à l’aide de l’API [d’administration](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)par lot. Avant de pouvoir ajouter des données à un jeu de données, celles-ci doivent être liées à un lot qui sera ultérieurement chargé dans un jeu de données spécifique.

**Requête**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Vous trouverez des informations détaillées sur la création d&#39;un lot, y compris des exemples de requêtes et de réponses, dans l&#39;aperçu [de l&#39;importation par](../ingestion/batch-ingestion/overview.md)lot.

### Écrire dans un jeu de données

Après avoir créé un nouveau lot, les fichiers peuvent être téléchargés vers un jeu de données spécifique. Plusieurs fichiers peuvent être publiés par lot jusqu’à ce qu’ils soient promus. Les fichiers peuvent être téléchargés à l’aide de l’API _de téléchargement de_ petits fichiers ; toutefois, si vos fichiers sont trop volumineux et que la limite de passerelle est dépassée, vous pouvez utiliser l’API _de téléchargement de fichiers_ volumineux. Vous trouverez des informations détaillées sur l&#39;utilisation des téléchargements de fichiers volumineux et petits dans l&#39;aperçu [de l&#39;importation](../ingestion/batch-ingestion/overview.md)par lot.

**Requête**

Les données de la plate-forme Expérience doivent être écrites sous la forme de fichiers en parquet.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Marquer le transfert par lot terminé

Une fois que tous les fichiers ont été téléchargés dans le lot, celui-ci peut être signalé comme étant terminé. Ce faisant, les entrées &quot;DataSetFile&quot; du catalogue sont créées pour les fichiers terminés et associées au lot généré. Le lot de catalogue est ensuite marqué comme ayant réussi, ce qui déclenche des flux en aval pour assimiler les données disponibles.

Les données arrivent d’abord à l’emplacement d’évaluation d’Adobe Experience Platform, puis sont déplacées vers l’emplacement final après le catalogage et la validation. Les lots sont marqués comme réussis une fois que toutes les données sont déplacées vers un emplacement permanent.

**Requête**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

En cas de réussite, la réponse renvoie HTTP Status 200 OK et le corps de la réponse est vide.

L&#39;outil ETL veillera à noter l&#39;horodatage des jeux de données source au fur et à mesure de la lecture des données.

Lors de la prochaine exécution de la transformation, probablement par appel de calendrier ou de événement, l’ETL début de demander les données de l’horodatage précédemment enregistré et toutes les données à venir.

### Obtenir l&#39;état du dernier lot

Avant d’exécuter de nouvelles tâches dans l’outil ETL, vous devez vous assurer que le dernier lot a bien été terminé. L’API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) Catalog Service fournit une option spécifique au lot qui fournit les détails des lots pertinents.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse**

De nouvelles tâches peuvent être planifiées si la valeur &quot;status&quot; du lot précédent est &quot;success&quot;, comme illustré ci-dessous :

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Obtenir le dernier état du lot par ID

Un statut de lot individuel peut être récupéré via l’API [du service de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catalogue en émettant une demande GET à l’aide du `{BATCH_ID}`. L’ `{BATCH_ID}` ID utilisé est identique à celui renvoyé lors de la création du lot.

**Requête**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Réponse - Réussite**

La réponse suivante indique un &quot;succès&quot; :

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Réponse - Échec**

En cas d&#39;échec, les &quot;erreurs&quot; peuvent être extraites de la réponse et apparues sur l&#39;outil ETL sous forme de messages d&#39;erreur.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Données et événements incrémentiels ou instantanés par rapport aux profils

Les données peuvent être représentées par deux matrices, comme suit :

| événements incrémentiels | profils incrémentiels |
|-------------------------------|----------------------|
| événements d&#39;instantané (moins probables) | profils d&#39;instantanés |

En règle générale, les données de Événement s’appliquent aux colonnes d’horodatage indexées de chaque ligne.

En règle générale, les données de Profil ne comportent pas d’horodatage et chaque ligne peut être identifiée par une clé primaire/composite.

Les données incrémentielles sont les seules données nouvelles ou mises à jour qui entrent dans le système et y sont ajoutées.

Les données de capture instantanée sont utilisées lorsque toutes les données entrent dans le système et remplacent certaines ou toutes les données précédentes d&#39;un jeu de données.

Dans le cas de événements incrémentiels, l&#39;outil ETL doit utiliser les dates disponibles/créer la date de l&#39;entité de lot. En cas de service Push, les dates disponibles ne seront pas présentes. L’outil utilisera donc la date créée/mise à jour par lot pour marquer les incréments. Chaque lot de événements incrémentiels doit être traité.

Pour les profils incrémentiels, l&#39;outil ETL utilise les dates créées/mises à jour de l&#39;entité par lot. En règle générale, chaque lot de données de profil incrémentielles doit être traité.

Les événements d&#39;instantanés sont très peu susceptibles en raison de la taille des données. Mais si cela était nécessaire, l&#39;outil ETL ne doit sélectionner que le dernier lot à traiter.

Lorsque des profils d&#39;instantané sont utilisés, l&#39;outil ETL doit sélectionner le dernier lot de données qui est arrivé dans le système. Mais si l&#39;exigence est de suivre les versions des modifications, tous les lots devront être traités. Le traitement de la déduplication dans le processus ETL contribuera à contrôler les coûts d&#39;enregistrement.

## Réexécution par lots et retraitement des données

Il peut s’avérer nécessaire de réexécuter le lot et de retraiter les données lorsqu’un client découvre que, au cours des &quot;n&quot; derniers jours, les données traitées par ETL n’ont pas été traitées comme prévu ou que les données source elles-mêmes n’ont pas été correctes.

Pour ce faire, les administrateurs de données du client utiliseront l’interface utilisateur de la plate-forme pour supprimer les lots contenant des données corrompues. Ensuite, l&#39;ETL devra probablement être réexécuté, rerenseignant ainsi les données correctes. Si la source elle-même contenait des données corrompues, l’ingénieur/l’administrateur de données devra corriger les lots source et réassimiler les données (dans Adobe Experience Platform ou via des connecteurs ETL).

En fonction du type de données généré, l&#39;ingénieur de données choisit de supprimer un seul lot ou tous les lots de certains jeux de données. Les données seront supprimées/archivées conformément aux directives de la plateforme d’expérience.

Il est probable que la fonctionnalité ETL pour purger les données soit importante.

Une fois la purge terminée, les administrateurs client devront reconfigurer Adobe Experience Platform pour redémarrer le traitement des services principaux à partir du moment où les lots sont supprimés.

## Traitement par lots simultané

À la discrétion du client, les administrateurs/ingénieurs de données peuvent décider d&#39;extraire, de transformer et de charger les données de manière séquentielle ou concomitante, selon les caractéristiques d&#39;un jeu de données particulier. Cela dépend également du cas d’utilisation que le client cible avec les données transformées.

Par exemple, si le client persiste dans un magasin de persistance modifiable et que la séquence ou l’ordre des événements est important, le client peut avoir besoin de traiter rigoureusement les tâches avec des transformations ETL séquentielles.

Dans d’autres cas, les données en panne peuvent être traitées par des applications/processus en aval qui trient en interne à l’aide d’un horodatage spécifié. Dans ces cas, des transformations ETL parallèles peuvent être viables pour améliorer les temps de traitement.

Pour les lots sources, elle dépend à nouveau de la préférence du client et des contraintes du consommateur. Si les données source peuvent être collectées en parallèle sans tenir compte de la régularité/de l&#39;ordre d&#39;une ligne, le processus de transformation peut alors créer des lots de processus avec un degré de parallélisme plus élevé (optimisation basée sur un traitement hors commande). Mais si la transformation doit respecter les horodatages ou modifier l’ordre de priorité, l’API d’accès aux données ou l’Planificateur d’outils ETL/invocation devra s’assurer que les lots ne sont pas traités dans l’ordre lorsque cela est possible.

## Report

Le report est un processus dans lequel les données d&#39;entrée ne sont pas encore suffisamment complètes pour être envoyées aux processus en aval, mais peuvent être utilisables à l&#39;avenir. Les clients détermineront leur tolérance individuelle à l&#39;égard de la fenêtre de données pour la mise en correspondance future par rapport au coût de traitement afin d&#39;informer leur décision de mettre de côté les données et de les retraiter lors de la prochaine transformation, en espérant qu&#39;elles pourront être enrichies et réconciliées/assemblés à un moment futur dans la fenêtre de rétention. Ce cycle se poursuit jusqu&#39;à ce que la ligne soit traitée suffisamment ou qu&#39;elle soit considérée comme trop obsolète pour continuer à investir dans. Chaque itération génère des données différées qui sont un superset de toutes les données différées des itérations précédentes.

Adobe Experience Platform n’identifie pas actuellement les données différées. Les implémentations clientes doivent donc s’appuyer sur les configurations manuelles ETL et Dataset pour créer un autre jeu de données dans Platform en miroir du jeu de données source qui peut être utilisé pour conserver les données différées. Dans ce cas, les données différées sont similaires aux données d&#39;instantané. Dans chaque exécution de la transformation ETL, les données source sont unies avec des données différées et envoyées pour traitement.

## Changelog

| Date | Action | Description |
| ---- | ------ | ----------- |
| 2019-01-19 | Suppression de la propriété &quot;fields&quot; des jeux de données | Les jeux de données comprenaient auparavant une propriété &quot;fields&quot; qui contenait une copie du schéma. Cette fonctionnalité ne doit plus être utilisée. Si la propriété &quot;fields&quot; est trouvée, elle doit être ignorée et la propriété &quot;observéSchema&quot; ou &quot;schemaRef&quot; utilisée à la place. |
| 2019-03-15 | Propriété &quot;schemaRef&quot; ajoutée aux jeux de données | La propriété &quot;schemaRef&quot; d’un jeu de données contient un URI référençant l’schéma XDM sur lequel le jeu de données est basé et représente tous les champs potentiels pouvant être utilisés par le jeu de données. |
| 2019-03-15 | Tous les identifiants d’utilisateur final correspondent à la propriété &quot;identityMap&quot;. | &quot;identityMap&quot; est un encapsulage de tous les identifiants uniques d’un sujet, tels que l’identifiant CRM, l’identifiant ECID ou l’identifiant de programme de fidélité. Cette carte est utilisée par [Identity Service](../identity-service/home.md) pour résoudre toutes les identités connues et anonymes d&#39;un sujet, en formant un graphique d&#39;identité unique pour chaque utilisateur final. |
| 2019-05-30 | EOL et Supprimer la propriété &quot;schéma&quot; des jeux de données | La propriété &quot;schéma&quot; du jeu de données fournissait un lien de référence vers le schéma à l’aide du point de terminaison obsolète de l’API de catalogue. `/xdms` Il a été remplacé par un &quot;schemaRef&quot; qui fournit &quot;id&quot;, &quot;version&quot; et &quot;contentType&quot; du schéma, comme référencé dans la nouvelle API de registre de Schéma. |
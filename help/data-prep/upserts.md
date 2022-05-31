---
keywords: Experience Platform;accueil;rubriques les plus consultées;prép de données;préparation de données;diffusion en continu;insertion en continu;insertion en continu
title: Envoi De Mises À Jour De Ligne Partielles Au Service De Profil À L’Aide De La Préparation De Données
description: Ce document fournit des informations sur la manière d’envoyer des mises à jour de lignes partielles au service Profile à l’aide de la préparation de données.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: 93c95fce45dc034c0b9c53d9893a8e38e752ec0f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 8%

---

# Envoi de mises à jour de lignes partielles à [!DNL Profile Service] using [!DNL Data Prep]

Diffusion en continu des upserts dans [!DNL Data Prep] vous permet d’envoyer des mises à jour de ligne partielles à [!DNL Profile Service] lors de la création et de l’établissement de nouveaux liens d’identité avec une seule requête API.

En diffusant en continu des upserts, vous pouvez conserver le format de vos données tout en convertissant ces données en [!DNL Profile Service] Demandes de PATCH pendant l’ingestion. En fonction des entrées que vous fournissez, [!DNL Data Prep] vous permet d’envoyer une seule charge utile API et de traduire les données dans les deux [!DNL Profile Service] PATCH et [!DNL Identity Service] CRÉEZ des requêtes.

Ce document fournit des informations sur la diffusion en continu de upserts dans [!DNL Data Prep].

## Prise en main

Cette présentation d’ nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).
* [[!DNL Identity Service]](../identity-service/home.md) : profitez d’une meilleure compréhension de vos clients et de leurs comportements en rapprochant des identités entre appareils et systèmes.
* [Real-time Customer Profile](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sources](../sources/home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services de Platform.

## Utilisation de serveurs de diffusion en continu dans [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Les sources suivantes prennent en charge l’utilisation de serveurs de diffusion en continu :<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Workflow de haut niveau des upserts en flux continu

Diffusion en continu des upserts dans [!DNL Data Prep] fonctionne comme suit :

* Vous devez d’abord créer et activer un jeu de données pour [!DNL Profile] consommation. Consultez le guide sur la [activation d’un jeu de données pour [!DNL Profile]](../catalog/datasets/enable-for-profile.md) pour plus d’informations;
* Si de nouvelles identités doivent être liées, vous devez également créer un jeu de données supplémentaire. **avec le même schéma** en tant que [!DNL Profile] jeu de données ;
* Une fois vos jeux de données préparés, vous devez créer un flux de données pour mapper votre requête entrante à la variable [!DNL Profile] jeu de données ;
* Vous devez ensuite mettre à jour la requête entrante afin d’inclure les en-têtes nécessaires. Ces en-têtes définissent :
   * L’opération de données à effectuer avec [!DNL Profile]: `create`, `merge`, et `delete`;
   * L’opération d’identité facultative à effectuer avec [!DNL Identity Service]: `create`.

### Configuration du jeu de données d’identité

Si de nouvelles identités doivent être liées, vous devez créer et transmettre un jeu de données supplémentaire dans la payload entrante. Lors de la création d’un jeu de données d’identité, vous devez vous assurer que les conditions suivantes sont remplies :

* Le jeu de données d’identité doit avoir son schéma associé comme [!DNL Profile] jeu de données. Une incohérence des schémas peut entraîner un comportement du système incohérent ;
* Cependant, vous devez vous assurer que le jeu de données d’identité est différent du [!DNL Profile] jeu de données. Si les jeux de données sont identiques, les données seront écrasées au lieu d’être mises à jour ;
* Alors que le jeu de données initial doit être activé pour [!DNL Profile], le jeu de données d’identité **should not** être activé pour [!DNL Profile]. Dans le cas contraire, les données seront également écrasées au lieu d’être mises à jour.

#### Champs obligatoires dans les schémas associés au jeu de données d’identité {#identity-dataset-required-fileds}

Si votre schéma contient des champs obligatoires, la validation du jeu de données doit être supprimée pour permettre [!DNL Identity Service] pour ne recevoir que les identités. Vous pouvez supprimer la validation en appliquant le `disabled` à la valeur `acp_validationContext` . Voir l&#39;exemple ci-dessous:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>Vous n’avez pas besoin d’effectuer de configuration supplémentaire si le schéma associé au jeu de données d’identité ne comporte aucun champ obligatoire.

## Structure de payload entrante

L’exemple suivant illustre une structure de payload entrante établissant de nouveaux liens d’identité.

### Payload avec configuration d’identité

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| Paramètre | Description |
| --- | --- |
| `flowId` | Identifiant unique permettant d’identifier un flux de données. Cet identifiant de flux de données doit correspondre à la connexion source créée avec [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]ou [!DNL HTTP API]. Ce flux de données doit également comporter une [!DNL Profile]-enabled dataset comme jeu de données cible. **Remarque**: L’identifiant de la variable [!DNL Profile]Le jeu de données cible activé est également utilisé comme `datasetId` . |
| `imsOrgId` | L’identifiant qui correspond à votre organisation. |
| `datasetId` | L’identifiant de la variable [!DNL Profile]-enabled target dataset de votre flux de données. **Remarque**: Il s’agit du même ID que la variable [!DNL Profile]Identifiant de jeu de données cible activé trouvé dans votre flux de données. |
| `operations` | Ce paramètre décrit les actions que [!DNL Data Prep] repose sur la requête entrante. |
| `operations.data` | Définit les actions qui doivent être effectuées dans [!DNL Profile Service]. |
| `operations.identity` | Définit les opérations autorisées sur les données par [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Facultatif) Identifiant du jeu de données d’identité requis uniquement si de nouvelles identités doivent être liées. |

#### Opérations prises en charge

Les opérations suivantes sont prises en charge par [!DNL Profile Service]:

| Opérations | Description |
| --- | --- | 
| `create` | Opération par défaut. Cela génère une méthode de création d’entité XDM pour [!DNL Profile Service]. |
| `merge` | Cela génère une méthode de mise à jour d’entité XDM pour [!DNL Profile Service]. |
| `delete` | Cette opération génère une méthode de suppression d’entité XDM pour [!DNL Profile Service] et supprime définitivement les données de la [!DNL Profile Store]. |

Les opérations suivantes sont prises en charge par [!DNL Identity Service]:

| Opérations | Descriptions |
| --- | --- |
| `create` | La seule opération autorisée pour ce paramètre. If `create` est transmis en tant que valeur pour `operations.identity`, puis [!DNL Data Prep] génère une requête de création d’entité XDM pour [!DNL Identity Service]. Si l’identité existe déjà, l’identité est ignorée. **Remarque :** If `operations.identity` est défini sur `create`, puis la variable `identityDatasetId` doit également être spécifié. L’entité XDM crée un message généré en interne par [!DNL Data Prep] est généré pour cet identifiant de jeu de données. |

### Charge utile sans configuration d’identité

Si de nouvelles identités n’ont pas besoin d’être liées, vous pouvez omettre la variable `identity` et `identityDatasetId` dans les opérations. Ainsi, les données ne sont envoyées qu’à [!DNL Profile Service] et ignore la variable [!DNL Identity Service]. Voir la payload ci-dessous pour obtenir un exemple :

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## Transmission dynamique des identités Principales

Pour les mises à jour XDM, le schéma doit être activé pour [!DNL Profile] et contiennent une identité Principale. Vous pouvez spécifier l’identité Principale d’un schéma XDM de deux manières :

* Désigner un champ statique comme identité Principale dans le schéma XDM ;
* Désignez l’un des champs d’identité comme identité Principale par le biais du groupe de champs de carte d’identité dans le schéma XDM.

### Désigner un champ statique comme champ d’identité Principal dans le schéma XDM

Dans l’exemple ci-dessous, `state`, `homePhone.number` et d’autres attributs sont mis à jour avec leurs valeurs respectives données dans la variable [!DNL Profile] avec la Principale identité de `sampleEmail@gmail.com`. Un message de mise à jour d’entité XDM est ensuite généré par la diffusion en continu. [!DNL Data Prep] composant. [!DNL Profile Service] confirme ensuite le message de mise à jour XDM pour insérer l’enregistrement de profil.

>[!NOTE]
>
>Dans cet exemple, les identités ne seront pas liées, car aucune opération n’est définie pour l’identité.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### Désigner l’un des champs d’identité comme identité Principale par le biais du groupe de champs de carte d’identité dans le schéma XDM

Dans cet exemple, l’en-tête contient le `operations` avec l’attribut `identity` et `identityDatasetId` propriétés. Cela permet de fusionner les données avec [!DNL Profile Service] et également pour les identités à transmettre à [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## Limites connues et considérations clés

Vous trouverez ci-dessous une liste des limites connues à prendre en compte lors de la diffusion en continu de upserts avec [!DNL Data Prep]:

* La méthode de mise à jour en continu ne doit être utilisée que lors de l’envoi de mises à jour de lignes partielles à [!DNL Profile Service]. Les mises à jour des lignes partielles sont **not** consommé par le lac de données.
* La méthode de diffusion en continu upserts ne prend pas en charge la mise à jour, le remplacement et la suppression des identités. De nouvelles identités sont créées si elles n’existent pas. D’où `identity` doit toujours être définie pour créer. Si une identité existe déjà, l’opération est un &quot;no-op&quot;.
* Actuellement, la méthode de mise en service par flux ne prend en charge que les attributs à valeur unique primitifs (tels que les entiers, les dates, les horodatages et les chaînes) et les objets. La méthode de serveur de diffusion en continu ne prend pas en charge le remplacement, l’ajout ou le remplacement d’attributs de tableau et d’index de tableau spécifiques.

## Étapes suivantes

En lisant ce document, vous devez maintenant comprendre comment diffuser des upserts dans [!DNL Data Prep] pour envoyer des mises à jour de ligne partielles à votre [!DNL Profile Service] , tout en créant et en liant des identités à une seule requête API. Pour plus d’informations sur les autres [!DNL Data Prep] fonctions, veuillez lire la [[!DNL Data Prep] aperçu](./home.md). Pour savoir comment utiliser les ensembles de mappages dans la [!DNL Data Prep] API, veuillez lire la [[!DNL Data Prep] guide de développement](./api/overview.md).

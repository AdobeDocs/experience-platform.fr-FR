---
keywords: Experience Platform;accueil;rubriques les plus consultées;préparation des données;préparation des données;diffusion en continu;upsert;diffusion en continu upsert
title: Envoyer Des Mises À Jour De Ligne Partielles Au Profil Client En Temps Réel À L’Aide De La Préparation Des Données
description: Découvrez comment envoyer des mises à jour de lignes partielles au profil client en temps réel à l’aide de la préparation des données.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 3%

---

# Envoyer des mises à jour de lignes partielles aux [!DNL Real-Time Customer Profile] à l’aide de [!DNL Data Prep]

>[!IMPORTANT]
>
>* L’ingestion de messages de mise à jour d’entité du modèle de données d’expérience (XDM) (avec des opérations JSON PATCH) pour les mises à jour de profil via l’entrée DCS est obsolète. Suivez les étapes décrites dans ce guide comme alternative.
>
>* Vous pouvez également utiliser la source d’API HTTP pour [ingérer des données brutes dans l’inlet DCS](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) et spécifier les mappages de données nécessaires pour transformer vos données en messages conformes à XDM pour les mises à jour de Profile.
>
>* Lors de l’utilisation de tableaux dans des upserts en flux continu, vous devez utiliser explicitement `upsert_array_append` ou `upsert_array_replace` pour définir l’intention claire de l’opération. Vous pouvez recevoir des erreurs si ces fonctions sont manquantes.

Utilisez des upserts en flux continu dans [!DNL Data Prep] pour envoyer des mises à jour de lignes partielles à [!DNL Real-Time Customer Profile] données tout en créant et en établissant de nouveaux liens d’identité avec une seule requête API.

En diffusant des upserts en continu, vous pouvez conserver le format de vos données tout en les traduisant en requêtes PATCH [!DNL Real-Time Customer Profile] lors de l’ingestion. En fonction des entrées que vous fournissez, [!DNL Data Prep] vous permet d’envoyer une seule payload d’API et de traduire les données à la fois vers [!DNL Real-Time Customer Profile] requêtes PATCH et [!DNL Identity Service] CREATE.

[!DNL Data Prep] utilise les paramètres d&#39;en-tête pour faire la distinction entre les insertions et les upserts. Toutes les lignes qui utilisent des upserts doivent avoir un en-tête. Vous pouvez utiliser des upserts avec ou sans descripteurs d’identité. Si vous utilisez des upserts avec des identités, vous devez suivre les étapes de configuration décrites dans la section [Configuration du jeu de données d’identité](#configure-the-identity-dataset). Si vous utilisez des upserts sans identités, vous n’avez pas besoin de fournir de configurations d’identité dans votre requête. Lisez la section sur la [diffusion en continu d’upserts sans identités](#payload-without-identity-configuration) pour plus d’informations.

>[!NOTE]
>
>Pour tirer parti de la fonctionnalité d’upsert, il est recommandé de désactiver les configurations compatibles avec XDM lors de l’ingestion des données et de remapper la payload entrante à l’aide du [mappeur de préparation des données](./ui/mapping.md).

Ce document fournit des informations sur la diffusion d’upserts dans [!DNL Data Prep].

## Prise en main

Cette présentation d’ nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Data Prep]](./home.md) : [!DNL Data Prep] permet aux ingénieurs de données de mapper, transformer et valider des données vers et à partir du modèle de données d’expérience (XDM).
* [[!DNL Identity Service]](../identity-service/home.md) : obtenez une meilleure compréhension des clients individuels et de leurs comportements en rapprochant des identités entre appareils et systèmes.
* [Real-Time Customer Profile](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sources](../sources/home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, d’étiqueter et d’améliorer les données entrantes à l’aide des services d’Experience Platform.

## Utiliser des upserts en flux continu dans [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Les sources suivantes prennent en charge l’utilisation d’upserts en flux continu :<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Workflow de haut niveau de diffusion d’upserts

La diffusion en continu d’upserts dans [!DNL Data Prep] fonctionne comme suit :

* Vous devez d’abord créer et activer un jeu de données pour la consommation [!DNL Profile]. Pour plus d’informations, consultez le guide sur [l’activation d’un jeu de données pour [!DNL Profile]](../catalog/datasets/enable-for-profile.md).
* Si de nouvelles identités doivent être liées, vous devez également créer un jeu de données supplémentaire **avec le même schéma** que votre jeu de données [!DNL Profile].
* Une fois que votre ou vos jeux de données sont préparés, vous devez créer un flux de données pour mapper votre requête entrante au jeu de données [!DNL Profile] ;
* Ensuite, vous devez mettre à jour la requête entrante pour inclure les en-têtes nécessaires. Ces en-têtes définissent les éléments suivants :
   * Opération de données devant être effectuée avec [!DNL Profile] : `create`, `merge` et `delete`.
   * Opération d’identité facultative à effectuer avec [!DNL Identity Service] : `create`.

### Configurer le jeu de données d’identité {#configure-the-identity-dataset}

Si de nouvelles identités doivent être liées, vous devez créer et transmettre un jeu de données supplémentaire dans la payload entrante. Lors de la création d’un jeu de données d’identité, vous devez vous assurer que les exigences suivantes sont remplies :

* Le jeu de données d’identité doit avoir son schéma associé comme jeu de données [!DNL Profile]. Une incohérence des schémas peut entraîner un comportement incohérent du système.
* Cependant, vous devez vous assurer que le jeu de données d’identité est différent du jeu de données d’[!DNL Profile]. Si les jeux de données sont identiques, les données sont remplacées au lieu d’être mises à jour.
* Alors que le jeu de données initial doit être activé pour [!DNL Profile], le jeu de données d’identité **ne doit pas être activé** par [!DNL Profile]. Sinon, les données seront également remplacées au lieu d’être mises à jour. Cependant, le jeu de données d’identité **doit être activé** par [!DNL Identity Service].

#### Champs obligatoires dans les schémas associés au jeu de données d’identité {#identity-dataset-required-fileds}

Si votre schéma contient des champs obligatoires, la validation du jeu de données doit être supprimée pour permettre aux [!DNL Identity Service] de ne recevoir que les identités. Vous pouvez supprimer la validation en appliquant la valeur `disabled` au paramètre `acp_validationContext` . Voir l’exemple ci-dessous :

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>Vous n’avez pas besoin d’effectuer de configuration supplémentaire si le schéma associé au jeu de données d’identité ne comporte aucun champ obligatoire.

## Structure de la payload entrante

Vous trouverez ci-dessous un exemple de structure de payload entrante qui établit de nouveaux liens d’identité.

### Payload avec configuration des identités

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
| `flowId` | Identifiant unique permettant d’identifier un flux de données. Cet identifiant de flux de données doit correspondre à la connexion source créée avec [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] ou [!DNL HTTP API]. Ce flux de données doit également avoir un jeu de données activé pour [!DNL Profile] comme jeu de données cible. **Remarque** : l’identifiant du jeu de données cible activé pour [!DNL Profile] est également utilisé comme paramètre de `datasetId`. |
| `imsOrgId` | Identifiant qui correspond à votre organisation. |
| `datasetId` | L’identifiant du jeu de données cible activé pour [!DNL Profile] de votre flux de données. **Remarque** : il s’agit du même identifiant que l’identifiant du jeu de données cible activé pour [!DNL Profile] qui se trouve dans votre flux de données. |
| `operations` | Ce paramètre décrit les actions que [!DNL Data Prep] entreprendrez en fonction de la requête entrante. |
| `operations.data` | Définit les actions qui doivent être effectuées dans [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Définit les opérations autorisées sur les données par [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Facultatif) Identifiant du jeu de données d’identité obligatoire uniquement si de nouvelles identités doivent être liées. |

#### Opérations prises en charge

Les opérations suivantes sont prises en charge par [!DNL Real-Time Customer Profile] :

| Opérations | Description |
| --- | --- | 
| `create` | Opération par défaut. Cela génère une méthode de création d’entité XDM pour [!DNL Real-Time Customer Profile]. |
| `merge` | Cela génère une méthode de mise à jour d’entité XDM pour [!DNL Real-Time Customer Profile]. |
| `delete` | Cela génère une méthode de suppression d’entité XDM pour [!DNL Real-Time Customer Profile] et supprime définitivement les données du [!DNL Profile store]. |

Les opérations suivantes sont prises en charge par [!DNL Identity Service] :

| Opérations | Descriptions |
| --- | --- |
| `create` | Seule opération autorisée pour ce paramètre. Si `create` est transmis en tant que valeur pour `operations.identity`, [!DNL Data Prep] génère une requête de création d’entité XDM pour [!DNL Identity Service]. Si l’identité existe déjà, elle est ignorée. **Remarque :** si `operations.identity` est défini sur `create`, le `identityDatasetId` doit également être spécifié. Le message de création d’entité XDM généré en interne par [!DNL Data Prep] composant sera généré pour cet identifiant de jeu de données. |

### Payload sans configuration d’identité {#payload-without-identity-configuration}

S’il n’est pas nécessaire de lier de nouvelles identités, vous pouvez omettre les paramètres `identity` et `identityDatasetId` dans les opérations. Cela envoie les données uniquement à [!DNL Real-Time Customer Profile] et ignore le [!DNL Identity Service]. Pour obtenir un exemple, reportez-vous à la payload ci-dessous :

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

## Transmission dynamique des identités principales

Pour les mises à jour XDM, le schéma doit être activé pour [!DNL Profile] et contenir une identité principale. Vous pouvez spécifier l’identité principale d’un schéma XDM de deux manières :

* Désigner un champ statique comme identité principale dans le schéma XDM ;
* Désignez l’un des champs d’identité comme identité principale par le biais du groupe de champs de mappage d’identités dans le schéma XDM.

### Désigner un champ statique comme champ d’identité principale dans le schéma XDM

Dans l’exemple ci-dessous, les attributs `state`, `homePhone.number` et autres sont insérés avec leurs valeurs données respectives dans le [!DNL Profile] avec l’identité principale de `sampleEmail@gmail.com`. Un message de mise à jour d’entité XDM est ensuite généré par le composant [!DNL Data Prep] de diffusion en continu. [!DNL Real-Time Customer Profile] confirme ensuite ce message de mise à jour XDM pour upsert l’enregistrement de profil.

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

### Désignez l’un des champs d’identité comme identité principale par le biais du groupe de champs de mappage d’identités dans le schéma XDM

Dans cet exemple, l’en-tête contient l’attribut `operations` avec les propriétés `identity` et `identityDatasetId` . Cela permet de fusionner les données avec [!DNL Real-Time Customer Profile] et de transmettre les identités à [!DNL Identity Service].

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

Vous trouverez ci-dessous une liste des limites connues à prendre en compte lors de la diffusion en flux continu d’upserts avec [!DNL Data Prep] :

* La méthode upserts en flux continu ne doit être utilisée que lors de l’envoi de mises à jour de lignes partielles à [!DNL Real-Time Customer Profile]. Les mises à jour de lignes partielles ne sont **pas** utilisées par le lac de données.
* La méthode upserts en flux continu ne prend pas en charge la mise à jour, le remplacement et la suppression des identités. De nouvelles identités sont créées si elles n’existent pas. Par conséquent, l’opération `identity` doit toujours être définie sur créer. Si une identité existe déjà, l’opération n’est pas opérationnelle.
* La méthode upserts en flux continu ne prend actuellement pas en charge [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) et [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Étapes suivantes

En lisant ce document, vous devriez maintenant comprendre comment diffuser des upserts dans [!DNL Data Prep] pour envoyer des mises à jour de lignes partielles à vos données [!DNL Real-Time Customer Profile], tout en créant et en liant des identités avec une seule requête API. Pour plus d’informations sur les autres fonctionnalités de [!DNL Data Prep], veuillez lire la [[!DNL Data Prep] présentation](./home.md). Pour savoir comment utiliser les jeux de mappages dans l’API [!DNL Data Prep], consultez le [[!DNL Data Prep] guide de développement](./api/overview.md).

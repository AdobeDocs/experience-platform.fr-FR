---
keywords: Experience Platform;accueil;rubriques les plus consultées;prép de données;préparation de données;diffusion en continu;insertion en continu;insertion en continu
title: Envoyer Des Mises À Jour Partielles De Ligne À Real-Time Customer Profile À L’Aide De La Préparation De Données
description: Découvrez comment envoyer des mises à jour de lignes partielles à Real-time Customer Profile à l’aide de la préparation de données.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 5%

---

# Envoyez des mises à jour de lignes partielles à [!DNL Real-Time Customer Profile] à l’aide de [!DNL Data Prep]

>[!WARNING]
>
>L’ingestion sur les messages de mise à jour d’entité du modèle de données d’expérience (XDM) (avec les opérations du PATCH JSON) pour les mises à jour de profil via l’inlet du DCS a été abandonnée. Vous pouvez également [ingérer des données brutes dans l’inlet du DCS](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) et spécifier les mappages de données nécessaires pour transformer vos données en messages compatibles XDM pour les mises à jour de Profile.

Les upserts de diffusion en continu dans [!DNL Data Prep] vous permettent d’envoyer des mises à jour de lignes partielles aux données [!DNL Real-Time Customer Profile] tout en créant et en établissant de nouveaux liens d’identité avec une seule requête API.

En diffusant en continu des upserts, vous pouvez conserver le format de vos données tout en convertissant ces données en demandes de PATCH [!DNL Real-Time Customer Profile] pendant l’ingestion. En fonction des entrées que vous fournissez, [!DNL Data Prep] vous permet d’envoyer une seule charge utile API et de traduire les données vers les requêtes [!DNL Real-Time Customer Profile] PATCH et [!DNL Identity Service] CREATE.

>[!NOTE]
>
>Pour tirer parti de la fonctionnalité de restauration, il est recommandé de désactiver les configurations compatibles XDM lors de l’ingestion des données et de mapper à nouveau la charge utile entrante à l’aide de [Data Prep Mapper](./ui/mapping.md).

Ce document fournit des informations sur la diffusion en continu de upserts dans [!DNL Data Prep].

## Prise en main

Cette présentation d’ nécessite une compréhension professionnelle des composants suivants d’Adobe Experience Platform :

* [[!DNL Data Prep]](./home.md) : [!DNL Data Prep] permet aux ingénieurs de données de mapper, de transformer et de valider des données vers et depuis le modèle de données d’expérience (XDM).
* [[!DNL Identity Service]](../identity-service/home.md) : profitez d’une meilleure vue d’ensemble des clients et de leur comportement en rapprochant des identités entre appareils et systèmes.
* [Real-Time Customer Profile](../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.
* [Sources](../sources/home.md) : Experience Platform permet d’ingérer des données provenant de diverses sources tout en vous offrant la possibilité de structurer, de libeller et d’améliorer les données entrantes à l’aide des services de Platform.

## Utilisation de serveurs de diffusion en continu dans [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>Les sources suivantes prennent en charge l’utilisation de serveurs de diffusion en continu :<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Workflow de haut niveau des upserts en flux continu

Les upserts de diffusion en continu dans [!DNL Data Prep] fonctionnent comme suit :

* Vous devez d’abord créer et activer un jeu de données pour la consommation [!DNL Profile]. Pour plus d’informations, consultez le guide sur l’ [activation d’un jeu de données pour [!DNL Profile]](../catalog/datasets/enable-for-profile.md) .
* Si de nouvelles identités doivent être liées, vous devez également créer un jeu de données supplémentaire **avec le même schéma** que votre jeu de données [!DNL Profile].
* Une fois vos jeux de données préparés, vous devez créer un flux de données pour mapper votre requête entrante au jeu de données [!DNL Profile].
* Vous devez ensuite mettre à jour la requête entrante afin d’inclure les en-têtes nécessaires. Ces en-têtes définissent :
   * L’opération de données à effectuer avec [!DNL Profile] : `create`, `merge` et `delete`.
   * Opération d’identité facultative à effectuer avec [!DNL Identity Service] : `create`.

### Configuration du jeu de données d’identité

Si de nouvelles identités doivent être liées, vous devez créer et transmettre un jeu de données supplémentaire dans la payload entrante. Lors de la création d’un jeu de données d’identité, vous devez vous assurer que les conditions suivantes sont remplies :

* Le jeu de données d’identité doit avoir son schéma associé comme jeu de données [!DNL Profile]. Une incohérence des schémas peut entraîner un comportement du système incohérent.
* Cependant, vous devez vous assurer que le jeu de données d’identité est différent du jeu de données [!DNL Profile]. Si les jeux de données sont identiques, les données seront écrasées au lieu d’être mises à jour.
* Bien que le jeu de données initial doive être activé pour [!DNL Profile], le jeu de données d’identité **ne doit pas être activé** pour [!DNL Profile]. Dans le cas contraire, les données seront également écrasées au lieu d’être mises à jour. Cependant, le jeu de données d’identité **doit être activé** pour [!DNL Identity Service].

#### Champs obligatoires dans les schémas associés au jeu de données d’identité {#identity-dataset-required-fileds}

Si votre schéma contient des champs obligatoires, la validation du jeu de données doit être supprimée pour permettre à [!DNL Identity Service] de recevoir uniquement les identités. Vous pouvez supprimer la validation en appliquant la valeur `disabled` au paramètre `acp_validationContext` . Voir l’exemple ci-dessous :

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
| `flowId` | Identifiant unique pour identifier un flux de données. Cet identifiant de flux de données doit correspondre à la connexion source créée avec [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] ou [!DNL HTTP API]. Ce flux de données doit également comporter un jeu de données activé [!DNL Profile] comme jeu de données cible. **Remarque** : L’identifiant du jeu de données cible [!DNL Profile] activé est également utilisé comme paramètre `datasetId`. |
| `imsOrgId` | L’identifiant qui correspond à votre organisation. |
| `datasetId` | L’identifiant du jeu de données cible [!DNL Profile] de votre flux de données. **Remarque** : Il s’agit du même identifiant que l’identifiant du jeu de données cible [!DNL Profile] trouvé dans votre flux de données. |
| `operations` | Ce paramètre décrit les actions que [!DNL Data Prep] va entreprendre en fonction de la requête entrante. |
| `operations.data` | Définit les actions qui doivent être effectuées dans [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Définit les opérations autorisées sur les données par [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Facultatif) Identifiant du jeu de données d’identité requis uniquement si de nouvelles identités doivent être liées. |

#### Opérations prises en charge

Les opérations suivantes sont prises en charge par [!DNL Real-Time Customer Profile] :

| Opérations | Description |
| --- | --- | 
| `create` | Opération par défaut. Cela génère une méthode de création d’entité XDM pour [!DNL Real-Time Customer Profile]. |
| `merge` | Cela génère une méthode de mise à jour d’entité XDM pour [!DNL Real-Time Customer Profile]. |
| `delete` | Cette opération génère une méthode de suppression d’entité XDM pour [!DNL Real-Time Customer Profile] et supprime définitivement les données de [!DNL Profile store]. |

Les opérations suivantes sont prises en charge par [!DNL Identity Service] :

| Opérations | Descriptions |
| --- | --- |
| `create` | La seule opération autorisée pour ce paramètre. Si `create` est transmis en tant que valeur pour `operations.identity`, alors [!DNL Data Prep] génère une requête de création d’entité XDM pour [!DNL Identity Service]. Si l’identité existe déjà, l’identité est ignorée. **Remarque :** Si `operations.identity` est défini sur `create`, le `identityDatasetId` doit également être spécifié. L’entité XDM crée un message généré en interne par le composant [!DNL Data Prep] sera généré pour cet identifiant de jeu de données. |

### Charge utile sans configuration d’identité

Si de nouvelles identités ne doivent pas être liées, vous pouvez omettre les paramètres `identity` et `identityDatasetId` dans les opérations. Cela envoie uniquement des données à [!DNL Real-Time Customer Profile] et ignore [!DNL Identity Service]. Voir la payload ci-dessous pour obtenir un exemple :

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

## Transmission dynamique des identités primaires

Pour les mises à jour XDM, le schéma doit être activé pour [!DNL Profile] et contenir une identité principale. Vous pouvez spécifier l’identité principale d’un schéma XDM de deux manières :

* Désigner un champ statique comme identité principale dans le schéma XDM ;
* Désignez l’un des champs d’identité comme identité principale par le biais du groupe de champs de carte d’identité dans le schéma XDM.

### Désigner un champ statique comme champ d’identité principal dans le schéma XDM

Dans l’exemple ci-dessous, `state`, `homePhone.number` et d’autres attributs sont mis à jour avec leurs valeurs respectives données dans le [!DNL Profile] avec l’identité principale de `sampleEmail@gmail.com`. Un message de mise à jour d’entité XDM est ensuite généré par le composant de diffusion en continu [!DNL Data Prep]. [!DNL Real-Time Customer Profile] confirme ensuite le message de mise à jour XDM pour insérer l’enregistrement de profil.

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

### Désigner l’un des champs d’identité comme identité principale par le biais du groupe de champs de carte d’identité dans le schéma XDM

Dans cet exemple, l’en-tête contient l’attribut `operations` avec les propriétés `identity` et `identityDatasetId`. Cela permet de fusionner les données avec [!DNL Real-Time Customer Profile] et de transmettre les identités à [!DNL Identity Service].

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

Voici une liste des limites connues à prendre en compte lors de la diffusion en continu de upserts avec [!DNL Data Prep] :

* La méthode des upserts de diffusion ne doit être utilisée que lors de l’envoi de mises à jour de lignes partielles à [!DNL Real-Time Customer Profile]. Les mises à jour de lignes partielles sont **et non** consommées par le lac de données.
* La méthode de diffusion en continu upserts ne prend pas en charge la mise à jour, le remplacement et la suppression des identités. De nouvelles identités sont créées si elles n’existent pas. Par conséquent, l’opération `identity` doit toujours être définie pour créer. Si une identité existe déjà, l’opération est un &quot;no-op&quot;.
* La méthode des upserts de diffusion en continu ne prend actuellement pas en charge [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) et [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Étapes suivantes

En lisant ce document, vous devez maintenant comprendre comment diffuser des upserts dans [!DNL Data Prep] pour envoyer des mises à jour de lignes partielles à vos données [!DNL Real-Time Customer Profile], tout en créant et en liant des identités à une seule requête API. Pour plus d&#39;informations sur les autres fonctionnalités [!DNL Data Prep], consultez la [[!DNL Data Prep] présentation](./home.md). Pour savoir comment utiliser les ensembles de mappages dans l’API [!DNL Data Prep], consultez le [[!DNL Data Prep] guide de développement](./api/overview.md).

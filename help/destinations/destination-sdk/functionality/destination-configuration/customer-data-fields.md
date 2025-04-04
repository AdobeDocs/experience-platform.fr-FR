---
description: Découvrez comment créer des champs d’entrée dans l’interface utilisateur d’Experience Platform qui permettent à vos utilisateurs de spécifier diverses informations relatives à la connexion et à l’exportation des données vers la destination.
title: Champs de données client
exl-id: 7f5b8278-175c-4ab8-bf67-8132d128899e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 71%

---

# Configuration d’une entrée utilisateur avec les champs de données client

Pendant la connexion à la destination dans l’interface utilisateur d’Experience Platform, il se peut que vos utilisateurs aient besoin de fournir des détails de configuration spécifiques ou de sélectionner des options spécifiques que vous leur fournissez. Dans Destination SDK, ces options sont appelées champs de données client.

Pour comprendre la place de ce composant dans une intégration créée avec Destination SDK, consultez le diagramme de la documentation [Options de configuration](../configuration-options.md) ou consultez les pages de vue d’ensemble de la configuration de destination suivantes :

* [Utiliser Destination SDK pour configurer une destination de diffusion en streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

## Cas d’utilisation des champs de données client {#use-cases}

Utilisez les champs de données client pour divers cas d’utilisation où des données doivent être saisies dans l’interface utilisateur d’Experience Platform. Par exemple, utilisez des champs de données client quand les éléments suivants doivent être fournis :

* noms et chemins d’accès aux compartiments d’espaces de stockage, pour les destinations basées sur des fichiers ;
* format accepté par les champs de données client ;
* types de compression de fichiers disponibles que les utilisateurs peuvent sélectionner ;
* listes des points d’entrée disponibles pour les intégrations en temps réel (streaming).

Vous pouvez configurer les champs de données client via le point d’entrée `/authoring/destinations`. Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit tous les types de configuration de champs de données client pris en charge que vous pouvez utiliser pour la destination et montre ce que la clientèle verra dans l’interface utilisateur d’Experience Platform.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Pour en savoir plus sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page, consultez le tableau ci-dessous.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (streaming) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Paramètres pris en charge {#supported-parameters}

Pendant la création de vos propres champs de données client, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour configurer leur comportement.

| Paramètre | Type | Obligatoire / Facultatif | Description |
|---------|----------|------|---|
| `name` | Chaîne | Obligatoire | Attribuez un nom au champ personnalisé que vous introduisez. Ce nom n’est pas visible dans l’interface utilisateur d’Experience Platform, sauf si le champ `title` est vide ou manquant. |
| `type` | Chaîne | Obligatoire | Indique le type de champ personnalisé que vous introduisez. Valeurs acceptées : <ul><li>`string`</li><li>`object`</li><li>`integer`</li></ul> |
| `title` | Chaîne | Facultatif | Indique le nom du champ tel qu’il est affiché par la clientèle dans l’interface utilisateur d’Experience Platform. Si ce champ est vide ou manquant, l’interface utilisateur hérite du nom du champ de la valeur `name`. |
| `description` | Chaîne | Facultatif | Fournissez une description du champ personnalisé. Cette description n’est pas visible dans l’interface utilisateur d’Experience Platform. |
| `isRequired` | Booléen | Facultatif | Indique si les utilisateurs doivent fournir une valeur pour ce champ dans le workflow de configuration de destination. |
| `pattern` | Chaîne | Facultatif | Impose un modèle pour le champ personnalisé, le cas échéant. Utilisez des expressions régulières pour appliquer un modèle. Par exemple, si vos identifiants de client n’incluent pas de chiffres ou de traits de soulignement, saisissez `^[A-Za-z]+$` dans ce champ. |
| `enum` | Chaîne | Facultatif | Rend le champ personnalisé sous forme de menu déroulant et répertorie les options disponibles pour l’utilisateur. |
| `default` | Chaîne | Facultatif | Définit la valeur par défaut d’une liste `enum`. |
| `hidden` | Booléen | Facultatif | Indique si le champ de données client s’affiche ou non dans l’interface utilisateur. |
| `unique` | Booléen | Facultatif | Utilisez ce paramètre quand vous devez créer un champ de données client dont la valeur doit être unique pour tous les flux de données de destination configurés par l’organisation d’un utilisateur. Par exemple, le champ **[!UICONTROL Alias d’intégration]** dans la destination [Personnalisation sur mesure](../../../catalog/personalization/custom-personalization.md) doit être unique, ce qui signifie que deux flux de données distincts vers cette destination ne peuvent pas avoir la même valeur pour ce champ. |
| `readOnly` | Booléen | Facultatif | Indique si le client peut modifier la valeur du champ ou non. |

{style="table-layout:auto"}

Dans l’exemple ci-dessous, la section `customerDataFields` définit deux champs que les utilisateurs doivent renseigner dans l’interface utilisateur d’Experience Platform au moment de la connexion à la destination :

* `Account ID` : identifiant de compte d’utilisateur pour votre plateforme de destination.
* `Endpoint region` : point d’entrée régional de l’API auquel ils se connectent. La section `enum` crée un menu déroulant avec les valeurs définies afin que les utilisateurs puissent les sélectionner.

```json
"customerDataFields":[
   {
      "name":"accountID",
      "title":"User account ID",
      "description":"User account ID for the destination platform.",
      "type":"string",
      "isRequired":true
   },
   {
      "name":"region",
      "title":"API endpoint region",
      "description":"The API endpoint region that the user should connect to.",
      "type":"string",
      "isRequired":true,
      "enum":[
         "EU"
         "US",
      ],
      "readOnly":false,
      "hidden":false
   }
]
```

L’expérience de l’interface utilisateur qui en résulte est affichée dans l’image ci-dessous.

![Image de l’interface utilisateur montrant un exemple de champs de données client.](../../assets/functionality/destination-configuration/customer-data-fields-example.png)

## Noms et descriptions des connexions de destination {#names-description}

Lors de la création d’une destination, Destination SDK ajoute automatiquement les champs **[!UICONTROL Nom]** et **[!UICONTROL Description]** à l’écran de connexion de la destination dans l’interface utilisateur d’Experience Platform. Comme vous pouvez le voir dans l’exemple ci-dessus, les champs **[!UICONTROL Nom]** et **[!UICONTROL Description]** sont générés dans l’interface utilisateur sans être inclus dans la configuration des champs de données client.

>[!IMPORTANT]
>
>Si vous ajoutez les champs **[!UICONTROL Nom]** et **[!UICONTROL Description]** dans la configuration des champs de données client, ils seront visibles deux fois dans l’interface utilisateur.

## Classement des champs de données client {#ordering}

L’ordre dans lequel vous ajoutez les champs de données client dans la configuration de destination est reflété dans l’interface utilisateur d’Experience Platform.

Par exemple, la configuration ci-dessous est reflétée en conséquence dans l’interface utilisateur : les options s’affichent par **[!UICONTROL nom]**, **[!UICONTROL description]**, **[!UICONTROL nom du compartiment]**, **[!UICONTROL chemin d’accès au dossier]**, **[!UICONTROL type de fichier]**, **[!UICONTROL format de compression]**.

```json
"customerDataFields":[
{
   "name":"bucketName",
   "title":"Bucket name",
   "description":"Amazon S3 bucket name",
   "type":"string",
   "isRequired":true,
   "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
   "readOnly":false,
   "hidden":false
},
{
   "name":"path",
   "title":"Folder path",
   "description":"Enter the path to your S3 bucket folder",
   "type":"string",
   "isRequired":true,
   "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
   "readOnly":false,
   "hidden":false
},
{
   "name":"fileType",
   "title":"File Type",
   "description":"Select the exported file type.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "hidden":false,
   "enum":[
      "csv",
      "json",
      "parquet"
   ],
   "default":"csv"
},
{
   "name":"compression",
   "title":"Compression format",
   "description":"Select the desired file compression format.",
   "type":"string",
   "isRequired":true,
   "readOnly":false,
   "enum":[
      "SNAPPY",
      "GZIP",
      "DEFLATE",
      "NONE"
   ]
}
]
```

![Image indiquant l’ordre des options de formatage de fichier dans l’interface utilisateur d’Experience Platform.](../../assets/functionality/destination-configuration/customer-data-fields-order.png)

## Regroupement des champs de données clients {#grouping}

Vous pouvez regrouper plusieurs champs de données client dans une seule section. Pendant la configuration de la connexion à la destination dans l’interface utilisateur, les utilisateurs peuvent voir et bénéficier d’un regroupement visuel par champs similaires.

Pour ce faire, utilisez `"type": "object"` pour créer le groupe et collecter les champs de données client de votre choix dans un objet `properties`, comme illustré dans l’image ci-dessous, où le regroupement **[!UICONTROL Options CSV]** est surligné.

```json {line-numbers="true" highlight="6-28"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Image montrant le regroupement des champs de données client dans l’interface utilisateur.](../../assets/functionality/destination-configuration/group-customer-data-fields.png)

## Création de sélecteurs de liste déroulante pour les champs de données client {#dropdown-selectors}

Dans les cas où vous souhaitez permettre aux utilisateurs de sélectionner plusieurs options (par exemple, le caractère qui doit être utilisé pour délimiter les champs dans les fichiers CSV), vous pouvez ajouter des champs de liste déroulante à l’interface utilisateur.

Pour ce faire, utilisez l’objet `namedEnum` comme illustré ci-dessous et configurez une valeur `default` pour les options que l’utilisateur peut sélectionner.

```json {line-numbers="true" highlight="15-24"}
"customerDataFields":[
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ]
   }
]
```

![Enregistrement d’écran montrant un exemple de sélecteurs de liste déroulante créée avec la configuration affichée ci-dessus.](../../assets/functionality/destination-configuration/customer-data-fields-dropdown.gif)

## Création de sélecteurs de liste déroulante dynamiques pour les champs de données client {#dynamic-dropdown-selectors}

Dans les cas où vous souhaitez appeler de manière dynamique une API et utiliser la réponse pour renseigner de manière dynamique les options d’un menu déroulant, vous pouvez utiliser un sélecteur de liste déroulante dynamique.

Les sélecteurs de liste déroulante dynamique sont identiques aux [sélecteurs de liste déroulante standard](#dropdown-selectors) de l’interface utilisateur. La seule différence est que les valeurs sont extraites dynamiquement d’une API.

Pour créer un sélecteur de liste déroulante dynamique, vous devez configurer deux composants :

**Étape 1.** [Créez un serveur de destination](../../authoring-api/destination-server/create-destination-server.md#dynamic-dropdown-servers) avec un modèle de `responseFields` pour l’appel API dynamique, comme illustré ci-dessous.

```json
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":" <--YOUR-API-ENDPOINT-PATH--> "
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

**Étape 2.** Utilisez l’objet `dynamicEnum` comme illustré ci-dessous. Dans l’exemple ci-dessous, la liste déroulante `User` est récupérée à l’aide du serveur dynamique.


```json {line-numbers="true" highlight="13-21"}
"customerDataFields": [
  {
    "name": "integrationId",
    "title": "Integration ID",
    "type": "string",
    "isRequired": true
  },
  {
    "name": "userId",
    "title": "User",
    "type": "string",
    "isRequired": true,
    "dynamicEnum": {
      "queryParams": [
        "integrationId"
      ],
      "destinationServerId": "<~dynamic-field-server-id~>",
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "value": "$.list",
      "responseFormat": "NAME_VALUE"
    }
  }
]
```

Définissez le paramètre `destinationServerId` sur l’identifiant du serveur de destination que vous avez créé à l’étape 1. Vous pouvez voir l’identifiant du serveur de destination dans la réponse de l’appel API [récupération d’une configuration de serveur de destination](../../authoring-api/destination-server/retrieve-destination-server.md).

## Créer des champs de données client imbriqués {#nested-fields}

Vous pouvez créer des champs de données client imbriqués pour les modèles d’intégration complexes. Vous pouvez ainsi enchaîner une série de sélections pour le client.

Par exemple, vous pouvez ajouter des champs de données client imbriqués pour obliger les clients à sélectionner un type d’intégration avec votre destination, suivi immédiatement d’une autre sélection. La deuxième sélection est un champ imbriqué dans le type d’intégration.

Pour ajouter un champ imbriqué, utilisez le paramètre `properties` comme illustré ci-dessous. Dans l’exemple de configuration ci-dessous, vous pouvez voir trois champs imbriqués distincts dans le champ de données client **Yourdestination - Paramètres spécifiques à l’intégration** .

>[!TIP]
>
>À partir de la version d’avril 2024, vous pouvez définir un paramètre `isRequired` sur les champs imbriqués. Par exemple, dans le fragment de code de configuration ci-dessous, les deux premiers champs imbriqués sont marqués comme obligatoires (ligne xxx mise en surbrillance) et les clients ne peuvent pas continuer, à moins de sélectionner une valeur pour le champ. Pour en savoir plus sur les champs obligatoires, consultez la section [paramètres pris en charge](#supported-parameters).

```json {line-numbers="true" highlight="11,20"}
    {
      "name": "yourdestination",
      "title": "Yourdestination - Integration Specific Settings",
      "type": "object",
      "properties": [
        {
          "name": "agreement",
          "title": "Advertiser data destination terms agreement. Enter I AGREE.",
          "type": "string",
          "isRequired": true,
          "pattern": "I AGREE",
          "readOnly": false,
          "hidden": false
        },
        {
          "name": "account-name",
          "title": "Account name",
          "type": "string",
          "isRequired": true,
          "readOnly": false,
          "hidden": false
        },
        {
          "name": "email",
          "title": "Email address",
          "type": "string",
          "isRequired": false,
          "pattern": "^[\\w-\\.]+@([\\w-]+\\.)+[\\w-]{2,4}$",
          "readOnly": false,
          "hidden": false
        }
      ],
      "isRequired": false,
      "readOnly": false,
      "hidden": false,
```

## Création de champs de données client conditionnels {#conditional-options}

Vous pouvez créer des champs de données clients conditionnels, qui s’affichent dans le workflow d’activation uniquement quand les utilisateurs sélectionnent une certaine option.

Par exemple, vous pouvez créer des options de mise en forme de fichier conditionnel qui s’afficheront uniquement quand les utilisateurs sélectionneront un type d’exportation de fichiers spécifique.

La configuration ci-dessous crée un regroupement conditionnel pour les options de formatage de fichier CSV. Les options de fichier CSV s’affichent uniquement quand l’utilisateur sélectionne CSV comme type de fichier souhaité pour l’exportation.

Pour définir un champ comme conditionnel, utilisez le paramètre `conditional` comme illustré ci-dessous :

```json
"conditional": {
   "field": "fileType",
   "operator": "EQUALS",
   "value": "CSV"
}
```

Dans un contexte plus large, vous pouvez voir le champ `conditional` utilisé dans la configuration de destination ci-dessous, avec le champ `fileType` et l’objet `csvOptions` dans lequel il est défini. Les champs conditionnels sont définis dans le paramètre `properties` .

```json {line-numbers="true" highlight="3-15, 21-25"}
"customerDataFields":[
   {
      "name":"fileType",
      "title":"File Type",
      "description":"Select your file type",
      "type":"string",
      "isRequired":true,
      "enum":[
         "PARQUET",
         "CSV",
         "JSON"
      ],
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"csvOptions",
      "title":"CSV Options",
      "description":"Select your CSV options",
      "type":"object",
      "conditional":{
         "field":"fileType",
         "operator":"EQUALS",
         "value":"CSV"
      },
      "properties":[
         {
            "name":"delimiter",
            "title":"Delimiter",
            "description":"Select your Delimiter",
            "type":"string",
            "isRequired":false,
            "default":",",
            "namedEnum":[
               {
                  "name":"Comma (,)",
                  "value":","
               },
               {
                  "name":"Tab (\\t)",
                  "value":"\t"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"quote",
            "title":"Quote Character",
            "description":"Select your Quote character",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Double Quotes (\")",
                  "value":"\""
               },
               {
                  "name":"Null Character (\u0000)",
                  "value":"\u0000"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"escape",
            "title":"Escape Character",
            "description":"Select your Escape character",
            "type":"string",
            "isRequired":false,
            "default":"\\",
            "namedEnum":[
               {
                  "name":"Back Slash (\\)",
                  "value":"\\"
               },
               {
                  "name":"Single Quote (')",
                  "value":"'"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"emptyValue",
            "title":"Empty Value",
            "description":"Select the output value of blank fields",
            "type":"string",
            "isRequired":false,
            "default":"",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         },
         {
            "name":"nullValue",
            "title":"Null Value",
            "description":"Select the output value of 'null' fields",
            "type":"string",
            "isRequired":false,
            "default":"null",
            "namedEnum":[
               {
                  "name":"Empty String",
                  "value":""
               },
               {
                  "name":"\"\"",
                  "value":"\"\""
               },
               {
                  "name":"null",
                  "value":"null"
               }
            ],
            "readOnly":false,
            "hidden":false
         }
      ],
      "isRequired":false,
      "readOnly":false,
      "hidden":false
   }
]
```

Vous trouverez ci-dessous l’écran de l’interface utilisateur qui en résulte, en fonction de la configuration ci-dessus. Quand l’utilisateur sélectionne le type de fichier CSV, d’autres options de mise en forme de fichier faisant référence au type de fichier CSV s’affichent dans l’interface utilisateur.

![Enregistrement d’écran affichant l’option de formatage de fichier conditionnel pour les fichiers CSV.](../../assets/functionality/destination-configuration/customer-data-fields-conditional.gif)

## Accès aux champs de données client modélisés {#accessing-templatized-fields}

Lorsque la destination nécessite une entrée utilisateur, vous devez fournir à vos utilisateurs une sélection de champs de données client qu’ils peuvent renseigner via l’interface utilisateur d’Experience Platform. Ensuite, vous devez configurer votre serveur de destination pour lire correctement les données saisies par l’utilisateur dans les champs de données client. Pour ce faire, vous devez utiliser des champs modélisés.

Les champs modélisés utilisent le format `{{customerData.fieldName}}`, où `fieldName` est le nom du champ de données client à partir duquel vous lisez des informations. Tous les champs de données client modélisés sont précédés de `customerData.` et entourés de doubles accolades `{{ }}`.

Prenons par exemple la configuration de destination Amazon S3 suivante :

```json
"customerDataFields":[
   {
      "name":"bucketName",
      "title":"Enter the name of your Amazon S3 bucket",
      "description":"Amazon S3 bucket name",
      "type":"string",
      "isRequired":true,
      "pattern":"(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
      "readOnly":false,
      "hidden":false
   },
   {
      "name":"path",
      "title":"Enter the path to your S3 bucket folder",
      "description":"Enter the path to your S3 bucket folder",
      "type":"string",
      "isRequired":true,
      "pattern":"^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
      "readOnly":false,
      "hidden":false
   }
]
```

Cette configuration invite les utilisateurs à saisir leurs nom du compartiment et chemin d’accès au dossier [!DNL Amazon S3] dans leurs champs de données client respectifs.

Pour qu’Experience Platform se connecte correctement à [!DNL Amazon S3], votre serveur de destination doit être configuré pour lire les valeurs de ces deux champs de données client, comme illustrés ci-dessous :

```json
 "fileBasedS3Destination":{
      "bucketName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucketName}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
```

Les valeurs modélisées `{{customerData.bucketName}}` et `{{customerData.path}}` lisent les valeurs fournies par l’utilisateur pour qu’Experience Platform puisse se connecter à la plateforme de destination.

Pour plus d’informations sur la manière de configurer votre serveur de destination pour lire les champs de modèle, consultez la documentation relative aux [champs codés en dur ou modélisés](../destination-server/server-specs.md#templatized-fields).

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment permettre à vos utilisateurs de saisir des informations dans l’interface utilisateur d’Experience Platform avec les champs de données client. Vous savez également sélectionner le champ de données client approprié à votre cas d’utilisation, ainsi que configurer, classer et regrouper les champs de données client dans l’interface utilisateur d’Experience Platform.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Autorisation OAuth2](oauth2-authorization.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)

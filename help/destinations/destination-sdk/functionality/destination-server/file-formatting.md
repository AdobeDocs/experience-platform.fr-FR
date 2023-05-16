---
description: Découvrez comment configurer les options de formatage de fichier pour les destinations basées sur des fichiers créées avec l’Adobe Experience Platform Destination SDK, via le point de terminaison `/destination-servers`.
title: Configuration du formatage des fichiers
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 25%

---


# Configuration du formatage des fichiers

Destination SDK prend en charge un ensemble flexible de fonctionnalités que vous pouvez configurer en fonction de vos besoins d’intégration. Parmi ces fonctionnalités, la prise en charge de [!DNL CSV] mise en forme des fichiers.

Lorsque vous créez des destinations basées sur des fichiers via Destination SDK, vous pouvez définir la manière dont les fichiers CSV exportés doivent être formatés. Vous pouvez personnaliser de nombreuses options de mise en forme, telles que :

* si le fichier CSV doit inclure un en-tête ;
* Quel caractère utiliser pour les guillemets de valeurs ?
* À quoi doivent ressembler les valeurs vides ?

Selon la configuration de votre destination, les utilisateurs verront certaines options dans l’interface utilisateur lors de la connexion à une destination basée sur des fichiers. Vous pouvez voir à quoi ressemblent ces options dans la variable [options de mise en forme des fichiers pour les destinations basées sur des fichiers](../../../ui/batch-destinations-file-formatting-options.md) documentation.


Les paramètres de mise en forme de fichier font partie de la configuration du serveur de destination pour les destinations basées sur des fichiers.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer les opérations [utiliser la Destination SDK pour configurer une destination basée sur des fichiers ;](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Vous pouvez configurer les options de formatage de fichier à partir du `/authoring/destination-servers` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de serveur de destination](../../authoring-api/destination-server/create-destination-server.md)
* [Mise à jour de la configuration d’un serveur de destination](../../authoring-api/destination-server/update-destination-server.md)

Cette page décrit tous les paramètres de formatage de fichier pris en charge pour les fichiers exportés `CSV` fichiers .

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Non |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Paramètres pris en charge {#supported-parameters}

Vous pouvez modifier plusieurs propriétés des fichiers exportés pour répondre aux exigences du système de réception de fichiers de votre destination, afin de lire et d’interpréter de manière optimale les fichiers reçus d’un Experience Platform.

>[!NOTE]
>
>Les options CSV ne sont disponibles que lors de l’exportation de fichiers CSV. La section `fileConfigurations` n’est pas obligatoire lors de la configuration d’un nouveau serveur de destination. Si vous ne transmettez aucune valeur dans l’appel API pour les options CSV, les valeurs par défaut de la variable [tableau de référence ci-dessous](#file-formatting-reference-and-example) sera utilisé.


## Options CSV dans lesquelles les utilisateurs ne peuvent pas sélectionner d’options de configuration {#file-configuration-templating-none}

Dans l’exemple de configuration ci-dessous, toutes les options CSV sont prédéfinies. Les paramètres d’exportation définis dans chacune des `csvOptions` sont définitifs et les utilisateurs ne peuvent pas les modifier.

```json
"fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        },
        "maxFileRowCount":5000000
    }
```

## Options CSV dans lesquelles les utilisateurs peuvent sélectionner des options de configuration {#file-configuration-templating-pebble}

Dans l’exemple de configuration ci-dessous, aucune des options CSV n’est prédéfinie. Le `value` dans chaque `csvOptions` Les paramètres sont configurés dans un champ de données client correspondant par l’intermédiaire de la fonction `/destinations` point de fin (par exemple, [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) pour le `quote` (option de mise en forme de fichier) et les utilisateurs peuvent utiliser l’interface utilisateur de l’Experience Platform pour sélectionner parmi les différentes options que vous configurez dans le champ de données client correspondant. Vous pouvez voir à quoi ressemblent ces options dans la variable [options de mise en forme des fichiers pour les destinations basées sur des fichiers](../../../ui/batch-destinations-file-formatting-options.md) documentation.

```json
{
   "fileConfigurations":{
      "compression":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
      },
      "fileType":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.fileType}}"
      },
      "csvOptions":{
         "sep":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
         },
         "quote":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
         },
         "escape":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
         },
         "nullValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
         },
         "emptyValue":{
            "templatingStrategy":"PEBBLE_V1",
            "value":"{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
         }
      }
   }
}
```

## Référence et exemples complets pour les options de formatage de fichier prises en charge {#file-formatting-reference-and-example}

>[!TIP]
>
>Les options de formatage de fichier CSV décrites ci-dessous sont également documentées dans la section [Guide Apache Spark pour les fichiers CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Les descriptions utilisées ci-dessous sont extraites du guide Apache Spark.

Vous trouverez ci-dessous une référence complète de toutes les options de formatage de fichier disponibles dans Destination SDK, ainsi que des exemples de sortie pour chaque option.

| Champ | Obligatoire / Facultatif | Description | Valeur par défaut | Exemple de sortie 1 | Exemple de sortie 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obligatoire | Pour chaque option de mise en forme de fichier que vous configurez, vous devez ajouter le paramètre . `templatingStrategy`, qui peut avoir deux valeurs : <br><ul><li>`NONE`: utilisez cette valeur si vous ne prévoyez pas de permettre aux utilisateurs de sélectionner différentes valeurs pour une configuration. Voir [cette configuration](#file-configuration-templating-none) pour un exemple où les options de formatage de fichier sont corrigées.</li><li>`PEBBLE_V1`: utilisez cette valeur si vous souhaitez permettre aux utilisateurs de sélectionner différentes valeurs pour une configuration. Dans ce cas, vous devez également configurer un champ de données client correspondant dans le `/destination` configuration des points de fin, pour faire apparaître les différentes options aux utilisateurs dans l’interface utilisateur. Voir [cette configuration](#file-configuration-templating-pebble) par exemple, où les utilisateurs peuvent sélectionner différentes valeurs pour les options de formatage de fichier.</li></ul> | - | - | - |
| `compression.value` | Facultatif | Codec de compression à utiliser lors de l’enregistrement de données dans un fichier. Valeurs prises en charge : `none`, `bzip2`, `gzip`, `lz4` et `snappy`. | `none` | - | - |
| `fileType.value` | Facultatif | Indique le format du fichier de sortie. Valeurs prises en charge : `csv`, `parquet` et `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour lʼéchappement des valeurs entre guillemets où le séparateur peut faire partie de la valeur. | `null` | - | - |
| `csvOptions.quoteAll.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique si toutes les valeurs doivent toujours être placées entre guillemets. La valeur par défaut est lʼéchappement des valeurs contenant un guillemet. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un séparateur pour chaque champ et valeur. Ce séparateur peut contenir un ou plusieurs caractères. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour lʼéchappement des guillemets dans une valeur déjà entre guillemets. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique si les valeurs contenant des guillemets doivent toujours être placées entre guillemets. La valeur par défaut est lʼéchappement de toutes les valeurs contenant un guillemet. | `true` | - | - |
| `csvOptions.header.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut écrire les noms des colonnes comme première ligne dans le fichier exporté. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut supprimer les espaces de tête des valeurs. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut supprimer les espaces à la fin des valeurs. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la représentation sous forme de chaîne d’une valeur nulle. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique le format de date. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la chaîne qui indique un format d’horodatage. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour l’échappement du caractère de guillemet. | `\` lorsque les caractères d’échappement et de guillemet sont différents. `\0` lorsque les caractères d’échappement et de guillemet sont identiques. | - | - |
| `csvOptions.emptyValue.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la représentation sous forme de chaîne d’une valeur vide. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre le fonctionnement du formatage des fichiers dans la configuration d’un serveur de destination et comment le configurer.

Pour en savoir plus sur les autres composants du serveur de destination, consultez les articles suivants :

* [Spécifications de serveur pour les destinations créées avec Destination SDK](server-specs.md)
* [Spécifications du modèle](templating-specs.md)
* [Format des messages](message-format.md)
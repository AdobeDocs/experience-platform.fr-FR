---
description: Découvrez comment configurer les options de formatage de fichier pour les destinations basées sur des fichiers créés avec Adobe Experience Platform Destination SDK, via le point d’entrée `/destination-servers`.
title: Configuration du formatage des fichiers
exl-id: 98fec559-9073-4517-a10e-34c2caf292d5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 88%

---

# Configuration du formatage des fichiers

Destination SDK prend en charge un ensemble flexible de fonctionnalités que vous pouvez configurer en fonction de vos besoins d’intégration. Parmi ces fonctionnalités, on trouve la prise en charge du formatage des fichiers [!DNL CSV].

Quand vous créez des destinations basées sur des fichiers avec Destination SDK, vous pouvez définir le formatage des fichiers CSV exportés. Vous pouvez personnaliser de nombreuses options de mise en forme, notamment, mais sans s’y limiter :

* si le fichier CSV doit inclure un en-tête ;
* quel caractère utiliser pour les valeurs entre guillemets ;
* à quoi doivent ressembler les valeurs vides.

Selon la configuration de la destination, les utilisateurs verront certaines options dans l’interface utilisateur pendant la connexion à une destination basée sur des fichiers. Vous pouvez voir à quoi ressemblent ces options dans les [options de mise en forme des fichiers pour les destinations basées sur des fichiers](../../../ui/batch-destinations-file-formatting-options.md).


Les paramètres de formatage de fichiers font partie de la configuration de serveur de destination quand celles-ci sont basées sur des fichiers.

Pour comprendre la place de ce composant dans une intégration créée avec Destination SDK, consultez le diagramme de la documentation [options de configuration](../configuration-options.md) ou consultez le guide sur la [utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Vous pouvez configurer les options de formatage de fichier via le point d’entrée `/authoring/destination-servers`. Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de serveur de destination](../../authoring-api/destination-server/create-destination-server.md)
* [Mise à jour d’une configuration de serveur de destination](../../authoring-api/destination-server/update-destination-server.md)

Cette page décrit tous les paramètres de formatage de fichier pris en charge pour les fichiers `CSV` exportés.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Pour en savoir plus sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page, consultez le tableau ci-dessous.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (streaming) | Non |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Paramètres pris en charge {#supported-parameters}

Vous pouvez modifier plusieurs propriétés des fichiers exportés pour répondre aux exigences de votre système de réception de fichiers de destination, afin de lire et d’interpréter de manière optimale les fichiers provenant d’Experience Platform.

>[!NOTE]
>
>Les options CSV ne sont disponibles que lors de l’exportation de fichiers CSV. La section `fileConfigurations` n’est pas obligatoire lors de la configuration d’un nouveau serveur de destination. Si vous ne transmettez aucune valeur dans l’appel API pour les options CSV, les valeurs par défaut du [tableau de référence ci-dessous](#file-formatting-reference-and-example) seront utilisées.


## Options sCSV dans lesquelles les utilisateurs ne peuvent pas sélectionner d’options de configuration {#file-configuration-templating-none}

Dans l’exemple de configuration ci-dessous, toutes les options CSV sont prédéfinies. Les paramètres d’exportation définis dans chacune des options `csvOptions` sont définitifs et les utilisateurs ne peuvent pas les modifier.

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
        "maxFileRowCount":5000000,
        "includeFileManifest": {
            "templatingStrategy":"PEBBLE_V1",
            "value":"{{ customerData.includeFileManifest }}"
      }
    }
```

## Options CSV dans lesquelles les utilisateurs peuvent sélectionner des options de configuration {#file-configuration-templating-pebble}

Dans l’exemple de configuration ci-dessous, aucune des options CSV n’est prédéfinie. La `value` de chaque paramètre `csvOptions` est configurée dans un champ de données client correspondant avec le point d’entrée `/destinations` (par exemple, [`customerData.quote`](../../functionality/destination-configuration/customer-data-fields.md#conditional-options) pour l’option de mise en forme de fichier `quote`) et les utilisateurs peuvent utiliser l’interface utilisateur d’Experience Platform pour sélectionner une option que vous configurez dans le champ de données client correspondant. Vous pouvez voir à quoi ressemblent ces options dans les [options de mise en forme des fichiers pour les destinations basées sur des fichiers](../../../ui/batch-destinations-file-formatting-options.md).

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
      },
      "maxFileRowCount":5000000,
      "includeFileManifest": {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{ customerData.includeFileManifest }}"
      }
   }
}
```

## Référence et exemples complets pour les options de formatage de fichier prises en charge {#file-formatting-reference-and-example}

>[!TIP]
>
>Les options de formatage de fichiers CSV décrites ci-dessous sont également documentées dans la section [Guide Apache Spark pour les fichiers CSV](https://spark.apache.org/docs/latest/sql-data-sources-csv.html). Les descriptions utilisées ci-dessous sont extraites du guide Apache Spark.

Vous trouverez ci-dessous une référence complète de toutes les options de formatage de fichier disponibles dans Destination SDK, ainsi que des exemples de sortie pour chaque option.

| Champ | Obligatoire / Facultatif | Description | Valeur par défaut | Exemple de sortie 1 | Exemple de sortie 2 |
|---|---|---|---|---|---|
| `templatingStrategy` | Obligatoire | Pour chaque option de formatage de fichier que vous configurez, vous devez ajouter le paramètre `templatingStrategy`, qui peut avoir deux valeurs : <br><ul><li>`NONE` : utilisez cette valeur si vous n’envisagez pas de donner aux utilisateurs la possibilité de choisir entre différentes valeurs pour une configuration. Pour obtenir un exemple d’options de formatage de fichier corrigées, consultez [cette configuration](#file-configuration-templating-none).</li><li>`PEBBLE_V1` : utilisez cette valeur si vous souhaitez donner aux utilisateurs la possibilité de choisir entre différentes valeurs pour une configuration. Dans ce cas, vous devez également configurer un champ de données client correspondant dans la configuration des points d’entrées `/destination`, pour faire apparaître les différentes options aux utilisateurs dans l’interface utilisateur. Pour obtenir un exemple où les utilisateurs peuvent sélectionner différentes valeurs pour les options de formatage de fichier, consultez [cette configuration](#file-configuration-templating-pebble).</li></ul> | - | - | - |
| `compression.value` | Facultatif | Codec de compression à utiliser lors de l’enregistrement de données dans un fichier. Valeurs prises en charge : `none`, `bzip2`, `gzip`, `lz4` et `snappy`. | `none` | - | - |
| `fileType.value` | Facultatif | Indique le format du fichier de sortie. Valeurs prises en charge : `csv`, `parquet` et `json`. | `csv` | - | - |
| `csvOptions.quote.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour lʼéchappement des valeurs entre guillemets où le séparateur peut faire partie de la valeur. | `null` | Exemple de valeur par défaut : `quote.value: "u0000"` —> `male,NULJohn,LastNameNUL` | Exemple personnalisé : `quote.value: "\""` —> `male,"John,LastName"` |
| `csvOptions.quoteAll.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique si toutes les valeurs doivent toujours être placées entre guillemets. La valeur par défaut est lʼéchappement des valeurs contenant un guillemet. | `false` | `quoteAll`:`false` --> `male,John,"TestLastName"` | `quoteAll`:`true` -->`"male","John","TestLastName"` |
| `csvOptions.delimiter.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un séparateur pour chaque champ et valeur. Ce séparateur peut contenir un ou plusieurs caractères. | `,` | `delimiter`:`,` --> `comma-separated values"` | `delimiter`:`\t` --> `tab-separated values` |
| `csvOptions.escape.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour lʼéchappement des guillemets dans une valeur déjà entre guillemets. | `\` | `"escape"`:`"\\"` --> `male,John,"Test,\"LastName5"` | `"escape"`:`"'"` --> `male,John,"Test,'''"LastName5"` |
| `csvOptions.escapeQuotes.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique si les valeurs contenant des guillemets doivent toujours être placées entre guillemets. La valeur par défaut est lʼéchappement de toutes les valeurs contenant un guillemet. | `true` | - | - |
| `csvOptions.header.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique si les noms des colonnes doivent être écrits sur la première ligne du fichier exporté. | `true` | - | - |
| `csvOptions.ignoreLeadingWhiteSpace.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut supprimer les espaces de tête des valeurs. | `true` | `ignoreLeadingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreLeadingWhiteSpace`:`false`--> `"    male","John","TestLastName"` |
| `csvOptions.ignoreTrailingWhiteSpace.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique s’il faut supprimer les espaces blancs à la fin des valeurs. | `true` | `ignoreTrailingWhiteSpace`:`true` --> `"male","John","TestLastName"` | `ignoreTrailingWhiteSpace`:`false`--> `"male    ","John","TestLastName"` |
| `csvOptions.nullValue.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la représentation sous forme de chaîne d’une valeur nulle. | `""` | `nullvalue`:`""` --> `male,"",TestLastName` | `nullvalue`:`"NULL"` --> `male,NULL,TestLastName` |
| `csvOptions.dateFormat.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Indique le format de date. | `yyyy-MM-dd` | `dateFormat`:`yyyy-MM-dd` --> `male,TestLastName,John,2022-02-24` | `dateFormat`:`MM/dd/yyyy` --> `male,TestLastName,John,02/24/2022` |
| `csvOptions.timestampFormat.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la chaîne qui indique un format d’horodatage. | `yyyy-MM-dd'T'HH:mm:ss[.SSS][XXX]` | - | - |
| `csvOptions.charToEscapeQuoteEscaping.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit un caractère unique utilisé pour l’échappement du caractère de guillemet. | `\` lorsque les caractères d’échappement et de guillemet sont différents. `\0` lorsque les caractères d’échappement et de guillemet sont identiques. | - | - |
| `csvOptions.emptyValue.value` | Facultatif | *Uniquement pour`"fileType.value": "csv"`*. Définit la représentation sous forme de chaîne d’une valeur vide. | `""` | `"emptyValue":""` --> `male,"",John` | `"emptyValue":"empty"` --> `male,empty,John` |
| `maxFileRowCount` | Facultatif | Indique le nombre maximal de lignes par fichier exporté, entre 1 000 000 et 10 000 000 de lignes. | 5 000 000 | - | - |
| `includeFileManifest` | Facultatif | Active la prise en charge de l’exportation d’un manifeste de fichier avec les exportations de fichiers. Le fichier JSON manifeste contient des informations sur l’emplacement d’exportation, la taille d’exportation, etc. Le manifeste est nommé à l’aide du format `manifest-<<destinationId>>-<<dataflowRunId>>.json`. | Affichez un [exemple de fichier de manifeste](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Le fichier manifeste comprend les champs suivants : <ul><li>`flowRunId` : exécution [flux de données](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) qui a généré le fichier exporté.</li><li>`scheduledTime` : heure en UTC à laquelle le fichier a été exporté. </li><li>`exportResults.sinkPath` : chemin d’accès à l’emplacement de stockage où le fichier exporté est déposé. </li><li>`exportResults.name` : nom du fichier exporté.</li><li>`size` : taille du fichier exporté, en octets.</li></ul> | - | - |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre le fonctionnement du formatage des fichiers dans la configuration d’un serveur de destination et comment le configurer.

Pour en savoir plus sur les autres composants de serveur de destination, consultez les articles suivants :

* [Spécifications de serveur pour les destinations créées avec Destination SDK](server-specs.md)
* [Spécifications du modèle](templating-specs.md)
* [Format des messages](message-format.md)

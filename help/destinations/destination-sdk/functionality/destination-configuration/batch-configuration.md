---
description: Découvrez comment configurer les paramètres d’exportation de fichiers pour les destinations créées avec Destination SDK.
title: Configuration par lots
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 18%

---


# Configuration par lots {#batch-configuration}

Utilisez les options de configuration par lot de Destination SDK pour permettre aux utilisateurs de personnaliser les noms des fichiers exportés et de configurer le planning d’exportation selon leurs préférences.

Lorsque vous créez des destinations basées sur des fichiers par le biais de Destination SDK, vous pouvez configurer le nommage de fichiers et les plannings d’exportation par défaut, ou vous pouvez donner aux utilisateurs la possibilité de configurer ces paramètres à partir de l’interface utilisateur de Platform. Par exemple, vous pouvez configurer des comportements tels que :

* Inclusion d’informations spécifiques dans le nom de fichier, telles que des identifiants de segment, des identifiants de destination ou des informations personnalisées.
* Permet aux utilisateurs de personnaliser l’attribution du nom des fichiers à partir de l’interface utilisateur de Platform.
* Configurez les exportations de fichiers pour qu’elles se produisent à des intervalles de temps définis.
* Définissez les options de personnalisation du nom de fichier et du planning d’exportation que les utilisateurs peuvent voir dans l’interface utilisateur de Platform.

Les paramètres de configuration de lot font partie de la configuration de destination pour les destinations basées sur des fichiers.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer les opérations [utiliser la Destination SDK pour configurer une destination basée sur des fichiers ;](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Vous pouvez configurer l’attribution de noms aux fichiers et les paramètres du planning d’exportation à l’aide du `/authoring/destinations` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les options de configuration par lots prises en charge que vous pouvez utiliser pour votre destination et indique ce que les clients verront dans l’interface utilisateur de Platform.

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

Les valeurs que vous configurez ici sont affichées dans la variable [Planification de l’exportation de segments](../../../ui/activate-batch-profile-destinations.md#scheduling) de l’étape du workflow d’activation des destinations basées sur des fichiers.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| Paramètre | Type | Description |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booléen | Définissez cette valeur sur `true` afin de permettre aux clients de spécifier les attributs de profil obligatoires. La valeur par défaut est `false`. Pour plus d’informations, consultez la section [Attributs obligatoires](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `allowDedupeKeyFieldSelection` | Booléen | Définissez cette valeur sur `true` afin de permettre aux clients de spécifier des clés de déduplication. La valeur par défaut est `false`. Pour plus d’informations, consultez la section [Clés de déduplication](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `defaultExportMode` | Énumération | Définit le mode d’exportation de fichier par défaut. Valeurs prises en charge :<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> La valeur par défaut est `DAILY_FULL_EXPORT`. Pour plus d’informations sur la planification des exportations de fichiers, consultez la [documentation sur l’activation par lots](../../../ui/activate-batch-profile-destinations.md#scheduling). |
| `allowedExportModes` | Liste | Définit les modes d’exportation de fichiers disponibles pour les clients. Valeurs prises en charge :<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Liste | Définit la fréquence d’exportation des fichiers disponible pour les clients. Valeurs prises en charge :<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Énumération | Définit la fréquence d’exportation des fichiers par défaut. Les valeurs prises en charge sont les suivantes :<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> La valeur par défaut est `DAILY`. |
| `defaultStartTime` | Chaîne | Définit l’heure de début par défaut de l’exportation du fichier. Utilise le format de fichier de 24 heures. La valeur par défaut est « 00:00 ». |
| `filenameConfig.allowedFilenameAppendOptions` | Chaîne | *Obligatoire*. Liste des macros de nom de fichier disponibles à l’intention des utilisateurs. Cela détermine les éléments qui sont ajoutés aux noms de fichier exportés (ID de segment, nom de l’organisation, date et heure de l’exportation, etc.). Lorsque vous définissez `defaultFilename`, veillez à éviter la duplication des macros. <br><br>Valeurs prises en charge : <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Quel que soit l’ordre dans lequel vous définissez les macros, l’interface utilisateur de l’Experience Platform les affiche toujours dans l’ordre présenté ici. <br><br> If `defaultFilename` est vide, la variable `allowedFilenameAppendOptions` La liste doit contenir au moins une macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Chaîne | *Obligatoire*. Macros de nom de fichier par défaut présélectionnées que les utilisateurs peuvent décocher.<br><br> Les macros de cette liste sont un sous-ensemble de celles définies dans la variable `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Chaîne | *Facultatif*. Définit les macros de nom de fichier par défaut pour les fichiers exportés. Ils ne peuvent pas être remplacés par les utilisateurs. <br><br>Toute macro définie par `allowedFilenameAppendOptions` sera annexé après l’événement `defaultFilename` macros. <br><br>If `defaultFilename` est vide, vous devez définir au moins une macro dans `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## Configuration du nom de fichier {#file-name-configuration}

Utilisez les macros de configuration des noms de fichier pour définir les noms de fichier exportés à inclure. Les macros du tableau ci-dessous décrivent les éléments figurant dans l’interface utilisateur de la fonction [configuration du nom de fichier](../../../ui/activate-batch-profile-destinations.md#file-names) écran.

>[!TIP]
> 
>En règle générale, vous devez toujours inclure la variable `SEGMENT_ID` macro dans les noms de fichiers exportés. Les identifiants de segment sont uniques. Par conséquent, leur inclusion dans le nom de fichier est la meilleure manière de s’assurer que les noms de fichier sont également uniques.

| Macro | Libellé de l’interface utilisateur | Description | Exemple |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destination] | Nom de la destination dans l’interface utilisateur. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Identifiant de segment] | Identifiant de segment unique généré par Platform | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nom du segment] | Nom de segment défini par l’utilisateur | abonné VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Identifiant de destination] | Identifiant unique généré par Platform de l’instance de destination. | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nom de la destination] | Nom défini par l’utilisateur de l’instance de destination. | Ma destination publicitaire 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nom de l’organisation] | Nom de l’organisation du client dans Adobe Experience Platform. | Mon nom d’organisation |
| `SANDBOX_NAME` | [!UICONTROL Nom du sandbox] | Nom de l’environnement de test utilisé par le client. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Date et heure] | `DATETIME` et `TIMESTAMP` les deux définissent le moment où le fichier a été généré, mais dans des formats différents. <br><br><ul><li>`DATETIME` utilise le format suivant : YYYYMMDD_HHMMSS.</li><li>`TIMESTAMP` utilise le format Unix à 10 chiffres. </li></ul> `DATETIME` et `TIMESTAMP` s’excluent mutuellement et ne peuvent pas être utilisés simultanément. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texte personnalisé] | Texte personnalisé défini par l’utilisateur à inclure dans le nom du fichier. Ne peut pas être utilisé dans `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Date et heure] | Horodatage à 10 chiffres de l’heure de génération du fichier, au format Unix. | 1652131584 |

{style="table-layout:auto"}

### Exemple de configuration de nom de fichier

L’exemple de configuration ci-dessous illustre la correspondance entre la configuration utilisée dans l’appel API et les options affichées dans l’interface utilisateur.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![Image de l’interface utilisateur affichant l’écran de configuration du nom de fichier avec les macros présélectionnées](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer l’attribution de noms aux fichiers et les calendriers d’exportation pour vos destinations basées sur les fichiers.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Configuration de l’authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)
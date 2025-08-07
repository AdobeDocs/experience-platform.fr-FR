---
description: Découvrez comment configurer les paramètres d’exportation de fichiers pour les destinations créées avec Destination SDK.
title: Configuration par lots
exl-id: 0ffbd558-a83c-4c3d-b4fc-b6f7a23a163a
source-git-commit: 8e7356bdc5692678e46a61b538d4b6748792a423
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 86%

---

# Configuration par lots {#batch-configuration}

Utilisez les options de configuration par lots de Destination SDK pour permettre aux utilisateurs de personnaliser les noms des fichiers exportés et de configurer le planning d’exportation en fonction de leurs préférences.

Lorsque vous créez des destinations basées sur des fichiers via Destination SDK, vous pouvez configurer les noms de fichiers et les plannings d’exportation par défaut, ou permettre aux utilisateurs de configurer ces paramètres à partir de l’interface utilisateur d’Experience Platform. Par exemple, vous pouvez configurer des comportements tels que :

* Ajouter des informations spécifiques dans le nom du fichier, telles que des identifiants d’audience, des identifiants de destination ou des informations personnalisées.
* Permettre aux utilisateurs de personnaliser le nom des fichiers à partir de l’interface utilisateur d’Experience Platform.
* Configurer des exportations de fichiers à des intervalles de temps définis.
* Définir les options de dénomination des fichiers et de planning d’exportation que les utilisateurs peuvent voir dans l’interface utilisateur d’Experience Platform.

Les paramètres de configuration par lots font partie de la configuration de destination pour les destinations basées sur des fichiers.

Pour comprendre la place de ce composant dans une intégration créée avec Destination SDK, consultez le diagramme de la documentation [options de configuration](../configuration-options.md) ou consultez le guide sur la [utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Vous pouvez configurer les noms de fichiers et les paramètres du planning d’exportation via le point d’entrée `/authoring/destinations`. Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les options de configuration par lots prises en charge que vous pouvez utiliser pour la destination et montre ce que la clientèle verra dans l’interface utilisateur d’Experience Platform.

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

Les valeurs que vous configurez ici sont affichées à l’étape [Planifier l’exportation d’audiences](../../../ui/activate-batch-profile-destinations.md#scheduling) du workflow d’activation des destinations basées sur des fichiers.

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
      "ONCE",
      "WEEKLY",
      "MONTHLY"
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
   "segmentGroupingEnabled": true
   }
```

| Paramètre | Type | Description |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booléen | Définissez cette valeur sur `true` afin de permettre la spécification des attributs de profil obligatoires. La valeur par défaut est `false`. Pour plus d’informations, consultez la section [Attributs obligatoires](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `allowDedupeKeyFieldSelection` | Booléen | Définissez cette valeur sur `true` afin de permettre la spécification des clés de déduplication. La valeur par défaut est `false`. Pour plus d’informations, consultez la section [Clés de déduplication](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `defaultExportMode` | Énumération | Définit le mode d’exportation de fichier par défaut. Valeurs prises en charge :<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> La valeur par défaut est `DAILY_FULL_EXPORT`. Pour plus d’informations sur la planification des exportations de fichiers, consultez la [documentation sur l’activation par lots](../../../ui/activate-batch-profile-destinations.md#scheduling). |
| `allowedExportModes` | Liste | Définit les modes d’exportation de fichiers disponibles pour les clients. Valeurs prises en charge :<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Liste | Définit la fréquence d’exportation des fichiers disponible pour les clients. Valeurs prises en charge :<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li><li>`WEEKLY`</li><li>`MONTHLY`</li></ul> |
| `defaultFrequency` | Énumération | Définit la fréquence d’exportation des fichiers par défaut. Les valeurs prises en charge sont les suivantes :<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li><li>`WEEKLY`</li><li>`MONTHLY`</li></ul> La valeur par défaut est `DAILY`. |
| `defaultStartTime` | Chaîne | Définit l’heure de début par défaut de l’exportation du fichier. Utilise le format de fichier de 24 heures. La valeur par défaut est « 00:00 ». |
| `filenameConfig.allowedFilenameAppendOptions` | Chaîne | *Obligatoire*. Liste des macros de nom de fichier disponibles. Cela détermine les éléments qui sont ajoutés aux noms de fichier exportés (identifiant d’audience, nom de l’organisation, date et heure de l’exportation, etc.). Quand vous définissez `defaultFilename`, veillez à ne pas dupliquer les macros. <br><br>Valeurs prises en charge : <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Quel que soit l’ordre dans lequel vous définissez les macros, l’interface utilisateur d’Experience Platform les affiche toujours dans l’ordre présenté ici. <br><br> Si `defaultFilename` est vide, la liste `allowedFilenameAppendOptions` doit contenir au moins une macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Chaîne | *Obligatoire*. Macros de nom de fichier par défaut présélectionnées que les utilisateurs peuvent décocher.<br><br> Les macros de cette liste sont un sous-ensemble de celles définies dans `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Chaîne | *Facultatif*. Définit les macros de nom de fichier par défaut pour les fichiers exportés. Elles ne peuvent pas être modifiées par les utilisateurs. <br><br>Toute macro définie par `allowedFilenameAppendOptions` sera ajoutée après les macros `defaultFilename`. <br><br>Si `defaultFilename` est vide, vous devez définir au moins une macro dans `allowedFilenameAppendOptions`. |
| `segmentGroupingEnabled` | Booléen | Définit si les audiences activées doivent être exportées dans un ou plusieurs fichiers, selon la [politique de fusion](../../../../profile/merge-policies/overview.md) des audiences. Valeurs prises en charge : <ul><li>`true` : exporte un fichier par politique de fusion.</li><li>`false` : exporte un fichier par audience, quelle que soit la politique de fusion. Il s’agit du comportement par défaut. Vous pouvez obtenir le même résultat en omettant complètement ce paramètre.</li></ul> |

{style="table-layout:auto"}

## Configuration du nom du fichier {#file-name-configuration}

Utilisez les macros de configuration des noms de fichiers pour définir les noms de fichiers exportés à inclure. Les macros du tableau ci-dessous décrivent les éléments figurant dans l’interface utilisateur de l’écran [configuration du nom du fichier](../../../ui/activate-batch-profile-destinations.md#file-names).

>[!TIP]
> 
>En règle générale, vous devez toujours inclure la macro `SEGMENT_ID` dans les noms de fichiers exportés. Les identifiants de segment sont uniques. Ainsi, la meilleure manière de s’assurer que les noms de fichiers sont également uniques est de les inclure dans le nom du fichier.

| Macro | Libellé de l’interface utilisateur | Description | Exemple |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destination] | Nom de la destination dans l’interface utilisateur. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Identifiant de segment] | ID d’audience unique généré par Experience Platform | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nom du segment] | Nom d’audience défini par l’utilisateur ou l’utilisatrice | abonné VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Identifiant de destination] | Identifiant unique de l’instance de destination, généré par Experience Platform | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nom de la destination] | Nom défini par l’utilisateur de l’instance de destination. | Ma destination publicitaire 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nom de l’organisation] | Nom de l’organisation du client dans Adobe Experience Platform. | Mon nom d’organisation |
| `SANDBOX_NAME` | [!UICONTROL Nom du sandbox] | Nom du sandbox utilisé par le client. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Date et heure] | `DATETIME` et `TIMESTAMP` définissent tous deux le moment où le fichier a été généré, mais dans des formats différents. <br><br><ul><li>`DATETIME` utilise le format suivant : AAAAMMJJ_HHMMSS.</li><li>`TIMESTAMP` utilise le format Unix à 10 chiffres. </li></ul> `DATETIME` et `TIMESTAMP` s’excluent mutuellement et ne peuvent pas être utilisés simultanément. | <ul><li>`DATETIME` : 20220509_210543</li><li>`TIMESTAMP` : 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texte personnalisé] | Texte personnalisé défini par l’utilisateur à inclure dans le nom du fichier. Ne peut pas être utilisé dans `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Date et heure] | Date et heure à 10 chiffres indiquant l’heure à laquelle le fichier a été généré, au format Unix. | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL Identifiant de la politique de fusion] | Identifiant de la [politique de fusion](../../../../profile/merge-policies/overview.md) utilisé pour générer l’audience exportée. Utilisez cette macro lorsque vous regroupez des audiences exportées dans des fichiers, en fonction d’une politique de fusion. Utilisez cette macro avec `segmentGroupingEnabled:true`. | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL Nom de la politique de fusion] | Nom de la [politique de fusion](../../../../profile/merge-policies/overview.md) utilisé pour générer l’audience exportée. Utilisez cette macro lorsque vous regroupez des audiences exportées dans des fichiers, en fonction d’une politique de fusion. Utilisez cette macro avec `segmentGroupingEnabled:true`. | Ma politique de fusion personnalisée |

{style="table-layout:auto"}

### Exemple de configuration de nom de fichier

L’exemple de configuration ci-dessous montre la correspondance entre la configuration utilisée dans l’appel API et les options affichées dans l’interface utilisateur.

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

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment configurer les noms de fichiers et la planification des exportations pour vos destinations basées sur les fichiers.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Configuration de l’authentification du client](customer-authentication.md)
* [Autorisation OAuth2](oauth2-authorization.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)

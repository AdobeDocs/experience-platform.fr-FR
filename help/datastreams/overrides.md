---
title: Configurer les remplacements de trains de données
description: Découvrez comment configurer les remplacements de flux de données dans l’interface utilisateur des flux de données et les activer via le SDK web ou le SDK mobile.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 17ed5f3c14d4787352f72d3d7721cbb6416d533e
workflow-type: tm+mt
source-wordcount: '1081'
ht-degree: 57%

---

# Configurer les remplacements de trains de données

Les remplacements de flux de données vous permettent de définir des configurations supplémentaires pour vos flux de données, qui sont transmises à l’Edge Network par le biais du SDK Web ou du SDK mobile.

Vous pouvez ainsi déclencher différents comportements de flux de données par rapport aux comportements par défaut, sans créer de flux de données ni modifier vos paramètres existants.

Le remplacement de la configuration du flux de données est un processus en deux étapes :

1. Tout d’abord, vous devez définir le remplacement de la configuration du flux de données dans la [page de configuration du flux de données](configure.md).
2. Ensuite, vous devez envoyer les remplacements à l’Edge Network de l’une des façons suivantes :
   * Par le biais des commandes `sendEvent` ou `configure` [SDK Web](#send-overrides) .
   * Par le biais du SDK Web [extension de balise](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * Grâce à l’API [sendEvent](#send-overrides) du SDK Mobile ou à l’aide de [Rules](#send-overrides).

Cet article décrit le processus de remplacement de configuration des trains de données de bout en bout pour chaque type de remplacement pris en charge.

>[!IMPORTANT]
>
>Les remplacements de flux de données ne sont pris en charge que pour les intégrations [SDK Web](../web-sdk/home.md) et [SDK mobile](https://developer.adobe.com/client-sdks/home/). Les intégrations [API serveur](../server-api/overview.md) ne prennent actuellement pas en charge les remplacements de flux de données.
><br>
>Utilisez les remplacements de trains de données pour envoyer différentes données à différents trains de données. N’utilisez pas de remplacements de flux de données pour les cas d’utilisation de la personnalisation ou les données de consentement.

## Cas d’utilisation {#use-cases}

Pour découvrir les avantages des remplacements de trains de données et leur utilisation, consultez les cas d’utilisation ci-dessous que la clientèle d’Adobe Experience Platform peut résoudre.

**Collecte de données dans plusieurs zones géographiques**

Une entreprise possède des sites web ou des sous-domaines distincts pour chaque pays dans lequel elle opère. Elle a [configuré](configure.md) des trains de données distincts avec des suites de rapports d’analyse spécifiques, des jetons de propriété Adobe Target et des schémas spécifiques à chaque pays, ainsi que des jeux de données, des configurations Journey Optimizer, etc. L’entreprise dispose également d’un jeu global de configurations où toutes les données spécifiques à un pays sont agrégées.

Grâce aux remplacements de trains de données, l’entreprise peut acheminer dynamiquement le flux de données vers différents trains de données, au lieu du comportement par défaut consistant à envoyer des données à un train de données unique.

Un cas d’utilisation courant peut être l’envoi de données à un flux de données spécifique à un pays, ainsi qu’à un flux de données global dans lequel les clients effectuent une action importante, comme passer une commande ou mettre à jour leur profil utilisateur.

**Différencier les profils et les identités pour chaque unité commerciale**

Une entreprise qui possède plusieurs unités opérationnelles souhaite utiliser plusieurs environnements de test Experience Platform pour stocker des données spécifiques à chaque unité opérationnelle.

Au lieu d’envoyer les données à un train de données par défaut, l’entreprise peut utiliser les remplacements de trains de données pour s’assurer que chaque unité commerciale dispose de son propre train de données pour recevoir les données.

## Configurer les remplacements de trains de données dans l’interface utilisateur des trains de données {#configure-overrides}

Les remplacements de configuration des trains de données vous permettent de modifier les configurations de trains de données suivantes :

* Jeux de données d’événement Experience Platform
* Jetons de propriété Adobe Target
* Conteneurs de synchronisation d’identifiants Audience Manager
* Suites de rapports Adobe Analytics

### Remplacements de trains de données pour Adobe Target {#target-overrides}

Pour configurer les remplacements de trains de données pour un train de données Adobe Target, vous devez d’abord créer un train de données Adobe Target. Suivez la procédure pour [configurer un train de données](configure.md) avec le service [Adobe Target](configure.md#target).

Une fois que vous avez créé le flux de données, modifiez le service [Adobe Target](configure.md#target) que vous avez ajouté et utilisez la section **[!UICONTROL Remplacements de jeton de propriété]** pour ajouter les remplacements de flux de données souhaités, comme illustré dans l’image ci-dessous. Ajoutez un jeton de propriété par ligne.

![Copie d’écran de l’interface utilisateur des trains de données montrant les paramètres du service Adobe Target, avec les remplacements de jetons de propriété mis en surbrillance.](assets/overrides/override-target.png)

Une fois que vous avez ajouté les remplacements souhaités, enregistrez les paramètres du train de données.

La configuration des remplacements de trains de données pour Adobe Target est terminée. Désormais, vous pouvez [envoyer les remplacements à l’Edge Network via le SDK Web ou le SDK Mobile](#send-overrides).

### Remplacements de trains de données pour Adobe Analytics {#analytics-overrides}

Pour configurer les remplacements de trains de données d’un train de données Adobe Analytics, vous devez d’abord créer un train de données [Adobe Analytics](configure.md#analytics). Suivez la procédure pour [configurer un train de données](configure.md) avec le service [Adobe Analytics](configure.md#analytics).

Une fois que vous avez créé le flux de données, modifiez le service [Adobe Analytics](configure.md#target) que vous avez ajouté et utilisez la section **[!UICONTROL Report Suite Overrides]** pour ajouter les remplacements de flux de données souhaités, comme illustré dans l’image ci-dessous.

Sélectionnez **[!UICONTROL Afficher le mode par lots]** pour activer la modification par lots des remplacements de suites de rapports. Vous pouvez copier et coller une liste de remplacements de suites de rapports. Saisissez une suite de rapports par ligne.

![Copie d’écran de l’interface utilisateur des trains de données montrant les paramètres du service Adobe Analytics, avec les remplacements de suites de rapports mis en surbrillance.](assets/overrides/override-analytics.png)

Une fois que vous avez ajouté les remplacements souhaités, enregistrez les paramètres du train de données.

La configuration des remplacements de trains de données Adobe Analytics est terminée. Désormais, vous pouvez [envoyer les remplacements à l’Edge Network via le SDK Web ou le SDK Mobile](#send-overrides).

### Remplacements de trains de données pour les jeux de données d’événements Experience Platform {#event-dataset-overrides}

Pour configurer les remplacements de trains de données pour les jeux de données d’événements Experience Platform, vous devez d’abord créer un train de données [Adobe Experience Platform](configure.md#aep). Suivez la procédure pour [configurer un train de données](configure.md) avec le service [Adobe Experience Platform](configure.md#aep).

Une fois que vous avez créé la structure de données, modifiez le service [Adobe Experience Platform](configure.md#aep) que vous avez ajouté et sélectionnez l’option **[!UICONTROL Ajouter un jeu de données d’événement]** pour ajouter un ou plusieurs jeux de données d’événement de remplacement, comme illustré dans l’image ci-dessous.

![Copie d’écran de l’interface utilisateur des trains de données présentant les paramètres du service Adobe Experience Platform, avec les remplacements de jeux de données d’événement mis en surbrillance.](assets/overrides/override-aep.png)

Une fois que vous avez ajouté les remplacements souhaités, enregistrez les paramètres du train de données.

Vous avez terminé la configuration des remplacements de trains de données Adobe Experience Platform. Désormais, vous pouvez [envoyer les remplacements à l’Edge Network via le SDK Web ou le SDK Mobile](#send-overrides).

### Remplacements de trains de données pour les conteneurs de synchronisation d’identifiants tiers {#container-overrides}

Avant de configurer les remplacements de trains de données pour les conteneurs de synchronisation d’identifiants tiers, vous devez créer un train de données. Pour ce faire, consultez la section [Configurer un train de données](configure.md).

Une fois que vous avez créé le train de données, accédez aux **[!UICONTROL Options avancées]** et activez l’option **[!UICONTROL Synchronisation des identifiants tiers]**.

Consultez ensuite la section **[!UICONTROL Remplacements d’ID de conteneur]** pour ajouter les ID de conteneur que vous souhaitez remplacer par le paramètre par défaut, comme illustré dans l’image ci-dessous.

>[!IMPORTANT]
>
>Les identifiants de conteneur doivent contenir des valeurs numériques, comme `1234567`, et non des chaînes, telles que `"1234567"`. Si vous envoyez une valeur de chaîne via le SDK Web en tant que remplacement d’identifiant de conteneur, vous recevrez une erreur.

![Copie d’écran de l’interface utilisateur des trains de données montrant les paramètres des trains de données, avec les remplacements des conteneurs de synchronisation d’identifiants tiers mis en surbrillance.](assets/overrides/override-container.png)

Une fois que vous avez ajouté les remplacements souhaités, enregistrez les paramètres du train de données.

Vous avez terminé la configuration des remplacements de conteneurs de synchronisation d’identifiants. Désormais, vous pouvez [envoyer les remplacements à l’Edge Network via le SDK Web ou le SDK Mobile](#send-overrides).

## Envoyer les remplacements à l’Edge Network {#send-overrides}

Après avoir configuré les remplacements de flux de données dans l’interface utilisateur de collecte de données, vous pouvez envoyer les remplacements à l’Edge Network par le biais du SDK Web ou du SDK mobile.

* **SDK Web** : Voir [ remplacements de configuration de la banque de données](../web-sdk/commands/datastream-overrides.md#library) pour obtenir des instructions d’extension de balise et des exemples de code de bibliothèque JavaScript.
* **SDK Mobile** : vous pouvez envoyer des remplacements d’ID de flux de données à l’aide de l’ [API sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) ou à l’aide de [règles](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

## Exemple de payload {#payload-example}

Les exemples ci-dessus génèrent une charge utile [!DNL Edge Network] similaire à celle ci-dessous.

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
          }
        }
      },
      "com_adobe_analytics": {
        "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
      },
      "com_adobe_identity": {
        "idSyncContainerId": "1234567"
      },
      "com_adobe_target": {
        "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
      }
    },
    "state": {  }
  },
  "events": [  ]
}
```

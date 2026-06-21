---
title: Configurer les remplacements de trains de données
description: Découvrez comment configurer les remplacements de trains de données dans l’interface utilisateur des trains de données et les activer via le Web SDK ou le Mobile SDK.
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
TQID: https://experienceleague.adobe.com/aJ2LwoPg77e9GJ-uGHyMnAHVzHeax9tkZxjY7Vc6CAY
product_v2:
  - id: cb954087-f4fc-4456-afb9-e939cabcdc79
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
  - id: df80eeb1-8d72-467e-b0df-9d51c7d3a0a1
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
  - id: f002a92a-b99f-47a4-90c8-65e0e415bc7a
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: b82b475d-1e7d-46c6-9172-1f9c73004b11
  - id: baaa0dd2-d27e-4921-aae3-7888623a5fa5
  - id: bef6f891-2e8a-425e-8f99-7ddf22070daa
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: d556b755-390a-43f0-be32-a08cf6236126
  - id: d833d0ef-8ed5-4cff-a5e7-9f12abd02a31
  - id: df64005d-8f9a-422e-ba4d-c6f6dc3454b4
  - id: e08599ea-8888-4294-ba74-3ba0a7762a46
  - id: eb9732ab-8232-4b21-bc4c-89de86dbe4d7
  - id: ed0d8d0e-04b9-4326-be72-a0fbca265377
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
  - id: fe96aceb-8194-4a8a-a6b0-75302d02804d
subfeature_v2:
  - id: aff8c1fa-1be7-48bd-92b8-4b12a668ca13
  - id: b64298cc-90cc-46b7-8917-ee391f1c7516
  - id: ca3d6bf4-a4af-4944-936b-8de1eb09f149
  - id: d2e8a157-b3b0-4143-9ff3-809bf400be56
  - id: d9830f6f-ceb6-4faa-9744-f281fe4439f9
  - id: de9975b2-c43a-4287-9698-4f4cad92b83f
  - id: e5329d1b-e590-4e24-a3fb-ef3fe0f2c721
  - id: e8a4c7eb-7254-4984-ac46-e651a57c7e39
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 979
ht-degree: 37%

---

# Configurer les remplacements de trains de données

Utilisez les remplacements de train de données pour définir des configurations supplémentaires pour vos trains de données, qui sont transmises au [!DNL Edge Network] via le Web SDK ou le Mobile SDK.

Déclenchez différents comportements de flux de données sans créer de flux de données ni modifier vos paramètres existants.

Le remplacement de la configuration des trains de données est un processus en deux étapes :

1. Tout d’abord, vous devez définir le remplacement de votre configuration de train de données sur la page [configuration du train de données](/help/datastreams/configure.md).
2. Ensuite, vous devez envoyer les remplacements au [!DNL Edge Network] de l’une des manières suivantes :
   * Via les commandes `sendEvent` ou `configure` [Web SDK](#send-overrides).
   * Via le SDK Web [extension de balise](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md).
   * Via l’API Mobile SDK [sendEvent](#send-overrides) ou à l’aide de [Rules](#send-overrides).

Cet article décrit le processus de remplacement de configuration des trains de données de bout en bout pour chaque type de remplacement pris en charge.

>[!IMPORTANT]
>
>Les intégrations d’API [!DNL Edge Network] ne prennent actuellement pas en charge les remplacements de trains de données.
>
>Utilisez les remplacements de trains de données pour envoyer différentes données à différents trains de données. N’utilisez pas de remplacements de flux de données pour les cas d’utilisation de personnalisation ou les données de consentement.

## Cas d’utilisation {#use-cases}

Les cas d’utilisation suivants montrent comment et quand utiliser les remplacements de train de données.

### Collecte de données multi-région {#multi-region}

Une entreprise possède des sites web ou des sous-domaines distincts pour chaque pays dans lequel elle opère. Ils ont [configuré](/help/datastreams/configure.md) des flux de données distincts avec les suites de rapports spécifiques aux analyses correspondantes, les jetons de propriété de [!DNL Adobe Target] spécifiques au pays, les schémas spécifiques au pays, les jeux de données, les configurations de [!DNL Journey Optimizer], etc. L’entreprise dispose également d’un jeu global de configurations où toutes les données spécifiques à un pays sont agrégées.

Grâce aux remplacements de trains de données, l’entreprise peut acheminer dynamiquement le flux de données vers différents trains de données, au lieu du comportement par défaut consistant à envoyer des données à un train de données unique.

Un cas d’utilisation courant consiste à envoyer des données à un flux de données spécifique à un pays ainsi qu’à un flux de données global lorsque les clients effectuent une action importante, telle que passer une commande ou mettre à jour leur profil utilisateur.

### Différenciation des profils et des identités pour différentes unités opérationnelles {#multiple-business-units}

Une entreprise avec plusieurs unités opérationnelles souhaite utiliser plusieurs sandbox Experience Platform pour stocker des données spécifiques à chaque unité opérationnelle.

Au lieu d’envoyer les données à un train de données par défaut, l’entreprise peut utiliser les remplacements de trains de données pour s’assurer que chaque unité commerciale dispose de son propre train de données pour recevoir les données.

## Configurer les remplacements de trains de données dans l’interface utilisateur des trains de données {#configure-overrides}

Les remplacements de configuration de train de données vous permettent de modifier les configurations de train de données suivantes :

* Jeux de données d’événement Experience Platform
* Jetons de propriété [!DNL Adobe Target]
* Conteneurs de synchronisation d’identifiants Audience Manager
* [!DNL Adobe Analytics] des suites de rapports

### Remplacements de trains de données pour Adobe Target {#target-overrides}

Pour configurer les remplacements de train de données pour un train de données [!DNL Adobe Target], vous devez d’abord créer un train de données [!DNL Adobe Target]. Suivez la procédure pour [configurer un train de données](/help/datastreams/configure.md) avec le service [Adobe Target](/help/datastreams/configure.md#target).

Après avoir créé le flux de données, modifiez le service [&#128279;](/help/datastreams/configure.md#target) que vous avez ajouté et utilisez la section **[!UICONTROL Remplacements de jeton de propriété]** pour ajouter les remplacements de flux de données souhaités. Ajoutez un jeton de propriété par ligne.

![Copie d’écran de l’interface utilisateur des trains de données montrant les paramètres du service Adobe Target, avec les remplacements de jetons de propriété mis en surbrillance.](assets/overrides/override-target.png)

Après avoir ajouté les remplacements souhaités, enregistrez les paramètres de votre flux de données.

Les remplacements de train de données [!DNL Adobe Target] sont maintenant configurés. Vous pouvez désormais [envoyer les remplacements au [!DNL Edge Network] via le SDK web ou le SDK mobile](#send-overrides).

### Remplacements de trains de données pour Adobe Analytics {#analytics-overrides}

Pour configurer les remplacements de train de données pour un train de données [!DNL Adobe Analytics], vous devez d’abord créer un train de données [Adobe Analytics](/help/datastreams/configure.md#analytics). Suivez la procédure pour [configurer un train de données](/help/datastreams/configure.md) avec le service [Adobe Analytics](/help/datastreams/configure.md#analytics).

Après avoir créé le flux de données, modifiez le service [&#128279;](/help/datastreams/configure.md#analytics) que vous avez ajouté et utilisez la section **[!UICONTROL Remplacements de suites de rapports]** pour ajouter les remplacements de flux de données souhaités.

Sélectionnez **[!UICONTROL Afficher le mode batch]** pour activer la modification par lots des remplacements de suites de rapports. Vous pouvez copier et coller une liste de remplacements de suites de rapports. Saisissez une suite de rapports par ligne.

![Copie d’écran de l’interface utilisateur des trains de données montrant les paramètres du service Adobe Analytics, avec les remplacements de suites de rapports mis en surbrillance.](assets/overrides/override-analytics.png)

Après avoir ajouté les remplacements souhaités, enregistrez les paramètres de votre flux de données.

Les remplacements de train de données [!DNL Adobe Analytics] sont maintenant configurés. Vous pouvez désormais [envoyer les remplacements au [!DNL Edge Network] via le SDK web ou le SDK mobile](#send-overrides).

### Remplacements de trains de données pour les jeux de données d’événements Experience Platform {#event-dataset-overrides}

Pour configurer les remplacements de trains de données pour les jeux de données d’événements Experience Platform, vous devez d’abord créer un train de données [Adobe Experience Platform](/help/datastreams/configure.md#aep). Suivez la procédure pour [configurer un train de données](/help/datastreams/configure.md) avec le service [Adobe Experience Platform](/help/datastreams/configure.md#aep).

Après avoir créé le flux de données, modifiez le service [&#128279;](/help/datastreams/configure.md#aep) que vous avez ajouté et sélectionnez l’option **[!UICONTROL Ajouter un jeu de données d’événement]** pour ajouter un ou plusieurs jeux de données d’événement de remplacement.

![Copie d’écran de l’interface utilisateur des trains de données présentant les paramètres du service Adobe Experience Platform, avec les remplacements de jeux de données d’événement mis en surbrillance.](assets/overrides/override-aep.png)

Après avoir ajouté les remplacements souhaités, enregistrez les paramètres de votre flux de données.

Les remplacements de train de données [!DNL Adobe Experience Platform] sont maintenant configurés. Vous pouvez désormais [envoyer les remplacements au [!DNL Edge Network] via le SDK web ou le SDK mobile](#send-overrides).

### Remplacements de trains de données pour les conteneurs de synchronisation d’identifiants tiers {#container-overrides}

Avant de configurer les remplacements de trains de données pour les conteneurs de synchronisation d’identifiants tiers, vous devez créer un train de données. Pour ce faire, consultez la section [Configurer un train de données](/help/datastreams/configure.md).

Après avoir créé le flux de données, accédez à **[!UICONTROL Options avancées]** et activez l’option **[!UICONTROL Synchronisation des identifiants tiers]**.

Utilisez ensuite la section **[!UICONTROL Remplacements d’ID de conteneur]** pour ajouter les ID de conteneur à remplacer par le paramètre par défaut.

>[!IMPORTANT]
>
>Les identifiants de conteneur doivent contenir des valeurs numériques, comme `1234567`, et non des chaînes, telles que `"1234567"`. Si vous envoyez une valeur de chaîne via le SDK Web en tant que remplacement d’identifiant de conteneur, vous recevrez une erreur.

![Copie d’écran de l’interface utilisateur des trains de données montrant les paramètres des trains de données, avec les remplacements des conteneurs de synchronisation d’identifiants tiers mis en surbrillance.](assets/overrides/override-container.png)

Après avoir ajouté les remplacements souhaités, enregistrez les paramètres de votre flux de données.

Les remplacements du conteneur de synchronisation des identifiants sont maintenant configurés. Vous pouvez désormais [envoyer les remplacements au [!DNL Edge Network] via le SDK web ou le SDK mobile](#send-overrides).

## Envoyer les remplacements à Edge Network {#send-overrides}

Après avoir configuré les remplacements de train de données dans l’interface utilisateur de collecte de données, vous pouvez envoyer les remplacements au [!DNL Edge Network] via le Web SDK ou Mobile SDK.

* **Web SDK** : voir [remplacements de configuration des trains de données](/help/collection/js/commands/configure/edgeconfigoverrides.md) pour obtenir des exemples de code de bibliothèque JavaScript.
* **Mobile SDK** : vous pouvez envoyer des remplacements d’ID de train de données à l’aide de l’API [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) ou à l’aide de [Rules](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

## Exemple de payload {#payload-example}

Les exemples précédents génèrent une payload [!DNL Edge Network] similaire à celle ci-dessous.

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

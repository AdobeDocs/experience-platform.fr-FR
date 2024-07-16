---
title: Remplacements de la configuration des flux de données
description: Découvrez comment configurer les remplacements de flux de données via le SDK Web.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---

# Configurer les remplacements de trains de données

L’objet `edgeConfigOverrides` vous permet de remplacer les paramètres de configuration des commandes exécutées sur la page active. Cet objet de remplacement n’est pas une commande, mais plutôt un objet que vous pouvez inclure dans la plupart des commandes du SDK Web.

Cet objet est utile lorsque vous disposez de différents sites web ou sous-domaines pour différents pays ou si vous disposez de plusieurs environnements de test Experience Platform pour stocker des données spécifiques à différentes unités opérationnelles.

>[!IMPORTANT]
>
>Pour obtenir des instructions de configuration de bout en bout détaillées sur les remplacements de flux de données, consultez la documentation [Remplacements de configuration de flux de données](../../datastreams/overrides.md#configure-overrides) .

Le remplacement de la configuration du flux de données est un processus en deux étapes :

1. Tout d’abord, vous devez définir le remplacement de la configuration de la banque de données dans la [page de configuration de la banque de données](../../datastreams/configure.md), dans l’interface utilisateur des flux de données. Pour obtenir des instructions sur la configuration des remplacements, reportez-vous à la documentation [Remplacements de configuration de la banque de données](../../datastreams/overrides.md#configure-overrides) .
2. Après avoir configuré le remplacement de la banque de données dans l’interface utilisateur, vous devez envoyer les remplacements à l’Edge Network de l’une des manières suivantes :
   * Par le biais du SDK Web [extension de balise](#tag-extension).
   * Par le biais des commandes du SDK Web `sendEvent` ou `configure`.
   * Par le biais de la commande SDK Mobile `sendEvent` .

Si vous définissez des remplacements dans la configuration du SDK Web et dans une commande spécifique (telle que [`sendEvent`](sendevent/overview.md)), ceux de la commande spécifique sont prioritaires.

## Propriétés de l’objet

Les propriétés suivantes sont disponibles dans cet objet :

* **Remplacement de la banque de données** : envoyez des appels à une autre banque de données. Si vous définissez cette valeur, d’autres remplacements qui nécessitent la configuration du flux de données doivent être configurés dans le flux de données défini ici.
* **Conteneur de synchronisation des identifiants tiers** : identifiant du conteneur de synchronisation des identifiants tiers de destination dans Adobe Audience Manager. La configuration d’un remplacement de conteneur d’ID tiers dans les paramètres de la banque de données est requise avant d’utiliser ce champ.
* **Jeton de propriété Target** : jeton de la propriété de destination dans Adobe Target. Avant d’utiliser ce champ, vous devez configurer un remplacement de jeton de propriété Target dans les paramètres de la banque de données.
* **Suites de rapports** : identifiants de suite de rapports à remplacer dans Adobe Analytics. Avant d’utiliser ce champ, vous devez configurer les remplacements de suite de rapports dans les paramètres de la banque de données.

## Envoi des remplacements de la banque de données à l’Edge Network par le biais de l’extension de balise SDK Web {#tag-extension}

Pour obtenir des instructions de configuration détaillées, reportez-vous à la documentation sur la [configuration des remplacements de jeux de données](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) à partir de l’extension de balise SDK Web.

Si vous souhaitez configurer les remplacements de la banque de données à partir de l’extension de balise SDK Web, définissez chaque champ de votre choix sous **[!UICONTROL Remplacements de configuration de la banque de données]** lors de la [configuration de l’extension de balise](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Extensions]**, puis cliquez sur **[!UICONTROL Configurer]** sur la carte [!UICONTROL SDK Web Adobe Experience Platform].
1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Remplacements de configuration du flux de données]** . Définissez chaque valeur de remplacement souhaitée.
1. Cliquez sur **[!UICONTROL Enregistrer]**, puis publiez vos modifications.

Si vous souhaitez définir des remplacements uniquement pour une commande spécifique, définissez chaque champ de votre choix dans les actions d’une règle de balise.

1. Connectez-vous à [experience.adobe.com](https://experience.adobe.com) à l’aide de vos informations d’identification Adobe ID.
1. Accédez à **[!UICONTROL Collecte de données]** > **[!UICONTROL Balises]**.
1. Sélectionnez la propriété de balise de votre choix.
1. Accédez à **[!UICONTROL Rules]**, puis sélectionnez la règle de votre choix.
1. Sous [!UICONTROL Actions], sélectionnez une action existante ou créez une action.
1. Définissez le champ déroulant [!UICONTROL Extension] sur **[!UICONTROL SDK Web Adobe Experience Platform]** et définissez le [!UICONTROL Type d’action] sur **[!UICONTROL Envoyer l’événement]**.
1. Faites défiler l’écran jusqu’à la section intitulée **[!UICONTROL Remplacements de configuration du flux de données]**.
1. Définissez chaque champ de cette section sur la valeur de remplacement souhaitée.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**, puis exécutez votre processus de publication.

Des champs distincts sont fournis pour les environnements [!UICONTROL Development], [!UICONTROL Staging] et [!UICONTROL Production]. Veillez à renseigner chaque champ souhaité pour chaque environnement.

## Envoyer les remplacements à l’Edge Network via la bibliothèque JavaScript SDK Web {#library}

Après avoir [configuré les remplacements de la banque de données](../../datastreams/overrides.md) dans l’interface utilisateur de collecte de données, vous pouvez désormais envoyer les remplacements à l’Edge Network, via la bibliothèque JavaScript du SDK Web.

Si vous utilisez le SDK Web, l’envoi des remplacements à l’Edge Network via la commande `edgeConfigOverrides` constitue la deuxième et dernière étape de l’activation des remplacements de configuration de la banque de données.

Les remplacements de configuration de trains de données sont envoyés au réseau Edge par l’intermédiaire de la commande `edgeConfigOverrides` du SDK Web. Cette commande crée des remplacements de flux de données qui sont transmis à [!DNL Edge Network] sur la commande suivante. Si vous utilisez la commande `configure`, les remplacements sont transmis pour chaque requête.

La commande `edgeConfigOverrides` crée des remplacements de la banque de données qui sont transmis à [!DNL Edge Network] sur la commande suivante.

Lorsqu’un remplacement de configuration est envoyé avec la commande `configure`, elle est incluse dans les commandes suivantes du SDK Web.

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

Les options spécifiées globalement peuvent être remplacées par l’option de configuration des commandes individuelles.

### Envoi des remplacements de configuration via la commande SDK Web `sendEvent` {#send-event}

L’exemple ci-dessous illustre le remplacement d’une configuration à l’aide de la commande `sendEvent`.

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| Paramètre | Description |
|---|---|
| `edgeConfigOverrides.datastreamId` | Ce paramètre permet à une requête unique d’accéder à un train de données différent de celui défini par la commande `configure`. |
| `com_adobe_analytics.reportSuites[]` | Tableau de chaînes qui détermine à quelles suites de rapports doivent envoyer des données Analytics. |
| `com_adobe_identity.idSyncContainerId` | Conteneur de synchronisation des identifiants tiers que vous souhaitez utiliser dans Audience Manager. |
| `com_adobe_target.propertyToken` | Jeton pour la propriété de destination Adobe Target. |

### Envoi des remplacements de configuration via la commande SDK Web `configure` {#send-configure}

L’exemple ci-dessous illustre le remplacement d’une configuration à l’aide de la commande `configure`.

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
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
  onBeforeEventSend: function() { /* … */ });
};
```

| Paramètre | Description |
|---|---|
| `edgeConfigOverrides.datastreamId` | Ce paramètre permet à une requête unique d’accéder à un train de données différent de celui défini par la commande `configure`. |
| `com_adobe_analytics.reportSuites[]` | Tableau de chaînes qui détermine à quelles suites de rapports doivent envoyer des données Analytics. |
| `com_adobe_identity.idSyncContainerId` | Conteneur de synchronisation des identifiants tiers que vous souhaitez utiliser dans Audience Manager. |
| `com_adobe_target.propertyToken` | Jeton pour la propriété de destination Adobe Target. |

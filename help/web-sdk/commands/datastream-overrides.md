---
title: Remplacements de la configuration des flux de données
description: Découvrez comment configurer les remplacements de flux de données via le SDK Web.
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 10%

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
   * Par le biais des commandes du SDK Web [`sendEvent`](../commands/sendevent/overview.md) ou [`configure`](../commands/configure/overview.md).
   * Par le biais de la commande SDK Mobile [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network) .

Si vous définissez des remplacements dans la configuration du SDK Web et dans une commande spécifique (telle que [`sendEvent`](sendevent/overview.md)), ceux de la commande spécifique sont prioritaires.

>[!NOTE]
>
>Si vous souhaitez qu’un remplacement de configuration *désactiver* un service Experience Cloud, vous devez vous assurer que le service est *activé* dans la configuration du flux de données. Pour plus d’informations sur l’ajout de services à un flux de données, consultez la documentation sur la [configuration des flux de données](../../datastreams/configure.md#add-services) .

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

L’exemple ci-dessous montre toutes les options de configuration de la chaîne de données dynamique prises en charge lors d’un appel `sendEvent`.

Si tous les services pris en charge sont activés pour votre configuration de flux de données, l’exemple ci-dessous remplace ce paramètre et désactive tous les services (voir le paramètre `enabled: false` sur chaque service).

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["ujslconfigoverrides3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

| Paramètre | Description |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | Ce paramètre permet à une requête unique d’accéder à un train de données différent de celui défini par la commande `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Définit la configuration de flux de données dynamique pour le service Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Définit si l’événement sera envoyé au service Experience Platform ou non. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Définit les jeux de données utilisés pour l’événement. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Définit si l’événement est envoyé au service Offer Decisioning ou non. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Définit si l’événement est envoyé ou non au service de segmentation Edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Définit si les données d’événement sont envoyées ou non aux destinations périphériques. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Définit si les données d’événement sont envoyées ou non au service Adobe Journey Optimizer. |
| `com_adobe_analytics.enabled` | Définit si les données d’événement sont envoyées à Adobe Analytics ou non. |
| `com_adobe_analytics.reportSuites[]` | Tableau de chaînes qui détermine à quelles suites de rapports vous souhaitez envoyer des données Analytics. |
| `com_adobe_identity.idSyncContainerId` | Conteneur de synchronisation des identifiants tiers que vous souhaitez utiliser dans Audience Manager. Pour que ce conteneur de synchronisation des identifiants fonctionne, vous devez définir `com_adobe_audience_manager.enabled` sur `true`. Sinon, le service d’Audience Manager est désactivé. |
| `com_adobe_target.enabled` | Définit si les données d’événement sont envoyées à Adobe Target. |
| `com_adobe_target.propertyToken` | Jeton pour la propriété de destination Adobe Target. |
| `com_adobe_audience_manager.enabled` | Définit si les données d’événement sont envoyées au service Audience Manager. |
| `com_adobe_launch_ssf` | Définit si les données d’événement sont envoyées au transfert côté serveur. |

### Envoi des remplacements de configuration via la commande SDK Web `configure` {#send-configure}

L’exemple ci-dessous illustre le remplacement d’une configuration à l’aide de la commande `configure`.

Si tous les services pris en charge sont activés pour votre configuration de flux de données, l’exemple ci-dessous remplace ce paramètre et désactive tous les services (voir le paramètre `enabled: false` sur chaque service).

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

| Paramètre | Description |
|---|---|
| `orgId` | L’identifiant de l’organisation IMS correspondant à votre compte d’Adobe. |
| `edgeConfigOverrides.datastreamId` | Ce paramètre permet à une requête unique d’accéder à un train de données différent de celui défini par la commande `configure`. |
| `edgeConfigOverrides.com_adobe_experience_platform` | Définit la configuration de flux de données dynamique pour le service Experience Platform. |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | Définit si l’événement sera envoyé au service Experience Platform ou non. |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | Définit les jeux de données utilisés pour l’événement. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | Définit si l’événement est envoyé au service Offer Decisioning ou non. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | Définit si l’événement est envoyé ou non au service de segmentation Edge. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | Définit si les données d’événement sont envoyées ou non aux destinations périphériques. |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | Définit si les données d’événement sont envoyées ou non au service Adobe Journey Optimizer. |
| `com_adobe_analytics.enabled` | Définit si les données d’événement sont envoyées à Adobe Analytics ou non. |
| `com_adobe_analytics.reportSuites[]` | Tableau de chaînes qui détermine à quelles suites de rapports vous souhaitez envoyer des données Analytics. |
| `com_adobe_identity.idSyncContainerId` | Conteneur de synchronisation des identifiants tiers que vous souhaitez utiliser dans Audience Manager. Pour que ce conteneur de synchronisation des identifiants fonctionne, vous devez définir `com_adobe_audience_manager.enabled` sur `true`. Sinon, le service d’Audience Manager est désactivé. |
| `com_adobe_target.enabled` | Définit si les données d’événement sont envoyées à Adobe Target. |
| `com_adobe_target.propertyToken` | Jeton pour la propriété de destination Adobe Target. |
| `com_adobe_audience_manager.enabled` | Définit si les données d’événement sont envoyées au service Audience Manager. |
| `com_adobe_launch_ssf` | Définit si les données d’événement sont envoyées au transfert côté serveur. |


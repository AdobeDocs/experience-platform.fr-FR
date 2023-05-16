---
description: Découvrez comment configurer les paramètres de métadonnées d’audience pour les destinations créées avec Destination SDK.
title: Configuration des métadonnées d’audience
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 6%

---


# Configuration des métadonnées d’audience

Lors de l’exportation de données d’Experience Platform vers votre destination, vous aurez peut-être besoin de métadonnées d’audience spécifiques, telles que les noms de segment ou les identifiants de segment, pour être partagées entre l’Experience Platform et votre destination.

Destination SDK propose des outils que vous pouvez utiliser pour créer, mettre à jour ou supprimer des audiences par programmation dans votre plateforme de destination.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer les opérations [utiliser la Destination SDK pour configurer une destination de diffusion en continu ;](../../guides/configure-destination-instructions.md#create-destination-configuration).

Vous pouvez configurer le modèle de métadonnées d’audience via le `/authoring/audience-templates` point de terminaison . Après avoir créé votre configuration de métadonnées d’audience, vous pouvez utiliser la variable `/authoring/destinations` point d’entrée pour configurer la variable `audienceMetadataConfig` . Cette section indique à votre destination les métadonnées de segment qu’elle doit mapper à votre modèle d’audience.

Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Créer un modèle d’audience](../../metadata-api/create-audience-template.md)
* [Mettre à jour un modèle d’audience](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |

## Paramètres pris en charge {#supported-parameters}

Lors de la création de la configuration des métadonnées d’audience, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour configurer les paramètres de mappage des segments.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booléen | Indique si la variable [[!UICONTROL ID de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination doit correspondre au nom du segment Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booléen | Indique si la variable [[!UICONTROL ID de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination, la valeur doit correspondre à l’identifiant du segment Experience Platform. |
| `mapUserInput` | Booléen | Active ou désactive la saisie utilisateur pour la variable [[!UICONTROL ID de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination. Si la variable est définie sur `true`, `audienceTemplateId` ne peut pas être présent. |
| `audienceTemplateId` | Booléen | Le `instanceId` de [modèle de métadonnées d’audience](../../metadata-api/create-audience-template.md) utilisé pour votre destination. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer les métadonnées d’audience pour votre destination.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Configuration de l’authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)
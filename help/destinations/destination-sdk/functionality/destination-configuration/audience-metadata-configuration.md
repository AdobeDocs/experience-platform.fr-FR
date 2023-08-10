---
description: Découvrez comment configurer les paramètres de métadonnées d’audience pour les destinations créées avec Destination SDK.
title: Configuration des métadonnées d’audience
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 65%

---


# Configuration des métadonnées d’audience

Lors de l’exportation de données d’Experience Platform vers votre destination, vous aurez peut-être besoin de métadonnées d’audience spécifiques, telles que les noms d’audience ou les ID d’audience, à partager entre l’Experience Platform et votre destination.

Destination SDK propose des outils que vous pouvez utiliser pour créer, mettre à jour ou supprimer des audiences par programmation dans la plateforme de destination.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer [utiliser la Destination SDK pour configurer une destination de diffusion en continu ;](../../guides/configure-destination-instructions.md#create-destination-configuration).

Vous pouvez configurer le modèle de métadonnées d’audience via le point d’entrée `/authoring/audience-templates`. Après avoir créé la configuration de métadonnées d’audience, vous pouvez utiliser le point d’entrée `/authoring/destinations` pour configurer la section `audienceMetadataConfig`. Cette section indique à votre destination les métadonnées d’audience qu’elle doit mapper à votre modèle d’audience.

Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Création d’un modèle d’audience](../../metadata-api/create-audience-template.md)
* [Mise à jour d’un modèle d’audience](../../metadata-api/update-audience-template.md)

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

Lors de la création de la configuration des métadonnées d’audience, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour configurer les paramètres de mappage d’audience.

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
| `mapExperiencePlatformSegmentName` | Booléen | Indique si la variable [[!UICONTROL ID de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination, la valeur doit correspondre au nom de l’audience Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booléen | Indique si la variable [[!UICONTROL ID de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination, la valeur doit correspondre à l’ID d’audience Experience Platform. |
| `mapUserInput` | Booléen | Active ou désactive l’entrée utilisateur pour la valeur de l’[[!UICONTROL identifiant de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination. S’il est défini sur `true`, `audienceTemplateId` ne peut pas être présent. |
| `audienceTemplateId` | Booléen | `instanceId` du [modèle de métadonnées d’audience](../../metadata-api/create-audience-template.md) utilisé pour votre destination. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment configurer les métadonnées d’audience pour la destination.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Configuration de l’authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)
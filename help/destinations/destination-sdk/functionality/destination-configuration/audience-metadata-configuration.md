---
description: Découvrez comment configurer les paramètres de métadonnées d’audience pour les destinations créées avec Destination SDK.
title: Configuration des métadonnées d’audience
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 20cb2dbfbfc8e73c765073818c8e7e561d4e6629
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 90%

---

# Configuration des métadonnées d’audience

Pendant l’exportation de données d’Experience Platform vers votre destination, vous aurez peut-être besoin de métadonnées d’audience spécifiques, telles que les noms ou les identifiants d’audience, à partager entre Experience Platform et votre destination.

Destination SDK propose des outils que vous pouvez utiliser pour créer, mettre à jour ou supprimer des audiences par programmation dans la plateforme de destination.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la documentation [options de configuration](../configuration-options.md) ou consultez le guide sur la [ utilisation de la Destination SDK pour configurer une destination de diffusion en continu](../../guides/configure-destination-instructions.md#create-destination-configuration).

Vous pouvez configurer le modèle de métadonnées d’audience via le point d’entrée `/authoring/audience-templates`. Après avoir créé la configuration de métadonnées d’audience, vous pouvez utiliser le point d’entrée `/authoring/destinations` pour configurer la section `audienceMetadataConfig`. Cette section indique à votre destination les métadonnées d’audience qu’elle doit mapper sur le modèle d’audience.

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

Pendant la création de la configuration des métadonnées d’audience, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour configurer les paramètres de mappage des audiences.

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
| `mapExperiencePlatformSegmentName` | Booléen | Indique si la valeur de l’[[!UICONTROL identifiant de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination doit correspondre au nom de l’audience Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booléen | Indique si la valeur de l’[[!UICONTROL identifiant de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination doit correspondre à l’identifiant de l’audience Experience Platform. |
| `mapUserInput` | Booléen | Active ou désactive l’entrée utilisateur pour la valeur de l’[[!UICONTROL identifiant de mappage]](../../../ui/activate-segment-streaming-destinations.md#scheduling) dans le workflow d’activation de destination. S’il est défini sur `true`, `audienceTemplateId` ne peut pas être présent. |
| `audienceTemplateId` | Chaîne | `instanceId` du [modèle de métadonnées d’audience](../../metadata-api/create-audience-template.md) utilisé pour votre destination. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment configurer les métadonnées d’audience pour la destination.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Configuration de l’authentification du client](customer-authentication.md)
* [Autorisation OAuth2](oauth2-authorization.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)

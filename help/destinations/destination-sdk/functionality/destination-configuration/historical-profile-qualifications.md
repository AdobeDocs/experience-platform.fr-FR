---
description: Découvrez les qualifications de profil historiques prises en charge par les destinations créées avec Destination SDK.
title: Qualifications des profils historiques
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 10%

---


# Qualifications des profils historiques

Toutes les destinations créées via Destination SDK prennent en charge les qualifications de profil historiques par défaut. Cela signifie que lorsque les utilisateurs configurent pour la première fois un flux de données d’activation vers vos destinations, la première exportation contient tous les membres du segment qui se sont jamais qualifiés pour ce segment.

Ce comportement est défini par la variable `"backfillHistoricalProfileData":true` dans la configuration de destination.

>[!IMPORTANT]
>
>Les qualifications de profil historique sont activées pour toutes les destinations créées via Destination SDK et la variable `backfillHistoricalProfileData` n’est pas configurable par l’utilisateur.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devez savoir que Experience Platform exporte automatiquement une population historique de tous les profils qui se sont qualifiés pour un segment activé lors de l’exportation initiale du segment vers la destination. Cette option n’est pas configurable dans Destination SDK ni dans l’interface utilisateur de l’Experience Platform.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
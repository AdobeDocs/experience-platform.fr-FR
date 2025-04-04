---
description: Découvrez les qualifications des historiques prises en charge par les destinations créées avec Destination SDK.
title: Qualifications des profils historiques
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 99%

---

# Qualifications des profils historiques

Toutes les destinations créées avec Destination SDK prennent en charge les qualifications de profil historiques par défaut. Cela signifie que quand les personnes configurent pour la première fois un flux de données d’activation vers vos destinations, la première exportation contient tous les membres de l’audience qui ne se sont jamais qualifiés pour ce segment.

Ce comportement est défini par le paramètre `"backfillHistoricalProfileData":true` dans la configuration de destination.

>[!IMPORTANT]
>
>Les qualifications de profil historique sont activées pour toutes les destinations créées avec Destination SDK et le paramètre `backfillHistoricalProfileData` n’est pas configurable par l’utilisateur.

## Types d’intégration pris en charge {#supported-integration-types}

Pour en savoir plus sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page, consultez le tableau ci-dessous.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (streaming) | Oui |
| Intégrations basées sur des fichiers (par lots) | Oui |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Experience Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Experience Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## Étapes suivantes {#next-steps}

Vous avez lu l’intégralité de cet article. À présent, vous devez savoir qu’Experience Platform exporte automatiquement un historique de tous les profils qui se sont qualifiés pour une audience activée quand l’audience est exportée pour la première fois vers la destination. Cette option n’est pas configurable dans Destination SDK ni dans l’interface utilisateur d’Experience Platform.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Autorisation OAuth2](oauth2-authorization.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)

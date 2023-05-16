---
description: Découvrez comment configurer une stratégie d’agrégation pour déterminer comment les requêtes HTTP vers votre destination doivent être groupées et regroupées par lot.
title: Politique d’agrégation
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 14%

---


# Politique d’agrégation

Pour garantir une efficacité maximale lors de l’exportation de données vers votre point de terminaison API, vous pouvez utiliser divers paramètres pour agréger les profils exportés en lots plus ou plus petits, les regrouper par identité et d’autres cas d’utilisation. Cela vous permet également d’adapter les exportations de données à toutes les limitations en aval de votre point d’entrée API (limitation de débit, nombre d’identités par appel API, etc.).

Utilisez l’agrégation configurable pour vous plonger dans les paramètres fournis par Destination SDK ou utilisez l’agrégation avec le meilleur effort pour indiquer à Destination SDK de traiter par lots les appels API du mieux qu’il peut.

Lors de la création d’une destination en temps réel (diffusion en continu) avec Destination SDK, vous pouvez configurer la manière dont les profils exportés doivent être combinés dans les exportations résultantes. Ce comportement est déterminé par les paramètres de la stratégie d’agrégation.

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer les opérations [utiliser la Destination SDK pour configurer une destination de diffusion en continu ;](../../guides/configure-destination-instructions.md#create-destination-configuration).

Vous pouvez configurer les paramètres de la stratégie d’agrégation via le `/authoring/destinations` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit tous les paramètres de stratégie d’agrégation pris en charge que vous pouvez utiliser pour votre destination.

Après avoir lu ce document, reportez-vous à la documentation sur [utilisation de modèles](../../functionality/destination-server/message-format.md#using-templating) et le [exemples clés d’agrégation](../../functionality/destination-server/message-format.md#template-aggregation-key) pour comprendre comment inclure la stratégie d’agrégation dans votre modèle de transformation des messages en fonction de votre stratégie d’agrégation sélectionnée.

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Non |

## Agrégation des meilleurs efforts {#best-effort-aggregation}

L’agrégation des meilleurs efforts fonctionne mieux pour les destinations qui préfèrent moins de profils par requête et qui préfèrent recevoir plus de requêtes avec moins de données que de requêtes avec plus de données.

L’exemple de configuration ci-dessous illustre une configuration d’agrégation des meilleurs efforts. Pour un exemple d’agrégation configurable, voir la section [agrégation configurable](#configurable-aggregation) . Les paramètres applicables à l&#39;agrégation des meilleurs efforts sont présentés dans le tableau ci-dessous.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `aggregationType` | Chaîne | Indique le type de stratégie d’agrégation que votre destination doit utiliser. Types d’agrégation pris en charge : <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Nombre entier | Experience Platform peut agréger plusieurs profils exportés en un seul appel HTTP. <br><br>Cette valeur indique le nombre maximal de profils que votre point de terminaison doit recevoir dans un seul appel HTTP. Notez qu’il s’agit d’une agrégation des meilleurs efforts. Par exemple, si vous spécifiez la valeur 100, Platform peut envoyer n’importe quel nombre de profils inférieur à 100 lors d’un appel. <br><br> Si votre serveur n’accepte pas plusieurs utilisateurs par demande, définissez cette valeur sur `1`. |
| `bestEffortAggregation.splitUserById` | Booléen | Utilisez cet indicateur si l’appel à la destination doit être partagé par identité. Définissez cet indicateur sur `true` si votre serveur n’accepte qu’une seule identité par appel, pour un espace de noms d’identité donné. |

{style="table-layout:auto"}

>[!TIP]
>
>Utilisez l’agrégation du meilleur effort si votre point de terminaison d’API accepte moins de 100 profils par appel d’API.

## Agrégation configurable {#configurable-aggregation}

L’agrégation configurable fonctionne mieux si vous préférez prendre des lots volumineux, avec des milliers de profils sur le même appel. Cette option permet également d’agréger les profils exportés en fonction de règles d’agrégation complexes.

L’exemple de configuration ci-dessous illustre une configuration d’agrégation configurable. Pour obtenir un exemple d’agrégation des meilleurs efforts, reportez-vous à la section [agrégation des meilleurs efforts](#best-effort-aggregation) . Les paramètres applicables à l&#39;agrégation configurable sont présentés dans le tableau ci-dessous.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Paramètre | Type | Description |
|---------|----------|------|
| `aggregationType` | Chaîne | Indique le type de stratégie d’agrégation que votre destination doit utiliser. Types d’agrégation pris en charge : <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Booléen | Utilisez cet indicateur si l’appel à la destination doit être partagé par identité. Définissez cet indicateur sur `true` si votre serveur n’accepte qu’une seule identité par appel, pour un espace de noms d’identité donné. |
| `configurableAggregation.maxBatchAgeInSecs` | Nombre entier | Utilisé en conjonction avec `maxNumEventsInBatch`, ce paramètre détermine la durée pendant laquelle l’Experience Platform doit attendre d’envoyer un appel API à votre point de terminaison . <ul><li>Valeur minimale (secondes) : 1 800</li><li>Valeur maximale (secondes) : 3600</li></ul> Par exemple, si vous utilisez la valeur maximale pour les deux paramètres, Experience Platform patiente 3 600 secondes OU jusqu’à ce qu’il y ait 1 000 profils qualifiés avant d’effectuer l’appel API, selon ce qui se produit en premier. |
| `configurableAggregation.maxNumEventsInBatch` | Nombre entier | Utilisé conjointement avec `maxBatchAgeInSecs`, ce paramètre détermine le nombre de profils qualifiés qui doivent être agrégés dans un appel API. <ul><li>Valeur minimale : 1000</li><li>Valeur maximale : 10 000</li></ul> Par exemple, si vous utilisez la valeur maximale pour les deux paramètres, Experience Platform patiente 3 600 secondes OU jusqu’à ce qu’il y ait 1 000 profils qualifiés avant d’effectuer l’appel API, selon ce qui se produit en premier. |
| `configurableAggregation.aggregationKey` | - | Permet d&#39;agréger les profils exportés mappés à la destination en fonction des paramètres décrits ci-dessous. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booléen | Définissez ce paramètre sur `true` si vous souhaitez regrouper les profils exportés vers votre destination par identifiant de segment. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booléen | Définissez ce paramètre et `includeSegmentId` to `true`, si vous souhaitez regrouper les profils exportés vers votre destination par identifiant de segment et état du segment. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booléen | Définissez ce paramètre sur `true` si vous souhaitez regrouper des profils exportés vers votre destination par espace de noms d’identité. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booléen | Définissez ce paramètre sur `true` si vous souhaitez que les profils exportés soient agrégés en groupes sur la base d’une seule identité (GAID, IDFA, numéros de téléphone, email, etc.). |
| `configurableAggregation.aggregationKey.groups` | Tableau | Créez des listes de groupes d’identités si vous souhaitez regrouper les profils exportés vers votre destination par groupes d’espaces de noms d’identité. Par exemple, vous pouvez combiner des profils qui contiennent les identifiants mobiles IDFA et GAID dans un appel vers votre destination et des emails dans un autre en utilisant la configuration affichée dans l’exemple ci-dessus. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer les stratégies d’agrégation pour votre destination.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Configuration de l’authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)
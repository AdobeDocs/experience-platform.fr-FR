---
description: Découvrez comment configurer une politique d’agrégation pour déterminer comment les requêtes HTTP vers la destination doivent être associées et regroupées par lot.
title: Politique d’agrégation
exl-id: 2dfa8815-2d69-4a22-8938-8ea41be8b9c5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 94%

---

# Politique d’agrégation

Pour garantir une efficacité maximale pendant l’exportation des données vers le point d’entrée de l’API, vous pouvez agréger à l’aide de divers paramètres les profils exportés en lots plus ou moins petits, les regrouper par identité et d’autres cas d’utilisation. Cela vous permet également d’adapter les exportations de données à toutes les limitations en aval du point d’entrée de l’API (limitation de débit, nombre d’identités par appel API, etc.).

Utilisez l’agrégation configurable pour vous plonger dans les paramètres de Destination SDK ou utilisez l’agrégation des meilleurs efforts pour indiquer à Destination SDK de traiter le mieux possible les appels API par lots.

Pendant la création d’une destination en temps réel (streaming) avec Destination SDK, vous pouvez configurer la manière dont les profils exportés doivent être combinés dans les exportations résultantes. Ce comportement est déterminé par les paramètres de la politique d’agrégation.

Pour comprendre la place de ce composant dans une intégration créée avec Destination SDK, consultez le diagramme de la documentation [options de configuration](../configuration-options.md) ou consultez le guide sur la [utilisation de Destination SDK pour configurer une destination de diffusion en streaming](../../guides/configure-destination-instructions.md#create-destination-configuration).

Vous pouvez configurer les paramètres de la politique d’agrégation via le point d’entrée `/authoring/destinations`. Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit tous les paramètres de politique d’agrégation pris en charge que vous pouvez utiliser pour la destination.

Vous êtes arrivé au bout de ce document. À présent, consultez la documentation relative à l’[utilisation de modèles](../../functionality/destination-server/message-format.md#using-templating) ainsi que les [exemples de clés d’agrégation](../../functionality/destination-server/message-format.md#template-aggregation-key) pour comprendre comment inclure la politique d’agrégation dans le modèle de transformation des messages en fonction de la politique d’agrégation que vous avez sélectionnée.

>[!IMPORTANT]
>
>Tous les noms et toutes les valeurs de paramètre pris en charge par Destination SDK **sont sensibles à la casse**. Pour éviter les erreurs de respect de la casse, utilisez les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Pour en savoir plus sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page, consultez le tableau ci-dessous.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (streaming) | Oui |
| Intégrations basées sur des fichiers (par lots) | Non |

## Agrégation des meilleurs efforts {#best-effort-aggregation}

L’agrégation des meilleurs efforts fonctionne mieux pour les destinations avec moins de profils par requête et qui préfèrent recevoir plus de requêtes avec moins de données.

L’exemple de configuration ci-dessous montre une configuration d’agrégation des meilleurs efforts. Pour obtenir un exemple d’agrégation configurable, consultez la section [Agrégation configurable](#configurable-aggregation). Les paramètres applicables à l’agrégation des meilleurs efforts sont présentés dans le tableau ci-dessous.

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
| `aggregationType` | Chaîne | Indique le type de politique d’agrégation que la destination doit utiliser. Types d’agrégation pris en charge : <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Nombre entier | Experience Platform peut agréger plusieurs profils exportés en un seul appel HTTP. <br><br>Cette valeur indique le nombre maximal de profils que le point d’entrée doit recevoir dans un seul appel HTTP. Notez qu’il s’agit d’une agrégation des meilleurs efforts. Par exemple, si vous spécifiez la valeur 100, Experience Platform peut envoyer n’importe quel nombre de profils inférieur à 100 lors d’un appel. <br><br> Si le serveur n’accepte pas plusieurs utilisateurs par requête, définissez cette valeur sur `1`. |
| `bestEffortAggregation.splitUserById` | Booléen | Utilisez cet indicateur si l’appel à la destination doit être partagé par identité. Définissez cet indicateur sur `true` si le serveur n’accepte qu’une seule identité par appel, pour un espace de nom d’identité donné. |

{style="table-layout:auto"}

>[!TIP]
>
>Utilisez l’agrégation des meilleurs efforts si le point d’entrée de l’API accepte moins de 100 profils par appel API.

## Agrégation configurable {#configurable-aggregation}

L’agrégation configurable fonctionne mieux si vous préférez accepter des lots volumineux, avec des milliers de profils sur le même appel. Cette option permet également d’agréger les profils exportés en fonction de règles d’agrégation complexes.

L’exemple de configuration ci-dessous montre une configuration d’agrégation configurable. Pour obtenir un exemple d’agrégation des meilleurs efforts, consultez la section [Agrégation des meilleurs efforts](#best-effort-aggregation). Les paramètres applicables à l’agrégation configurable sont présentés dans le tableau ci-dessous.

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
| `aggregationType` | Chaîne | Indique le type de politique d’agrégation que la destination doit utiliser. Types d’agrégation pris en charge : <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Booléen | Utilisez cet indicateur si l’appel à la destination doit être partagé par identité. Définissez cet indicateur sur `true` si le serveur n’accepte qu’une seule identité par appel, pour un espace de nom d’identité donné. |
| `configurableAggregation.maxBatchAgeInSecs` | Nombre entier | Associé à `maxNumEventsInBatch`, ce paramètre détermine combien de temps Experience Platform doit attendre avant d’envoyer un appel API vers le point d’entrée. <ul><li>Valeur minimale (secondes) : 1 800</li><li>Valeur maximale (secondes) : 3 600</li></ul> Par exemple, si vous utilisez la valeur maximale pour les deux paramètres, Experience Platform attend 3 600 secondes où qu’il y ait 10 000 profils qualifiés avant d’effectuer l’appel API, selon ce qui se produit en premier. |
| `configurableAggregation.maxNumEventsInBatch` | Nombre entier | Associé à `maxBatchAgeInSecs`, ce paramètre détermine le nombre de profils qualifiés qui doivent être agrégés dans un appel API. <ul><li>Valeur minimale : 1 000</li><li>Valeur maximale : 10 000</li></ul> Par exemple, si vous utilisez la valeur maximale pour les deux paramètres, Experience Platform attend 3 600 secondes où qu’il y ait 10 000 profils qualifiés avant d’effectuer l’appel API, selon ce qui se produit en premier. |
| `configurableAggregation.aggregationKey` | - | Permet d’agréger les profils exportés mappés à la destination en fonction des paramètres décrits ci-dessous. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booléen | Définissez ce paramètre sur `true` pour regrouper les profils exportés vers votre destination par identifiant d’audience. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booléen | Définissez ce paramètre ainsi qu’`includeSegmentId` sur `true` pour regrouper les profils exportés vers votre destination par identifiant et statut d’audience. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booléen | Définissez ce paramètre sur `true` si vous souhaitez regrouper les profils exportés vers la destination par espace de noms d’identité. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booléen | Définissez ce paramètre sur `true` si vous souhaitez que les profils exportés soient agrégés en groupes d’une seule identité (GAID, IDFA, numéros de téléphone, e-mail, etc.). |
| `configurableAggregation.aggregationKey.groups` | Tableau | Créez des listes de groupes d’identités si vous souhaitez regrouper les profils exportés vers la destination par groupes d’espace de noms d’identité. Par exemple, vous pouvez combiner des profils contenant les identifiants mobiles IDFA et GAID dans un appel vers la destination et des e-mails dans un autre en utilisant la configuration montrée dans l’exemple ci-dessus. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment configurer les politiques d’agrégation pour la destination.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Configuration de l’authentification du client](customer-authentication.md)
* [Autorisation OAuth2](oauth2-authorization.md)
* [Champs de données client](customer-data-fields.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Diffusion de destination](destination-delivery.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)

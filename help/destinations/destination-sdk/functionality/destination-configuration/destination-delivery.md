---
description: Découvrez comment configurer les paramètres de diffusion de destination pour les destinations créées avec Destination SDK, afin d’indiquer où vont les données exportées et quelle règle d’authentification est utilisée à l’emplacement où les données atterriront.
title: Diffusion de destination
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 8%

---


# Diffusion de destination

Pour mieux contrôler où se trouvent les données exportées vers votre destination, Destination SDK vous permet de spécifier les paramètres de remise de destination.

La section de diffusion destination indique où vont les données exportées et quelle règle d’authentification est utilisée à l’emplacement où les données atterriront.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consultez les pages de présentation de la configuration de destination suivantes :

* [Utiliser Destination SDK pour configurer une destination de diffusion en continu](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utiliser Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Vous pouvez configurer les paramètres de diffusion de destination via le `/authoring/destinations` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les options de remise de destination prises en charge que vous pouvez utiliser pour votre destination.

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

Lors de la configuration des paramètres de diffusion de destination, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour définir l’endroit où les données exportées doivent être envoyées.

| Paramètre | Type | Description |
|---------|----------|------|
| `authenticationRule` | Chaîne | Indique comment [!DNL Platform] devrait se connecter à votre destination. Valeurs prises en charge :<ul><li>`CUSTOMER_AUTHENTICATION`: Utilisez cette option si les clients Platform se connectent à votre système par l’intermédiaire de l’une des méthodes d’authentification décrites [here](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Utilisez cette option s’il existe un système d’authentification global entre l’Adobe et votre destination et la variable [!DNL Platform] Le client n’a pas besoin de fournir d’informations d’authentification pour se connecter à votre destination. Dans ce cas, vous devez créer un objet d’identification à l’aide de la variable [API des informations d’identification](../../credentials-api/create-credential-configuration.md) configuration. </li><li>`NONE`: Utilisez cette option si aucune authentification n’est requise pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationServerId` | Chaîne | Le `instanceId` de [serveur de destination](../../authoring-api/destination-server/create-destination-server.md) vers lequel vous souhaitez exporter des données. |
| `deliveryMatchers.type` | Chaîne | <ul><li>Lors de la configuration de la diffusion de destination pour les destinations basées sur des fichiers, définissez toujours cette variable sur `SOURCE`.</li><li>Lors de la configuration de la diffusion de destination pour une destination de diffusion en continu, la variable `deliveryMatchers` n’est pas requise.</li></ul> |
| `deliveryMatchers.value` | Chaîne | <ul><li>Lors de la configuration de la diffusion de destination pour les destinations basées sur des fichiers, définissez toujours cette variable sur `batch`.</li><li>Lors de la configuration de la diffusion de destination pour une destination de diffusion en continu, la variable `deliveryMatchers` n’est pas requise.</li></ul> |

{style="table-layout:auto"}

## Paramètres de diffusion de destination pour les destinations de diffusion en continu {#destination-delivery-streaming}

L’exemple ci-dessous montre comment les paramètres de diffusion de destination doivent être configurés pour une destination de diffusion en continu. Notez que la variable `deliveryMatchers` n’est pas nécessaire pour les destinations de diffusion en continu.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Paramètres de diffusion de destination pour les destinations basées sur des fichiers {#destination-delivery-file-based}

L’exemple ci-dessous montre comment configurer les paramètres de diffusion de destination pour une destination basée sur des fichiers. Notez que la variable `deliveryMatchers` est requise pour les destinations basées sur des fichiers.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre comment configurer les emplacements où votre destination doit exporter des données, pour les destinations en flux continu et basées sur des fichiers.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Authentification OAuth 2](oauth2-authentication.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Champs de données client](customer-data-fields.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)
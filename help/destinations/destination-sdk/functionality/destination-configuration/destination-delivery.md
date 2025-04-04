---
description: Découvrez comment configurer les paramètres de diffusion de destination pour les destinations créées avec Destination SDK afin d’indiquer où vont les données exportées et quelle règle d’authentification est utilisée à l’emplacement où les données seront envoyées.
title: Diffusion de destination
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 96%

---

# Diffusion de destination

Pour mieux contrôler où se trouvent les données exportées vers la destination, Destination SDK vous permet de spécifier les paramètres de diffusion de destination.

La section de diffusion de destination indique l’emplacement des données exportées et la règle d’authentification utilisée à l’emplacement d’entrée des données.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Pour comprendre la place de ce composant dans une intégration créée avec Destination SDK, consultez le diagramme de la documentation [Options de configuration](../configuration-options.md) ou consultez les pages de vue d’ensemble de la configuration de destination suivantes :

* [Utiliser Destination SDK pour configurer une destination de diffusion en streaming](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Utilisation de Destination SDK pour configurer une destination basée sur des fichiers](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Vous pouvez configurer les paramètres de diffusion de destination via le point d’entrée `/authoring/destinations`. Pour obtenir des exemples d’appels API détaillés dans lesquels vous pouvez configurer les composants affichés sur cette page, consultez les pages de référence de l’API suivantes.

* [Création d’une configuration de destination](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Mise à jour d’une configuration de destination](../../authoring-api/destination-configuration/update-destination-configuration.md)

Cet article décrit toutes les options de diffusion de destination prises en charge que vous pouvez utiliser pour la destination.

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

Pendant la configuration des paramètres de diffusion de destination, vous pouvez utiliser les paramètres décrits dans le tableau ci-dessous pour définir l’endroit où les données exportées doivent être envoyées.

| Paramètre | Type | Description |
|---------|----------|------|
| `authenticationRule` | Chaîne | Indique comment [!DNL Experience Platform] devrait se connecter à la destination. Valeurs prises en charge :<ul><li>`CUSTOMER_AUTHENTICATION` : utilisez cette option si la clientèle Experience Platform se connecte à votre système via l’une des méthodes d’authentification décrites [ici](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION` : utilisez cette option s’il existe un système d’authentification global entre Adobe et la destination et que le client [!DNL Experience Platform] n’a pas besoin de fournir d’informations d’authentification pour se connecter à la destination. Dans ce cas, vous devez créer des informations d’identification à l’aide de la configuration des [informations d’identification API](../../credentials-api/create-credential-configuration.md). </li><li>`NONE` : utilisez cette option si aucune authentification n’est obligatoire pour envoyer des données à votre plateforme de destination. </li></ul> |
| `destinationServerId` | Chaîne | Paramètre `instanceId` du [serveur de destination](../../authoring-api/destination-server/create-destination-server.md) vers lequel vous souhaitez exporter des données. |
| `deliveryMatchers.type` | Chaîne | <ul><li>Pendant la configuration de la diffusion de destination pour les destinations basées sur des fichiers, définissez toujours ce paramètre sur `SOURCE`.</li><li>Pendant la configuration de la diffusion de destination pour une destination de diffusion en streaming, la section `deliveryMatchers` n’est pas obligatoire.</li></ul> |
| `deliveryMatchers.value` | Chaîne | <ul><li>Pendant la configuration de la diffusion de destination pour les destinations basées sur des fichiers, définissez toujours ce paramètre sur `batch`.</li><li>Pendant la configuration de la diffusion de destination pour une destination de diffusion en streaming, la section `deliveryMatchers` n’est pas obligatoire.</li></ul> |

{style="table-layout:auto"}

## Paramètres de diffusion de destination pour les destinations de diffusion en streaming {#destination-delivery-streaming}

L’exemple ci-dessous montre comment les paramètres de diffusion de destination doivent être configurés pour une destination de diffusion en streaming. Notez que la section `deliveryMatchers` n’est pas obligatoire pour les destinations de diffusion en streaming.

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

L’exemple ci-dessous montre comment les paramètres de diffusion de destination doivent être configurés pour une destination basée sur des fichiers. Notez que la section `deliveryMatchers` n’est pas obligatoire pour les destinations basées sur des fichiers.

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

Vous êtes arrivé au bout de cet article. À présent, vous devriez mieux comprendre comment configurer les emplacements des exportations de données de la destination, tant pour les destinations de diffusion en streaming que pour les destinations basées sur des fichiers.

Pour en savoir plus sur les autres composants de destination, consultez les articles suivants :

* [Authentification du client](customer-authentication.md)
* [Autorisation OAuth2](oauth2-authorization.md)
* [Attributs de l’interface utilisateur](ui-attributes.md)
* [Champs de données client](customer-data-fields.md)
* [Configuration du schéma](schema-configuration.md)
* [Configuration de l’espace de noms d’identité](identity-namespace-configuration.md)
* [Configurations de mappage prises en charge](supported-mapping-configurations.md)
* [Configuration des métadonnées d’audience](audience-metadata-configuration.md)
* [Politique d’agrégation](aggregation-policy.md)
* [Configuration par lots](batch-configuration.md)
* [Qualifications des profils historiques](historical-profile-qualifications.md)

---
description: Découvrez comment formater les requêtes HTTP envoyées à votre point de terminaison. Utilisez le point d’entrée /authoring/destination-servers pour configurer les spécifications de modèle de serveur de destination en Adobe Experience Platform Destination SDK.
title: Spécifications de modèle pour les destinations créées avec Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 24%

---


# Spécifications de modèle pour les destinations créées avec Destination SDK

Utilisez la partie spec du modèle de la configuration du serveur de destination pour configurer la manière de formater les requêtes HTTP envoyées à votre destination.

Dans une spécification de modèle, vous pouvez définir comment transformer les champs d’attribut de profil entre le schéma XDM et le format pris en charge par votre plateforme.

Les spécifications de modèle font partie de la configuration du serveur de destination pour les destinations en temps réel (diffusion en continu).

Pour comprendre où ce composant entre dans une intégration créée avec Destination SDK, reportez-vous au diagramme de la section [options de configuration](../configuration-options.md) ou consulter le guide sur la manière d’effectuer les opérations [utiliser la Destination SDK pour configurer une destination de diffusion en continu ;](../../guides/configure-destination-instructions.md#create-server-template-configuration).

Vous pouvez configurer les spécifications du modèle pour votre destination via le `/authoring/destination-servers` point de terminaison . Consultez les pages de référence d’API suivantes pour obtenir des exemples d’appels d’API détaillés dans lesquels vous pouvez configurer les composants affichés dans cette page.

* [Création d’une configuration de serveur de destination](../../authoring-api/destination-server/create-destination-server.md)
* [Mise à jour de la configuration d’un serveur de destination](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Tous les noms et valeurs de paramètre pris en charge par Destination SDK sont **respect de la casse**. Pour éviter les erreurs de respect de la casse, veuillez utiliser les noms et valeurs des paramètres exactement comme indiqué dans la documentation.

## Types d’intégration pris en charge {#supported-integration-types}

Reportez-vous au tableau ci-dessous pour plus d’informations sur les types d’intégration qui prennent en charge les fonctionnalités décrites sur cette page.

| Type d’intégration | Fonctionnalité de prise en charge |
|---|---|
| Intégrations en temps réel (diffusion en continu) | Oui |
| Intégrations basées sur des fichiers (par lots) | Non |

## Configuration d’une spécification de modèle {#configure-template-spec}

Adobe utilise un langage de modèle similaire à [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) pour transformer les champs du schéma XDM en un format pris en charge par votre destination.

![Mise en surbrillance de la configuration des modèles](../../assets/functionality/destination-server/template-configuration.png)

Pour plus d’informations sur la transformation, consultez les liens ci-dessous :

* [Format des messages](message-format.md)
* [Utiliser une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments ](message-format.md#using-templating)

>[!TIP]
>
>Adobe vous propose un [outil de développement](../../testing-api/streaming-destinations/create-template.md) pour créer et tester un modèle de transformation de messages.

Voir ci-dessous un exemple de modèle de requête HTTP, ainsi que des descriptions de chaque paramètre individuel.

```json
{
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| Paramètre | Type | Description |
|---|---|---|
| `httpMethod` | Chaîne | *Obligatoire.* Méthode qu’Adobe utilise dans les appels vers votre serveur. Méthodes prises en charge : `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `value` | Chaîne | *Obligatoire.* Cette chaîne est la version avec échappement de caractères du modèle qui formate les requêtes HTTP envoyées par Platform au format attendu par votre destination. <br> Pour plus d’informations sur l’écriture du modèle, consultez la section sur [utilisation de modèles](message-format.md#using-templating). <br> Pour plus d’informations sur les caractères d’échappement, consultez la section [Norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Pour un exemple de transformation simple, reportez-vous à la section [attributs de profil](message-format.md#attributes) transformation. |
| `contentType` | Chaîne | *Obligatoire.* Type de contenu que votre serveur accepte. Selon le type de sortie produit par votre modèle de transformation, il peut s’agir de l’une des sorties prises en charge. [Types de contenu des applications HTTP](https://www.iana.org/assignments/media-types/media-types.xhtml#application). Dans la plupart des cas, cette valeur doit être définie sur `application/json`. |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

Après avoir lu cet article, vous devriez mieux comprendre la spécification d’un modèle et la manière dont vous pouvez le configurer.

Pour en savoir plus sur les autres composants du serveur de destination, consultez les articles suivants :

* [Spécifications de serveur pour les destinations créées avec Destination SDK](server-specs.md)
* [Format des messages](message-format.md)
* [Configuration du formatage des fichiers](file-formatting.md)
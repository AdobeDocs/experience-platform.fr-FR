---
description: Les spécifications du serveur et du modèle peuvent être configurées dans Adobe Experience Platform Destination SDK via le point d’entrée commun « /authoring/destination-servers ».
title: Options de configuration des spécifications de serveur et de modèle dans Destination SDK
exl-id: cf493ed5-0bdb-4b90-b84d-73926a566a2a
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: ht
source-wordcount: '425'
ht-degree: 100%

---

# Options de configuration des spécifications du serveur et des modèles pour les destinations de diffusion en continu

## Présentation {#overview}

Les spécifications de serveur et de modèle peuvent être configurées dans Adobe Experience Platform Destination SDK via le point d’entrée commun `/authoring/destination-servers`. Consultez la section [Opérations de point d’entrée de l’API Destinations](./destination-server-api.md) pour obtenir une liste complète des opérations que vous pouvez effectuer sur le point d’entrée.

## Spécifications du serveur {#server-specs}

![Mise en surbrillance de la configuration du serveur](./assets/server-configuration.png)

Les clients pourront activer les données dʼAdobe Experience Platform vers votre destination par le biais d’exportations HTTP. La configuration de serveur contient des informations sur le serveur recevant les messages (le serveur de votre côté).

Ce processus fournit des données utilisateur sous forme d’une série de messages HTTP vers votre plateforme de destination. Les paramètres ci-dessous forment le modèle de spécifications du serveur HTTP.

| Paramètre | Type | Description |
|---|---|---|
| `name` | Chaîne | *Obligatoire.* Représente le nom convivial de votre serveur, visible uniquement par Adobe. Ce nom n’est pas visible pour les partenaires ou les clients. Par exemple, `Moviestar destination server`. |
| `destinationServerType` | Chaîne | *Obligatoire.* Définissez sur `URL_BASED` pour les destinations de diffusion en continu. |
| `templatingStrategy` | Chaîne | *Obligatoire.* <ul><li>Utilisez `PEBBLE_V1` si vous utilisez une macro au lieu d’une valeur fixe dans le champ `value`. Utilisez cette option si vous disposez d’un point d’entrée du type : `https://api.moviestar.com/data/{{customerData.region}}/items` </li><li> Utilisez `NONE` si aucune transformation n’est nécessaire du côté d’Adobe, par exemple si vous avez un point d’entrée tel que : `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Chaîne | *Obligatoire.* Renseignez l’adresse du point d’entrée de l’API auquel Experience Platform doit se connecter. |

{style=&quot;table-layout:auto&quot;}

## Spécifications des modèles {#template-specs}

![Mise en surbrillance de la configuration des modèles](./assets/template-configuration.png)

La spécification des modèles vous permet de configurer le format du message exporté vers votre destination. Adobe utilise un langage de modèle similaire à [Jinja](https://jinja.palletsprojects.com/en/2.11.x/) pour transformer les champs du schéma XDM en un format pris en charge par votre destination. Pour plus d’informations sur la transformation, consultez les liens ci-dessous :

* [Format des messages](./message-format.md)
* [Utiliser une langue de modèle pour les transformations d’identité, d’attributs et d’appartenance aux segments ](./message-format.md#using-templating)

>[!TIP]
>
>Adobe vous propose un [outil de développement](./create-template.md) pour créer et tester un modèle de transformation de messages.

## Exemple de configuration de destination de diffusion en continu  {#example-configuration}

```json
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
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
| `httpMethod` | Chaîne | *Obligatoire.* Méthode qu’Adobe utilise dans les appels vers votre serveur. Les options sont les suivantes : `GET`, `PUT`, `POST`, `DELETE` ou `PATCH`. |
| `templatingStrategy` | Chaîne | *Obligatoire.* Utilisez `PEBBLE_V1`. |
| `value` | Chaîne | *Obligatoire.* Cette chaîne est la version placée dans une séquence dʼéchappement qui transforme les données des clients Platform au format attendu par votre service. <br> Pour plus d’informations sur l’écriture du modèle, consultez la section [Utiliser les modèles](./message-format.md#using-templating). <br> Pour plus d’informations sur les caractères d’échappement, consultez la section [Norme RFC JSON, section 7](https://tools.ietf.org/html/rfc8259#section-7). <br> Pour un exemple de transformation simple, reportez-vous à la transformation des [attributs de profil](./message-format.md#attributes). |
| `contentType` | Chaîne | *Obligatoire.* Type de contenu que votre serveur accepte. Cette valeur est probablement `application/json`. |

{style=&quot;table-layout:auto&quot;}
---
keywords: Experience Platform;home;popular topics;;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience eventExperience event;XDM Experience Event;XDM ExperienceEvent;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema;troubleshooting;FAQ;faq;Union schema;UNION PROFILE;union profile
solution: Experience Platform
title: Guide de dépannage du système de modèle de données d’expérience (XDM)
description: Ce document fournit des réponses aux questions fréquentes sur le système de modèle de données d’expérience (XDM), ainsi qu’un guide de dépannage pour les erreurs courantes.
topic: troubleshooting
translation-type: tm+mt
source-git-commit: e87fcd9f028bc6dedaec0435c4eef54e6aecae2d
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 74%

---


# [!DNL Experience Data Model] (XDM) Guide de dépannage système

This document provides answers to frequently asked questions about [!DNL Experience Data Model] (XDM) System, as well as a troubleshooting guide for common errors. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** est une spécification open source qui définit des schémas normalisés pour la gestion de l’expérience client. The methodology on which [!DNL Experience Platform] is built, **XDM System**, operationalizes [!DNL Experience Data Model] schemas for use by [!DNL Platform] services. Le **[!DNL Schema Registry]** fournit une interface utilisateur et une API RESTful pour accéder à la **[!DNL Schema Library]** dans [!DNL Experience Platform]. Pour plus d’informations, consultez la [documentation XDM](home.md).

## FAQ

The following is a list of answers to frequently asked questions about XDM System and use of the [!DNL Schema Registry] API.

### Comment ajouter des champs à un schéma ?

Vous pouvez ajouter des champs à un schéma à l’aide d’un mixin. Chaque mixin est compatible avec une ou plusieurs classes, ce qui permet de l’utiliser dans n’importe quel schéma qui met en œuvre une de ces classes compatibles. Bien qu’Adobe Experience Platform fournisse plusieurs mixins de secteur avec leurs propres champs prédéfinis, vous pouvez ajouter vos propres champs à un schéma en créant de nouveaux mixins à l’aide de l’API ou de l’interface utilisateur.

Pour plus d’informations sur la création de mixins dans l’ [!DNL Schema Registry] API, consultez le guide [des points de terminaison de](api/mixins.md#create)mixin. Si vous utilisez l’interface utilisateur, consultez le [tutoriel de l’éditeur de schémas](./tutorials/create-schema-ui.md).

### Quelles sont les meilleures utilisations des mixins par rapport aux types de données ?

Les [mixins](./schema/composition.md#mixin) sont des composants qui définissent un ou plusieurs champs dans un schéma. Les mixins imposent la manière dont leurs champs apparaissent dans la hiérarchie du schéma, et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les mixins ne sont compatibles qu’avec des classes spécifiques, identifiées par leur attribut `meta:intendedToExtend`.

Les [types de données](./schema/composition.md#data-type) peuvent également fournir un ou plusieurs champs pour un schéma. Toutefois, contrairement aux mixins, les types de données ne sont pas limités à une classe particulière. Ainsi, les types de données constituent une option plus souple pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes.

### Quel est l’identifiant unique d’un schéma ?

All [!DNL Schema Registry] resources (schemas, mixins, data types, classes) have a URI that acts as an unique ID for reference and lookup purposes. Lorsqu’un schéma est affiché dans l’API, il se trouve dans les attributs `$id` et `meta:altId` de niveau supérieur.

For more information, see the [resource identification](api/getting-started.md#resource-identification) section in the [!DNL Schema Registry] API developer guide.

### Quand un schéma commence-t-il à éviter les modifications avec rupture ?

Des modifications avec rupture peuvent être apportées à un schéma tant qu’il n’a jamais été utilisé pour la création d’un jeu de données ou activé pour être utilisé dans [[!DNL Real-time Customer Profile]](../profile/home.md). Once a schema has been used in dataset creation or enabled for use with [!DNL Real-time Customer Profile], the rules of [Schema Evolution](schema/composition.md#evolution) become strictly enforced by the system.

### Quelle est la taille maximale d’un type de champ long ?

Un type de champ long est un entier dont la taille maximale est de 53 (+1) bits, ce qui lui donne une plage potentielle comprise entre -9007199254740992 et 9007199254740992. Cela est dû à une limitation des possibilités de représentation des entiers longs lors des mises en œuvre de JSON en JavaScript.

Pour plus d’informations sur les types de champ, voir le document sur les contraintes [de type de champ](./schema/field-constraints.md)XDM.

### Comment définir les identités pour mon schéma ?

In [!DNL Experience Platform], identities are used to identify a subject (typically an individual person) regardless of the sources of data being interpreted. Elles sont définies dans les schémas en marquant les champs clés comme « Identité ». Commonly used fields for identity include email address, phone number, [[!DNL Experience Cloud ID (ECID)]](https://docs.adobe.com/content/help/fr-FR/id-service/using/home.html), CRM ID, and other unique ID fields.

Les champs peuvent être marqués comme identités à l’aide de l’API ou de l’interface utilisateur.

#### Définition des identités dans l’API

Dans l’API, les identités sont établies en créant des descripteurs d’identité. Les descripteurs d’identité signalent qu’une propriété spécifique d’un schéma est un identifiant unique.

Les descripteurs d’identité sont créés par une requête POST au point de terminaison /descriptors. Une réponse réussie renvoie un état HTTP 201 (Created) avec un objet de réponse contenant les détails du nouveau descripteur.

For more details on creating identity descriptors in the API, see the document on [descriptors](api/descriptors.md) section in the [!DNL Schema Registry] developer guide.

#### Définition des identités dans l’interface utilisateur

Une fois votre schéma ouvert dans l’éditeur de schémas, cliquez sur le champ de la section **[!UICONTROL Structure]** de l’éditeur que vous souhaitez marquer comme identité. Sous **[!UICONTROL Propriétés du champ]** à droite, cochez la case **[!UICONTROL Identité]**.

Pour plus d’informations sur la gestion des identités dans l’interface utilisateur, consultez la section sur la [définition des champs d’identité](./tutorials/create-schema-ui.md#identity-field) dans le tutoriel de l’éditeur de schémas.

### Mon schéma a-t-il besoin d’une identité principale ?

Les identités principales sont facultatives, car les schémas peuvent en avoir 0 ou 1. Cependant, un schéma doit avoir une identité principale afin de pouvoir être utilisé dans [!DNL Real-time Customer Profile]. Pour plus d’informations, consultez la section [Identité](./tutorials/create-schema-ui.md#identity-field) du tutoriel de l’éditeur de schémas.

### How do I enable a schema for use in [!DNL Real-time Customer Profile]?

Les schémas peuvent être utilisés dans [[!DNL Real-time Customer Profile]](../profile/home.md) grâce à l’ajout d’une balise « union », située dans l’attribut `meta:immutableTags` du schéma. Enabling a schema for use with [!DNL Profile] can be done using the API or the user interface.

#### Enabling an existing schema for [!DNL Profile] using the API

Effectuez une requête PATCH pour mettre à jour le schéma et ajoutez l’attribut `meta:immutableTags` sous forme de tableau contenant la valeur « union ». Si la mise à jour se déroule correctement, la réponse affichera le schéma mis à jour qui contient désormais la balise union.

For more information on using the API to enable a schema for use in [!DNL Real-time Customer Profile], see the [unions](./api/unions.md) document of the [!DNL Schema Registry] developer guide.

#### Enabling an existing schema for [!DNL Profile] using the UI

In [!DNL Experience Platform], click on **[!UICONTROL Schemas]** in the left-navigation, and select the name of the schema you wish to enable from the list of schemas. Ensuite, dans la partie droite de l’éditeur, sous **[!UICONTROL Propriétés du schéma]**, cliquez sur **[!UICONTROL Profil]** pour l’activer.


Pour plus d’informations, consultez la section sur l’[utilisation dans Real-time Customer Profile](./tutorials/create-schema-ui.md#profile) dans le tutoriel de l’éditeur de schémas.

### Puis-je modifier directement un schéma d’union ?

Les schémas d’union sont en lecture seule et générés automatiquement par le système. Ils ne peuvent pas être modifiés directement. Les schémas d’union sont créés pour une classe spécifique lorsqu’une balise « union » est ajoutée au schéma qui met en œuvre cette classe.

Pour plus d’informations sur les unions dans XDM, consultez la section sur les [unions](./api/unions.md) dans le guide de développement de l’API [!DNL Schema Registry]

### Comment dois-je formater mon fichier de données pour ingérer des données dans mon schéma ?

[!DNL Experience Platform] accepte les fichiers de données au format JSON [!DNL Parquet] ou JSON. Le contenu de ces fichiers doit être conforme au schéma référencé par le jeu de données. Pour plus d’informations sur les bonnes pratiques en matière d’ingestion de fichiers de données, reportez-vous à la [présentation de l’ingestion par lots](../ingestion/home.md).

## Erreurs et résolution des problèmes

The following is a list of error messages that you may encounter when working with the [!DNL Schema Registry] API.

### Objet introuvable

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Cette erreur s’affiche lorsque le système n’a pas pu trouver une ressource particulière. La ressource a peut-être été supprimée, ou le chemin d’accès dans l’appel API n’est pas valide. Assurez-vous d’avoir saisi un chemin d’accès valide pour votre appel API avant de réessayer. Vous pouvez vérifier que vous avez saisi l’identifiant correct pour la ressource, et que le chemin d’accès comporte le bon espace de noms avec le conteneur approprié (mondial ou client).

For more information on constructing lookup paths in the API, see the [container](./api/getting-started.md#container) and [resource identification](api/getting-started.md#resource-identification) sections in the [!DNL Schema Registry] developer guide.

### Le titre doit être unique

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

Ce message d’erreur s’affiche lorsque vous tentez de créer une ressource avec un titre déjà utilisé par une autre ressource. Les titres doivent être uniques pour tous les types de ressources. Par exemple, si vous essayez de créer un mixin avec un titre déjà utilisé par un schéma, vous obtiendrez cette erreur.

### Les champs personnalisés doivent utiliser un champ de niveau supérieur

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Ce message d’erreur s’affiche lorsque vous essayez de créer un nouveau mixin avec des champs dont l’espace de noms est incorrect. Les mixins définis par votre organisation IMS doivent être dotés d’un espace de noms avec un `TENANT_ID` afin d’éviter tout conflit avec d’autres ressources du secteur et des fournisseurs. Vous trouverez des exemples détaillés de structures de données appropriées pour les mixins dans le guide [des points de terminaison des](./api/mixins.md#create)mixins.


### [!DNL Real-time Customer Profile] erreurs

Les messages d’erreur suivants sont associés aux opérations impliquées dans l’activation des schémas de [!DNL Real-time Customer Profile]. Pour plus d’informations, consultez la section sur les [unions](./api/unions.md) dans le guide de développement de l’API [!DNL Schema Registry]

#### Pour activer les jeux de données de profil, le schéma doit être valide

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Ce message d’erreur s’affiche lorsque vous tentez d’activer un jeu de données de profil pour un schéma qui n’a pas été activé pour [!DNL Real-time Customer Profile]. Assurez-vous que le schéma contient une balise union avant d’activer le jeu de données.

#### Il doit y avoir un descripteur d’identité de référence

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

This error message displays when you attempt to enable a schema for [!DNL Profile] and one of its properties contains a relationship descriptor without a reference identity descriptor. Ajoutez un descripteur d’identité de référence au champ de schéma en question pour résoudre cette erreur.

#### Les espaces de noms du champ du descripteur d’identité de référence et du schéma de destination doivent correspondre

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

In order to enable schemas that contain relationship descriptors for use in [!DNL Profile], the namespace of the source field and the primary namespace of the target field must be the same. Ce message d’erreur s’affiche lorsque vous essayez d’activer un schéma qui contient un espace de noms incompatible avec son descripteur d’identité de référence. Pour résoudre ce problème, il faut s’assurer que la valeur `xdm:namespace` du champ d’identité du schéma de destination correspond à celle de la propriété `xdm:identityNamespace` dans le descripteur d’identité de référence du champ source.

Pour obtenir une liste des codes d’espaces de noms d’identité pris en charge, consultez la section sur les [espaces de noms standard](../identity-service/namespaces.md) dans la présentation des espaces de noms d’identité.

### Erreurs dans l’en-tête Accept

Most GET requests in the [!DNL Schema Registry] API require an Accept header in order for the system to determine how to format the response. Voici une liste des erreurs courantes associées à l’en-tête Accept. Pour obtenir la liste des en-têtes Accept compatibles pour les différentes requêtes API, veuillez vous référer aux sections correspondantes dans le [guide de développement du registre des schémas](api/getting-started.md).

#### Le paramètre d’en-tête Accept est obligatoire

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête Accept est absent d’une requête API. Assurez-vous qu’un en-tête Accept est inclus avant de réessayer.

#### Support Accept inconnu fourni

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête Accept n’est pas valide. Assurez-vous d’avoir correctement saisi un en-tête Accept compatible avec la requête API que vous essayez de créer avant de réessayer.

#### Format Accept inconnu disponible

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Ce message d’erreur s’affiche lorsque l’en-tête Accept n’a pas été correctement fourni lors de la recherche d’un descripteur. Assurez-vous d’avoir correctement saisi l’un des [en-têtes Accept pour les descripteurs pris en charge](./api/descriptors.md) avant de réessayer.

#### La version doit être indiquée dans l’en-tête Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Ce message d’erreur s’affiche lorsqu’un numéro de version n’a pas été inclus dans l’en-tête Accept. Certains éléments comme les schémas nécessitent de spécifier une version lors de la recherche d’instances individuelles. Un en-tête Accept contenant un numéro de version se présente comme suit :

```plaintext
application/vnd.adobe.xed+json; version=1
```

For a list of supported Accept headers, see the [Accept header](api/getting-started.md#accept) section in the [!DNL Schema Registry] developer guide.

#### La version ne doit pas être indiquée dans l’en-tête Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Si vous essayez d’inclure une version dans votre en-tête Accept lors de l’énumération des ressources (GET), vous obtiendrez cette erreur. Les versions ne sont requises que lorsque vous tentez une requête de recherche sur une seule ressource. Supprimez la version de l’en-tête Accept pour résoudre l’erreur.
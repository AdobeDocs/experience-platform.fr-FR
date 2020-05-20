---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage du système XDM (Experience Data Model)
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8
workflow-type: tm+mt
source-wordcount: '1918'
ht-degree: 0%

---


# Guide de dépannage du système XDM (Experience Data Model)

Ce document fournit des réponses aux questions fréquentes sur le système XDM (Experience Data Model) ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant d’autres services d’Adobe Experience Platform, reportez-vous au guide [de dépannage](../landing/troubleshooting.md)Experience Platform.

**Le modèle de données d’expérience (XDM)** est une spécification open source qui définit des schémas normalisés pour la gestion de l’expérience client. La méthodologie sur laquelle la plate-forme d’expérience est créée, **XDM System**, rend opérationnels les schémas de modèles de données d’expérience pour les utiliser par les services de plateforme. Le Registre **des** Schémas fournit une interface utilisateur et une API RESTful pour accéder à la bibliothèque **de** Schémas dans la plate-forme d’expérience. See the [XDM documentation](home.md) for more information.

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions les plus fréquentes sur XDM System et l&#39;utilisation de l&#39;API de registre de Schéma.

### Comment ajouter des champs à un schéma ?

Vous pouvez ajouter des champs à un schéma à l’aide d’un mixin. Chaque mixin est compatible avec une ou plusieurs classes, ce qui permet d&#39;utiliser le mixin dans n&#39;importe quel schéma qui implémente l&#39;une de ces classes compatibles. Bien qu’Adobe Experience Platform fournisse plusieurs mixins du secteur avec leurs propres champs prédéfinis, vous pouvez ajouter vos propres champs à un schéma en créant de nouveaux mixins à l’aide de l’API ou de l’interface utilisateur.

Pour plus d&#39;informations sur la création de mixins dans l&#39;API, consultez le guide du développeur de l&#39;API de registre de Schémas [Création d&#39;un document de mixin](api/create-mixin.md) . Si vous utilisez l’interface utilisateur, consultez le didacticiel [de l’éditeur de](./tutorials/create-schema-ui.md)Schémas.

### Quelles sont les meilleures utilisations pour les mixins par rapport aux types de données ?

[Les mixins](./schema/composition.md#mixin) sont des composants qui définissent un ou plusieurs champs d’un schéma. Les mixins appliquent la manière dont leurs champs apparaissent dans la hiérarchie du schéma et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les mixins ne sont compatibles qu&#39;avec des classes spécifiques, identifiées par leur `meta:intendedToExtend` attribut.

[Les types](./schema/composition.md#data-type) de données peuvent également fournir un ou plusieurs champs pour un schéma. Cependant, contrairement aux mixins, les types de données ne sont pas limités à une classe particulière. Cela rend les types de données plus flexibles pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes.

### Quel est l’identifiant unique d’un schéma ?

Toutes les ressources de registre de Schéma (schémas, mixins, types de données, classes) ont une URI qui agit comme un identifiant unique à des fins de référence et de recherche. Lors de l’affichage d’un schéma dans l’API, il se trouve dans les attributs de niveau supérieur `$id` et `meta:altId` .

Pour plus d&#39;informations, reportez-vous à la section Identification [du](api/getting-started.md#schema-identification) schéma du guide du développeur d&#39;API du registre de Schémas.

### Quand un schéma début-t-il pour empêcher les modifications ?

Les modifications de rupture peuvent être apportées à un schéma tant qu’elles n’ont jamais été utilisées dans la création d’un jeu de données ou activées pour une utilisation dans le Profil [client en temps](../profile/home.md)réel. Une fois qu’un schéma a été utilisé dans la création de jeux de données ou activé pour une utilisation avec le Profil client en temps réel, les règles de l’évolution [du](schema/composition.md#evolution) Schéma sont strictement appliquées par le système.

### Quelle est la taille maximale d’un type de champ long ?

A long field type is an integer with a maximum size of 53(+1) bits, giving it a potential range between -9007199254740992 and 9007199254740992. Ceci est dû à une limitation de la manière dont les implémentations JavaScript de JSON représentent des entiers longs.

Pour plus d&#39;informations sur les types de champ, consultez la section [Définition des types](api/appendix.md#field-types) de champ XDM dans le guide du développeur de l&#39;API de registre de Schéma.

### Comment définir les identités de mon schéma ?

Dans la plate-forme d’expérience, les identités sont utilisées pour identifier un sujet (généralement une personne individuelle), quelles que soient les sources de données interprétées. Ils sont définis dans les schémas en marquant les champs clés comme &quot;Identité&quot;. Les champs d’identité couramment utilisés comprennent l’adresse électronique, le numéro de téléphone, l’identifiant [Experience Cloud (ECID)](https://docs.adobe.com/content/help/fr-FR/id-service/using/home.html), l’identifiant de gestion de la relation client et d’autres champs d’identifiant unique.

Les champs peuvent être marqués comme identités à l’aide de l’API ou de l’interface utilisateur.

#### Définition des identités dans l’API

Dans l&#39;API, les identités sont établies en créant des descripteurs d&#39;identité. Les descripteurs d’identité signalent qu’une propriété particulière d’un schéma est un identifiant unique.

Les descripteurs d’identité sont créés par une requête POST au point de terminaison /descriptors. En cas de réussite, vous recevrez un état HTTP 201 (créé) et un objet de réponse contenant les détails du nouveau descripteur.

Pour plus d&#39;informations sur la création de descripteurs d&#39;identité dans l&#39;API, reportez-vous à la section document sur les [descripteurs](api/descriptors.md) du guide du développeur du registre des Schémas.

#### Définition des identités dans l’interface utilisateur

Lorsque votre schéma est ouvert dans l&#39;Editeur de Schéma, cliquez sur le champ de la section **Structure** de l&#39;éditeur que vous souhaitez marquer comme une identité. Sous Propriétés **** du champ sur la droite, cochez la case **Identité** .

Pour plus d&#39;informations sur la gestion des identités dans l&#39;interface utilisateur, consultez la section sur la [définition des champs](./tutorials/create-schema-ui.md#identity-field) d&#39;identité dans le didacticiel de l&#39;éditeur de Schémas.

### Mon schéma a-t-il besoin d&#39;une identité primaire ?

Les identités primaires sont facultatives, car les schémas peuvent en avoir 0 ou 1. Cependant, un schéma doit posséder une identité principale pour que le schéma soit activé pour une utilisation dans le Profil client en temps réel. Pour plus d&#39;informations, consultez la section [identité](./tutorials/create-schema-ui.md#identity-field) du didacticiel de l&#39;éditeur de Schémas.

### Comment activer un schéma pour une utilisation dans le Profil client en temps réel ?

Les Schémas peuvent être utilisés dans le Profil [client en temps](../profile/home.md) réel grâce à l’ajout d’une balise &quot;union&quot;, située dans l’ `meta:immutableTags` attribut du schéma. L’activation d’un schéma à utiliser avec le Profil peut s’effectuer à l’aide de l’API ou de l’interface utilisateur.

#### Activation d’un schéma existant pour le Profil à l’aide de l’API

Effectuez une requête PATCH pour mettre à jour le schéma et ajouter l&#39; `meta:immutableTags` attribut sous la forme d&#39;un tableau contenant la valeur &quot;union&quot;. Si la mise à jour réussit, la réponse affiche le schéma mis à jour qui contient désormais la balise d&#39;union.

Pour plus d&#39;informations sur l&#39;utilisation de l&#39;API pour activer un schéma à utiliser dans le Profil client en temps réel, consultez le document des [unions](./api/unions.md) du guide du développeur du registre des Schémas.

#### Activation d’un schéma existant pour le Profil à l’aide de l’interface utilisateur

Dans la plate-forme d’expérience, cliquez sur **Schémas** dans le volet de navigation de gauche, puis sélectionnez le nom du schéma que vous souhaitez activer à partir de la liste des schémas. Ensuite, sur le côté droit de l’éditeur sous Propriétés **du** Schéma, cliquez sur le **Profil** pour activer ou désactiver l’éditeur.


Pour plus d’informations, voir la section sur l’ [utilisation dans le Profil](./tutorials/create-schema-ui.md#profile) client en temps réel dans le didacticiel de l’éditeur de Schéma.

### Puis-je modifier directement un schéma d’union ?

Les schémas d’Union sont en lecture seule et sont générés automatiquement par le système. Ils ne peuvent pas être modifiés directement. Les schémas d’Union sont créés pour une classe spécifique lorsqu’une balise &quot;union&quot; est ajoutée au schéma qui implémente cette classe.

Pour plus d&#39;informations sur les unions dans XDM, consultez la section [unions](./api/unions.md) du guide du développeur d&#39;API de registre de Schémas.

### Comment dois-je formater mon fichier de données pour intégrer des données dans mon schéma ?

Experience Platform accepts datafiles in either Parquet or JSON format. Le contenu de ces fichiers doit être conforme au schéma référencé par le jeu de données. For details about best practices for datafile ingestion, see the [batch ingestion overview](../ingestion/home.md).

## Erreurs et dépannage

The following is a list of error messages that you may encounter when working with the Schema Registry API.

### Object not found

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Cette erreur s&#39;affiche lorsque le système n&#39;a pas pu trouver une ressource particulière. La ressource a peut-être été supprimée ou le chemin d&#39;accès dans l&#39;appel d&#39;API n&#39;est pas valide. Assurez-vous d’avoir saisi un chemin d’accès valide pour votre appel d’API avant de réessayer. You may want to check that you have entered the correct ID for the resource, and that the path is properly namespaced with the appropriate container (global or tenant).

For more information on constructing lookup paths in the API, see the [container](./api/getting-started.md#container) and [schema identification](api/getting-started.md#schema-identification) sections in the Schema Registry developer guide.

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

Ce message d&#39;erreur s&#39;affiche lorsque vous tentez de créer une ressource avec un titre déjà utilisé par une autre ressource. Les titres doivent être uniques pour tous les types de ressources. For example, if you try to create a mixin with a title that is already being used by a schema, you will receive this error.

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

Ce message d’erreur s’affiche lorsque vous tentez de créer un nouveau mixin avec des champs d’espacement de noms incorrects. Les mixins définis par votre organisation IMS doivent espace de nommage leurs champs avec un `TENANT_ID` afin d’éviter les conflits avec d’autres ressources du secteur et des fournisseurs. Vous trouverez des exemples détaillés de structures de données appropriées pour les mixins dans le document sur la [création d&#39;une section de mixin](api/create-mixin.md) dans le guide du développeur de l&#39;API Schéma Registry.


### Erreurs de Profil client en temps réel

Les messages d’erreur suivants sont associés aux opérations d’activation de schémas pour le Profil client en temps réel. Pour plus d&#39;informations, consultez la section [unions](./api/unions.md) du guide du développeur d&#39;API de registre de Schémas.

#### Pour activer les jeux de données de profil, le schéma doit être valide

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Ce message d’erreur s’affiche lorsque vous tentez d’activer un jeu de données de profil pour un schéma qui n’a pas été activé pour le Profil client en temps réel. Assurez-vous que le schéma contient une balise d’union avant d’activer le jeu de données.

#### Il doit y avoir un descripteur d&#39;identité de référence

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

Ce message d’erreur s’affiche lorsque vous tentez d’activer un schéma pour le Profil et que l’une de ses propriétés contient un descripteur de relation sans descripteur d’identité de référence. Ajouter un descripteur d&#39;identité de référence au champ de schéma en question pour résoudre cette erreur.

#### Les espaces de nommage du champ descripteur d&#39;identité de référence et du schéma de destination doivent correspondre

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

Pour activer les schémas qui contiennent des descripteurs de relation à utiliser dans le Profil, l’espace de nommage du champ source et l’espace de nommage principal du champ cible doivent être identiques. Ce message d&#39;erreur s&#39;affiche lorsque vous tentez d&#39;activer un schéma qui contient un espace de nommage sans correspondance pour son descripteur d&#39;identité de référence. Assurez-vous que la `xdm:namespace` valeur du champ d&#39;identité du schéma de destination correspond à celle de la `xdm:identityNamespace` propriété dans le descripteur d&#39;identité de référence du champ source pour résoudre ce problème.

Pour obtenir une liste des codes d&#39;espace de nommage d&#39;identité pris en charge, reportez-vous à la section sur les espaces de nommage [](../identity-service/namespaces.md) standard dans la présentation de l&#39;espace de nommage d&#39;identité.

### Accepter les erreurs d’en-tête

La plupart des requêtes GET dans l&#39;API de registre de Schéma nécessitent un en-tête Accepter pour que le système détermine comment formater la réponse. The following is a list of common errors associated with the Accept header. Pour les listes d&#39;en-têtes d&#39;Acceptation compatibles pour différentes demandes d&#39;API, reportez-vous aux sections correspondantes du guide [de développement du registre des](api/getting-started.md)Schémas.

#### Accepter le paramètre d&#39;en-tête est requis

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête Accepter est absent d’une requête d’API. Assurez-vous qu’un en-tête Accepter est inclus avant de réessayer.

#### Support Accept inconnu fourni

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête Accepter n’est pas valide. Ensure that you have correctly entered an Accept header that is compatible with the API request you are trying to make before trying again.

#### Unknown Accept format available

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Ce message d’erreur s’affiche lorsque l’en-tête Accepter a été fourni de manière incorrecte lors de la recherche d’un descripteur. Assurez-vous d’avoir saisi correctement l’un des en-têtes Accepter [pris en charge pour les descripteurs](./api/descriptors.md) avant de réessayer.

#### La version doit être fournie dans l&#39;en-tête Accept.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Ce message d’erreur s’affiche lorsqu’un numéro de version n’a pas été inclus dans l’en-tête Accepter. Certains éléments, tels que les schémas, nécessitent qu’une version soit spécifiée lors de la recherche d’instances individuelles. Un en-tête Accepter contenant un numéro de version se présente comme suit :

```plaintext
application/vnd.adobe.xed+json; version=1
```

Pour obtenir la liste des en-têtes Accepter pris en charge, reportez-vous à la section d&#39;en-tête [](api/getting-started.md#accept) Accepter du guide du développeur du registre des Schémas.

#### La version ne doit pas être fournie dans l&#39;en-tête Accepter

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Si vous tentez d’inclure une version dans votre en-tête Accepter lors de la mise en vente des ressources (GET), cette erreur s’affichera. Versions are required only when attempting a lookup request on a single resource. Remove the version from the Accept header to resolve the error.
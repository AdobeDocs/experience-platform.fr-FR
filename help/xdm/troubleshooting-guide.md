---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de dépannage du système XDM (Experience Data Model)
topic: troubleshooting
translation-type: tm+mt
source-git-commit: f7c87cc86bfc5017ec5c712d05e39be5c14a7147

---


# Guide de dépannage du système XDM (Experience Data Model)

Ce fournit des réponses aux questions les plus fréquentes sur le système XDM (Experience Data Model), ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant d’autres services d’Adobe Experience Platform, reportez-vous au guide [de dépannage d’](../landing/troubleshooting.md)Experience Platform.

**Le modèle de données d’expérience (XDM)** est une spécification open source qui définit des  normalisées pour la gestion de l’expérience client. La méthodologie sur laquelle est construite la plateforme d’expérience, **XDM System**, rend opérationnel le de modèles de données d’expérience pour l’utilisation par les services de plateforme. Le Registre **des** fournit une interface utilisateur et une API RESTful pour accéder à la bibliothèque **de  de** dans la plateforme d’expérience. See the [XDM documentation](home.md) for more information.

## FAQ

Vous trouverez ci-dessous un  de réponses aux questions les plus fréquentes sur le système XDM et l&#39;utilisation de l&#39;API de registre .

### Comment ajouter des champs à un  de ?

Vous pouvez ajouter des champs à un à l’aide d’un mixin. Chaque mixin est compatible avec une ou plusieurs classes, ce qui permet d’utiliser le mixin dans n’importe quel qui implémente l’une de ces classes compatibles. Bien qu’Adobe Experience Platform fournisse plusieurs mixins du secteur avec leurs propres champs prédéfinis, vous pouvez ajouter vos propres champs à un en créant de nouveaux mixins à l’aide de l’API ou de l’interface utilisateur.

Pour plus d’informations sur la création de nouveaux mixins dans l’API, reportez-vous à la  [Création d’un mixin](api/create-mixin.md) dans le guide du développeur de l’API de registre. Si vous utilisez l’interface utilisateur, reportez-vous au didacticiel [de l’éditeur de](./tutorials/create-schema-ui.md).

### Quelles sont les meilleures utilisations pour les mixins par rapport aux types de données ?

[Les mixins](./schema/composition.md#mixin) sont des composants qui définissent un ou plusieurs champs d’un . Les mixins appliquent la manière dont leurs champs apparaissent dans la hiérarchie des  et présentent donc la même structure dans chaque  dans lequel ils sont inclus. Les mixins ne sont compatibles qu’avec des classes spécifiques, identifiées par leur `meta:intendedToExtend` attribut.

[Les types](./schema/composition.md#data-type) de données peuvent également fournir un ou plusieurs champs pour un  de. Cependant, contrairement aux mixins, les types de données ne sont pas limités à une classe particulière. Cela rend les types de données plus souples pour décrire les structures de données communes qui sont réutilisables dans plusieurs  avec des classes potentiellement différentes.

### Quel est l’identifiant unique d’un  ?

Toutes les ressources de Registre de  (, mixins, types de données, classes) ont un URI qui agit comme un identifiant unique à des fins de référence et de recherche. Lors de l’affichage d’un  dans l’API, il se trouve dans les attributs `$id` et les attributs de niveau supérieur `meta:altId` .

Pour plus d&#39;informations, reportez-vous à la section d&#39;identification [des ](api/getting-started.md#schema-identification) dans le guide du développeur de l&#39;API de registre.

### Quand un -il  éviter les changements ?

Des modifications de rupture peuvent être apportées à un  tant qu’il n’a jamais été utilisé dans la création d’un jeu de données ou activé pour une utilisation dans le [client en temps](../profile/home.md)réel. Une fois qu’un a été utilisé dans la création de jeux de données ou activé pour une utilisation avec le client en temps réel, les règles de l’évolution [de la](schema/composition.md#evolution) de lasont strictement appliquées par le système.

### Quelle est la taille maximale d’un type de champ long ?

Un type de champ long est un entier dont la taille maximale est de 53 (+1) bits, ce qui lui donne une plage potentielle comprise entre -9007199254740992 et 9007199254740992. Cela est dû à une limitation de la manière dont les implémentations JavaScript de JSON représentent des entiers longs.

Pour plus d’informations sur les types de champs, voir la section [Définition des types](api/appendix.md#field-types) de champs XDM dans le guide du développeur de l’API de registre des .

### Comment définir les identités de mes  ?

Dans la plate-forme d’expérience, les identités sont utilisées pour identifier un sujet (généralement une personne individuelle) quelle que soit la source des données interprétées. Ils sont définis dans le  en marquant les champs clés comme &quot;Identité&quot;. Les champs d’identité couramment utilisés comprennent l’adresse électronique, le numéro de téléphone, l’ID [Experience Cloud (ECID)](https://marketing.adobe.com/resources/help/en_US/mcvid/), l’ID de gestion de la relation client et d’autres champs d’ID uniques.

Les champs peuvent être marqués comme identités à l’aide de l’API ou de l’interface utilisateur.

#### Définition des identités dans l’API

Dans l’API, les identités sont établies en créant des descripteurs d’identité. Les descripteurs d’identité signalent qu’une propriété spécifique d’un  d’est un identifiant unique.

Les descripteurs d’identité sont créés par une requête POST au point de fin /descriptors. Si vous réussissez, vous recevrez un état HTTP 201 (créé) et un objet de réponse contenant les détails du nouveau descripteur.

Pour plus d&#39;informations sur la création de descripteurs d&#39;identité dans l&#39;API, reportez-vous à la section  sur les [descripteurs](api/descriptors.md) dans le guide du développeur du registre de .

#### Définition d’identités dans l’interface utilisateur

Lorsque votre est ouvert dans l&#39;éditeur de  de, cliquez sur le champ de la section **Structure** de l&#39;éditeur que vous souhaitez marquer comme une identité. Sous Propriétés **du** champ sur la droite, cliquez sur la case **Identité** .

Pour plus d’informations sur la gestion des identités dans l’interface utilisateur, reportez-vous à la section relative à la [définition des champs](./tutorials/create-schema-ui.md#identity-field) d’identité dans le didacticiel de l’éditeur de  de.

### Mon a-t-il  besoin d&#39;une identité primaire ?

Les identités primaires sont facultatives, car les  peuvent en avoir 0 ou 1. Toutefois, un  doit avoir une identité principale pour que le  être activé pour une utilisation dans le cadre de l’ Client en temps réel. Pour plus d’informations, consultez la section [identité](./tutorials/create-schema-ui.md#identity-field) du didacticiel de l’éditeur de .

### Comment activer un  pour une utilisation dans le client en temps réel ?

Les  de sont activées pour une utilisation dans le [Client en temps](../profile/home.md) réel par l’ajout d’une balise &quot; `meta:immutableTags` &quot;, située dans l’attribut de l’. L’activation d’un pour une utilisation avec des  peut s’effectuer à l’aide de l’API ou de l’interface utilisateur.

#### Activation d’un  existant pour les  de à l’aide de l’API

Effectuez une requête PATCH pour mettre à jour le  du et ajouter l’ `meta:immutableTags` attribut sous forme de tableau contenant la valeur &quot; &quot;. Si la mise à jour réussit, la réponse affichera le mis à jour qui contient désormais la balise .

Pour plus d’informations sur l’utilisation de l’API pour activer un  à utiliser dans le  Client en temps réel, reportez-vous à la [du](./api/unions.md) dedu guide du développeur du registre des.

#### Activation d’un  existant pour les  de à l’aide de l’interface utilisateur

Dans la plate-forme d’expérience, cliquez sur **** dans le volet de navigation de gauche, puis sélectionnez le nom du  que vous souhaitez activer à partir de la  de l’. Ensuite, sur le côté droit de l&#39;éditeur sous Propriétés ****, cliquez sur le **** pour le mettre en marche.


Pour plus d’informations, reportez-vous à la section relative à l’ [utilisation dans le](./tutorials/create-schema-ui.md#profile) Client en temps réel dans le didacticiel de l’éditeur de  de.

### Puis-je modifier   directement ?

  sont en lecture seule et sont générés automatiquement par le système. Ils ne peuvent pas être modifiés directement.   sont créés pour une classe spécifique lorsqu’une balise &quot;&quot; est ajoutée à un qui implémente cette classe.

Pour plus d&#39;informations sur   dans XDM, reportez-vous à la [section](./api/unions.md)  du guide du développeur d&#39;API de registre des.

### Comment dois-je formater mon fichier de données pour intégrer des données dans mon  de ?

Experience Platform accepte les fichiers de données au format Parquet ou JSON. Le contenu de ces fichiers doit être conforme au  de référence du jeu de données. Pour plus d’informations sur les meilleures pratiques d’importation de fichiers de données, reportez-vous à l’aperçu [de l’assimilation par](../ingestion/home.md)lot.

## Erreurs et dépannage

Vous trouverez ci-dessous un de messages d’erreur que vous pouvez rencontrer lorsque vous utilisez l’API de registre de .

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

Cette erreur s&#39;affiche lorsque le système n&#39;a pas pu trouver une ressource particulière. La ressource a peut-être été supprimée ou le chemin d&#39;accès dans l&#39;appel d&#39;API n&#39;est pas valide. Vérifiez que vous avez saisi un chemin valide pour votre appel d’API avant de réessayer. Vous pouvez vérifier que vous avez saisi l’ID correct pour la ressource et que le chemin d’accès porte l’espace de noms approprié avec le  de approprié (global ou locataire).

Pour plus d&#39;informations sur la construction de chemins de recherche dans l&#39;API, reportez-vous aux sections d&#39;identification [des](./api/getting-started.md#container) de [et des  de](api/getting-started.md#schema-identification) dans le guide du développeur du registre de l&#39;.

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

Ce message d’erreur s’affiche lorsque vous tentez de créer une ressource avec un titre déjà utilisé par une autre ressource. Les titres doivent être uniques pour tous les types de ressource. Par exemple, si vous essayez de créer un mixin avec un titre déjà utilisé par un , vous recevrez cette erreur.

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

Ce message d’erreur s’affiche lorsque vous tentez de créer un nouveau mixin avec des champs d’espacement de nom incorrects. Les mixins définis par votre organisation IMS doivent   leurs champs avec un `TENANT_ID` afin d’éviter les conflits avec d’autres ressources du secteur et des fournisseurs. Vous trouverez des exemples détaillés de structures de données appropriées pour les mixins dans le  sur la [création d&#39;un mixin](api/create-mixin.md) dans le guide du développeur de l&#39;API de registre de.


### Erreurs de  du client en temps réel

Les messages d’erreur suivants sont associés aux opérations impliquées dans l’activation des  de pour les  de clients en temps réel. Pour plus d&#39;informations, reportez-vous à la section  [de](./api/unions.md) du guide du développeur de l&#39;API de registre.

#### Pour activer les jeux de données , le doit être valide

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Ce message d’erreur s’affiche lorsque vous tentez d’activer un jeu de données de  pour un qui n’a pas été activé pour l’ Client en temps réel. Assurez-vous que le  contient une balise  avant d’activer le jeu de données.

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

Ce message d’erreur s’affiche lorsque vous tentez d’activer un pour  de et que l’une de ses propriétés contient un descripteur de relation sans descripteur d’identité de référence. Ajouter un descripteur d’identité de référence au champ  en question pour résoudre cette erreur.

#### Le   du champ descripteur d&#39;identité de référence et le de destination doivent correspondre

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

Afin d’activer les  de qui contiennent des descripteurs de relation à utiliser dans les , le  du champ source et le principal du champ de l’d’articles doivent être identiques. Ce message d’erreur s’affiche lorsque vous tentez d’activer un  de qui contient un  sans correspondance pour son descripteur d’identité de référence. Assurez-vous que la `xdm:namespace` valeur du champ d’identité  de destination correspond à celle de la `xdm:identityNamespace` propriété dans le descripteur d’identité de référence du champ source pour résoudre ce problème.

Pour un de codes d&#39; d&#39;identité  pris en charge, reportez-vous à la section sur les [](../identity-service/namespaces.md) destandard dans l&#39;aperçu du d&#39;identité.

### Accepter les erreurs d’en-tête

La plupart des requêtes GET dans l’API de Registre  du nécessitent un en-tête Accept pour que le système détermine le format de la réponse. Voici un  d’erreurs courantes associées à l’en-tête Accepter. Pour les  d&#39;en-têtes Accepter compatibles pour les différentes demandes d&#39;API, reportez-vous aux sections correspondantes du guide [du développeur du registre de](api/getting-started.md).

#### Le paramètre d&#39;en-tête Accepter est obligatoire

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête Accept est manquant dans une requête d’API. Assurez-vous qu’un en-tête Accepter est inclus avant de réessayer.

#### Support Accept inconnu fourni

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête Accepter n’est pas valide. Assurez-vous d’avoir saisi correctement un en-tête Accept compatible avec la demande d’API que vous tentez d’effectuer avant de réessayer.

#### Format Accept inconnu disponible

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Ce message d’erreur s’affiche lorsque l’en-tête Accepter a été fourni de manière incorrecte lors de la recherche d’un descripteur. Vérifiez que vous avez saisi correctement l’un des en-têtes Accepter [pris en charge pour les descripteurs](./api/descriptors.md) avant de réessayer.

#### La version doit être fournie dans l’en-tête Accept.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Ce message d’erreur s’affiche lorsqu’un numéro de version n’a pas été inclus dans l’en-tête Accepter. Certains éléments, tels que le, nécessitent une version à spécifier lors de la recherche d’instances individuelles. Un en-tête Accept contenant un numéro de version se présente comme suit :

```plaintext
application/vnd.adobe.xed+json; version=1
```

Pour un  d’en-têtes Accepter pris en charge, reportez-vous à la section d’en-tête [Accepter](api/getting-started.md#accept) du guide du développeur de registre de .

#### La version ne doit pas être fournie dans l’en-tête Accept.

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Si vous tentez d’inclure une version dans l’en-tête Accepter lors de la liste des ressources GET, vous recevez cette erreur. Les versions ne sont requises que lorsque vous tentez une requête de recherche sur une ressource unique. Supprimez la version de l’en-tête Accepter pour résoudre l’erreur.
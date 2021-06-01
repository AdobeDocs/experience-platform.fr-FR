---
keywords: Experience Platform;accueil;rubriques populaires;XDM;système XDM;profil individuel XDM;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;événement d’expérience;événement XDM ExperienceEvent;XDM ExperienceEvent;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;schéma;schéma;FAQ;schéma d’union;PROFIL d’union;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;
solution: Experience Platform
title: Guide de dépannage du système XDM
description: Trouvez des réponses aux questions fréquentes sur le modèle de données d’expérience (XDM), y compris les étapes pour résoudre les erreurs d’API courantes.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 415938f6f3aeec342774b73d1ae5f2dc0e27349c
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 36%

---

# Guide de dépannage du système XDM

Ce document fournit des réponses aux questions fréquentes sur [!DNL Experience Data Model] (XDM) et le système XDM dans Adobe Experience Platform, y compris un guide de dépannage pour les erreurs courantes. Pour les questions et le dépannage relatifs aux autres services Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** est une spécification open source qui définit des schémas normalisés pour la gestion de l’expérience client. La méthodologie sur laquelle [!DNL Experience Platform] est construit, **Système XDM**, rend les schémas [!DNL Experience Data Model] opérationnels pour être utilisés par les services [!DNL Platform]. **[!DNL Schema Registry]** fournit une interface utilisateur et une API RESTful pour accéder à **[!DNL Schema Library]** dans [!DNL Experience Platform]. Pour plus d’informations, consultez la [documentation XDM](home.md).

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes sur le système XDM et l’utilisation de l’API [!DNL Schema Registry].

### Comment ajouter des champs à un schéma ?

Vous pouvez ajouter des champs à un schéma à l’aide d’un groupe de champs de schéma. Chaque groupe de champs est compatible avec une ou plusieurs classes, ce qui permet d’utiliser le groupe de champs dans n’importe quel schéma qui implémente l’une de ces classes compatibles. Bien que Adobe Experience Platform fournisse plusieurs groupes de champs du secteur avec leurs propres champs prédéfinis, vous pouvez ajouter vos propres champs à un schéma en créant des groupes de champs personnalisés à l’aide de l’API ou de l’interface utilisateur.

Pour plus d’informations sur la création de groupes de champs dans l’API [!DNL Schema Registry], consultez le [guide de point de terminaison de groupe de champs](api/field-groups.md#create). Si vous utilisez l’interface utilisateur, consultez le [tutoriel de l’éditeur de schémas](./tutorials/create-schema-ui.md).

### Quelles sont les meilleures utilisations des groupes de champs par rapport aux types de données ?

[Les ](./schema/composition.md#field-group) groupes de champs sont des composants qui définissent un ou plusieurs champs d’un schéma. Les groupes de champs imposent la manière dont leurs champs apparaissent dans la hiérarchie du schéma et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les groupes de champs ne sont compatibles qu’avec des classes spécifiques, identifiées par leur attribut `meta:intendedToExtend`.

Les [types de données](./schema/composition.md#data-type) peuvent également fournir un ou plusieurs champs pour un schéma. Cependant, contrairement aux groupes de champs, les types de données ne sont pas limités à une classe particulière. Ainsi, les types de données constituent une option plus souple pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes.

### Qu’est-ce que l’ID unique d’un schéma ?

Toutes les ressources [!DNL Schema Registry] (schémas, groupes de champs, types de données, classes) ont un URI qui agit comme un identifiant unique à des fins de référence et de recherche. Lorsqu’un schéma est affiché dans l’API, il se trouve dans les attributs `$id` et `meta:altId` de niveau supérieur.

Pour plus d’informations, voir la section [identification des ressources](api/getting-started.md#resource-identification) dans le guide de l’API [!DNL Schema Registry].

### Quand un schéma commence-t-il à éviter les modifications avec rupture ?

Des modifications avec rupture peuvent être apportées à un schéma tant qu’il n’a jamais été utilisé pour la création d’un jeu de données ou activé pour être utilisé dans [[!DNL Real-time Customer Profile]](../profile/home.md). Une fois qu’un schéma a été utilisé pour la création d’un jeu de données ou activé pour être utilisé avec [!DNL Real-time Customer Profile], les règles de [Evolution des schémas](schema/composition.md#evolution) sont strictement appliquées par le système.

### Quelle est la taille maximale d’un type de champ long ?

Un type de champ long est un entier dont la taille maximale est de 53 (+1) bits, ce qui lui donne une plage potentielle comprise entre -9007199254740992 et 9007199254740992. Cela est dû à une limitation des possibilités de représentation des entiers longs lors des mises en œuvre de JSON en JavaScript.

Pour plus d’informations sur les types de champ, consultez le document sur les [contraintes de type de champ XDM](./schema/field-constraints.md).

### Comment définir les identités pour mon schéma ?

Dans [!DNL Experience Platform], les identités sont utilisées pour identifier un sujet (généralement une personne individuelle), quelles que soient les sources de données interprétées. Elles sont définies dans les schémas en marquant les champs clés comme « Identité ». Les champs généralement utilisés pour l’identité comprennent l’adresse électronique, le numéro de téléphone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), l’ID CRM et d’autres champs d’ID uniques.

Les champs peuvent être marqués comme identités à l’aide de l’API ou de l’interface utilisateur.

#### Définition des identités dans l’API

Dans l’API, les identités sont établies en créant des descripteurs d’identité. Les descripteurs d’identité signalent qu’une propriété spécifique d’un schéma est un identifiant unique.

Les descripteurs d’identité sont créés par une requête POST au point de terminaison /descriptors. Une réponse réussie renvoie un état HTTP 201 (Created) avec un objet de réponse contenant les détails du nouveau descripteur.

Pour plus d’informations sur la création de descripteurs d’identité dans l’API, consultez le document sur la section [descripteurs](api/descriptors.md) du guide de développement [!DNL Schema Registry].

#### Définition des identités dans l’interface utilisateur

Une fois votre schéma ouvert dans l’éditeur de schémas, sélectionnez le champ de la section **[!UICONTROL Structure]** de l’éditeur que vous souhaitez marquer comme identité. Sous **[!UICONTROL Propriétés du champ]** à droite, cochez la case **[!UICONTROL Identité]** .

Pour plus d’informations sur la gestion des identités dans l’interface utilisateur, consultez la section sur la [définition des champs d’identité](./tutorials/create-schema-ui.md#identity-field) dans le tutoriel de l’éditeur de schémas.

### Mon schéma a-t-il besoin d’une identité principale ?

Les identités Principal sont facultatives, car les schémas peuvent n’avoir aucun ou l’un d’eux. Cependant, un schéma doit avoir une identité principale afin de pouvoir être utilisé dans [!DNL Real-time Customer Profile]. Pour plus d’informations, consultez la section [Identité](./tutorials/create-schema-ui.md#identity-field) du tutoriel de l’éditeur de schémas.

### Comment activer un schéma à utiliser dans [!DNL Real-time Customer Profile] ?

Les schémas peuvent être utilisés dans [[!DNL Real-time Customer Profile]](../profile/home.md) en ajoutant une balise &quot;union&quot; dans l’attribut `meta:immutableTags` du schéma. L’activation d’un schéma à utiliser avec [!DNL Profile] peut être effectuée à l’aide de l’API ou de l’interface utilisateur.

#### Activation d’un schéma existant pour [!DNL Profile] à l’aide de l’API

Effectuez une requête PATCH pour mettre à jour le schéma et ajoutez l’attribut `meta:immutableTags` sous forme de tableau contenant la valeur « union ». Si la mise à jour se déroule correctement, la réponse affichera le schéma mis à jour qui contient désormais la balise union.

Pour plus d’informations sur l’utilisation de l’API pour activer un schéma à utiliser dans [!DNL Real-time Customer Profile], consultez le document [unions](./api/unions.md) du guide de développement [!DNL Schema Registry].

#### Activation d’un schéma existant pour [!DNL Profile] à l’aide de l’interface utilisateur

Dans [!DNL Experience Platform], sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche, puis sélectionnez le nom du schéma que vous souhaitez activer dans la liste des schémas. Ensuite, dans la partie droite de l’éditeur, sous **[!UICONTROL Propriétés du schéma]**, sélectionnez **[!UICONTROL Profil]** pour l’activer.


Pour plus d’informations, consultez la section sur l’[utilisation dans Real-time Customer Profile](./tutorials/create-schema-ui.md#profile) dans le tutoriel de l’éditeur de schémas.

### Puis-je modifier directement un schéma d’union ?

Les schémas d’union sont en lecture seule et générés automatiquement par le système. Ils ne peuvent pas être modifiés directement. Les schémas d’union sont créés pour une classe spécifique lorsqu’une balise « union » est ajoutée au schéma qui met en œuvre cette classe.

Pour plus d’informations sur les unions dans XDM, consultez la section [unions](./api/unions.md) du guide de l’API [!DNL Schema Registry].

### Comment dois-je formater mon fichier de données pour ingérer des données dans mon schéma ?

[!DNL Experience Platform] accepte les fichiers de données au format JSON  [!DNL Parquet] ou JSON. Le contenu de ces fichiers doit être conforme au schéma référencé par le jeu de données. Pour plus d’informations sur les bonnes pratiques en matière d’ingestion de fichiers de données, reportez-vous à la [présentation de l’ingestion par lots](../ingestion/home.md).

## Erreurs et résolution des problèmes

Voici une liste des messages d’erreur que vous pouvez rencontrer lors de l’utilisation de l’API [!DNL Schema Registry].

### Ressource introuvable

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

Cette erreur s’affiche lorsque le système n’a pas pu trouver une ressource particulière. La ressource a peut-être été supprimée, ou le chemin d’accès dans l’appel API n’est pas valide. Assurez-vous d’avoir saisi un chemin d’accès valide pour votre appel API avant de réessayer. Vous pouvez vérifier que vous avez saisi l’identifiant correct pour la ressource, et que le chemin d’accès comporte le bon espace de noms avec le conteneur approprié (mondial ou client).

>[!NOTE]
>
>Selon le type de ressource récupéré, cette erreur peut utiliser l’un des URI `type` suivants :
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Pour plus d’informations sur la création de chemins de recherche dans l’API, consultez les sections [container](./api/getting-started.md#container) et [identification des ressources](api/getting-started.md#resource-identification) du guide de développement [!DNL Schema Registry].

### Titre non unique

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

Ce message d’erreur s’affiche lorsque vous tentez de créer une ressource avec un titre déjà utilisé par une autre ressource. Les titres doivent être uniques pour tous les types de ressources. Par exemple, si vous essayez de créer un groupe de champs avec un titre déjà utilisé par un schéma, vous recevrez cette erreur.

### Erreur de validation d’espace de noms

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

Ce message d’erreur s’affiche lorsque vous tentez de créer une ressource avec des champs dont l’espace de noms est incorrect ou d’ajouter des champs dont l’espace de noms est incorrect à une ressource existante.

Les ressources définies par votre organisation IMS doivent placer leurs champs sous votre ID de tenant afin d’éviter tout conflit avec d’autres ressources du secteur et du fournisseur. Lors de la création d’un schéma à l’aide de groupes de champs standard, tous les champs personnalisés que vous ajoutez dans la structure de ces groupes doivent également comporter un espace de noms sous votre identifiant de tenant.

>[!NOTE]
>
>Selon la nature spécifique de l’erreur d’espace de noms, cette erreur peut utiliser l’un des URI `type` suivants avec différents détails de message :
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Vous trouverez des exemples détaillés de structures de données appropriées pour les ressources XDM dans le guide de l’API Schema Registry :

* [Création d’une classe personnalisée](./api/classes.md#create)
* [Création d’un groupe de champs personnalisé](./api/field-groups.md#create)
* [Création d’un type de données personnalisé](./api/data-types.md#create)

### En-tête Accept non valide

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

Les requêtes de GET dans l’API [!DNL Schema Registry] nécessitent un en-tête `Accept` pour que le système détermine comment formater la réponse. Cette erreur se produit lorsqu’un en-tête `Accept` requis n’est pas valide ou est absent.

Selon le point de terminaison que vous utilisez, la propriété `detailed-message` indique à quoi doit ressembler un en-tête `Accept` valide pour une réponse réussie. Assurez-vous d’avoir correctement saisi un en-tête `Accept` compatible avec la requête API que vous essayez d’effectuer avant de réessayer.

>[!NOTE]
>
>Selon le point de terminaison utilisé, cette erreur peut utiliser l’un des URI `type` suivants :
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Pour obtenir la liste des en-têtes Accept compatibles pour les différentes requêtes API, veuillez vous référer aux sections correspondantes dans le [guide de développement du registre des schémas](./api/overview.md).

### [!DNL Real-time Customer Profile] errors

Les messages d’erreur suivants sont associés aux opérations impliquées dans l’activation des schémas de [!DNL Real-time Customer Profile]. Pour plus d’informations, consultez la section [unions](./api/unions.md) du guide de l’API [!DNL Schema Registry].

#### Il doit y avoir un descripteur d’identité de référence

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

Ce message d’erreur s’affiche lorsque vous tentez d’activer un schéma pour [!DNL Profile] et que l’une de ses propriétés contient un descripteur de relation sans descripteur d’identité de référence. Ajoutez un descripteur d’identité de référence au champ de schéma en question pour résoudre cette erreur.

#### Les espaces de noms du champ du descripteur d’identité de référence et du schéma de destination doivent correspondre

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

Pour activer les schémas qui contiennent des descripteurs de relation à utiliser dans [!DNL Profile], l’espace de noms du champ source et l’espace de noms Principal du champ cible doivent être identiques. Ce message d’erreur s’affiche lorsque vous essayez d’activer un schéma qui contient un espace de noms incompatible avec son descripteur d’identité de référence. Pour résoudre ce problème, il faut s’assurer que la valeur `xdm:namespace` du champ d’identité du schéma de destination correspond à celle de la propriété `xdm:identityNamespace` dans le descripteur d’identité de référence du champ source.

Pour obtenir la liste des codes d’espace de noms d’identité standard, reportez-vous à la section sur les [espaces de noms standard](../identity-service/namespaces.md) dans la présentation des espaces de noms d’identité.

#### Le schéma doit inclure un identityMap ou une identité Principale.

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

Avant d’activer un schéma pour Profile, vous devez d’abord [créer un descripteur d’identité Principal](./api/descriptors.md#create) pour le schéma, ou inclure un champ de carte d’identité pour agir à la place sur l’identité Principale.
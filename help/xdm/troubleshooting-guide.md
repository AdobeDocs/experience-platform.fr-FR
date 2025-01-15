---
keywords: Experience Platform;rubriques populaires;XDM;système XDM;profil individuel XDM;Événement d’expérience XDM;Événement d’expérience XDM;Événementd’expérience;événement d’expérienceEvénementd’expérience;Événement d’expérience XDM;Événementd’expérience XDM;modèle de données d’expérience;Modèle de données d’expérience;Modèle de Données d’expérience;modèle de données;Modèle de Données;schéma;dépannage;Questions fréquentes;questions fréquentes;schéma d’union;PROFIL D’UNION;profil d’union;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guide de dépannage du système XDM
description: Trouvez des réponses aux questions fréquentes sur le modèle de données d’expérience (XDM), y compris les étapes pour résoudre les erreurs d’API courantes.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: b345330595aadcfe2380dd1795802470b249cb4a
workflow-type: tm+mt
source-wordcount: '2347'
ht-degree: 82%

---

# Guide de dépannage du système XDM

Ce document répond aux questions fréquentes sur [!DNL Experience Data Model] (XDM) et le système XDM dans Adobe Experience Platform, y compris un guide de dépannage pour les erreurs courantes. Pour les questions et le dépannage relatifs aux autres services Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model] (XDM)** est une spécification open source conçue pour définir des schémas normalisés pour la gestion de l’expérience client. La méthodologie sur laquelle repose [!DNL Experience Platform], **le système XDM**, rend les schémas [!DNL Experience Data Model] opérationnels pour qu’ils soient utilisés par les services de [!DNL Platform]. Le **[!DNL Schema Registry]** fournit une interface utilisateur et une API RESTful pour accéder à **[!DNL Schema Library]** dans [!DNL Experience Platform]. Pour plus d’informations, consultez la [documentation XDM](home.md).

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes concernant le système XDM et l’utilisation de l’API [!DNL Schema Registry].

## Principes de base des schémas

Dans cette section, vous trouverez des réponses à des questions fondamentales sur la structure des schémas, l’utilisation des champs et l’identification dans le système XDM.

### Comment ajouter des champs à un schéma ?

Vous pouvez ajouter des champs à un schéma à l’aide d’un groupe de champs de schéma. Chaque groupe de champs est compatible avec une ou plusieurs classes, ce qui permet de l’utiliser dans n’importe quel schéma qui met en œuvre une de ces classes compatibles. Bien qu’Adobe Experience Platform fournisse plusieurs groupes de champs de secteur avec leurs propres champs prédéfinis, vous pouvez ajouter vos propres champs à un schéma en créant de nouveaux groupes de champ personnalisés à l’aide de l’API ou de l’interface utilisateur.

Pour plus d’informations sur la création de groupes de champs dans l’API [!DNL Schema Registry], voir le [guide de point d’entrée des groupes de champs](api/field-groups.md#create). Si vous utilisez l’interface utilisateur, consultez le [tutoriel de l’éditeur de schémas](./tutorials/create-schema-ui.md).

### Quelles sont les meilleures utilisations des groupes de champs par rapport aux types de données ?

Les [groupes de champs](./schema/composition.md#field-group) sont des composants qui définissent un ou plusieurs champs dans un schéma. Les groupes de champs imposent la manière dont leurs champs apparaissent dans la hiérarchie du schéma, et présentent donc la même structure dans chaque schéma dans lequel ils sont inclus. Les groupes de champs ne sont compatibles qu’avec des classes spécifiques, identifiées par leur attribut `meta:intendedToExtend`.

Les [types de données](./schema/composition.md#data-type) peuvent également fournir un ou plusieurs champs pour un schéma. Toutefois, contrairement aux groupes de champs, les types de données ne sont pas limités à une classe particulière. Ainsi, les types de données constituent une option plus souple pour décrire des structures de données communes réutilisables sur plusieurs schémas avec des classes potentiellement différentes.

### Qu’est-ce que l’ID unique d’un schéma ?

Toutes les ressources [!DNL Schema Registry] (schémas, groupes de champs, types de données, classes) ont un URI qui agit comme un ID unique à des fins de référence et de recherche. Lorsqu’un schéma est affiché dans l’API, il se trouve dans les attributs `$id` et `meta:altId` de niveau supérieur.

Pour plus d’informations, consultez la section sur l’[identification des ressources](api/getting-started.md#resource-identification) dans le guide de l’API [!DNL Schema Registry].

### Quelle est la taille maximale d’un type de champ long ?

Un type de champ long est un entier dont la taille maximale est de 53 (+1) bits, ce qui lui donne une plage potentielle comprise entre -9007199254740992 et 9007199254740992. Cela est dû à une limitation des possibilités de représentation des entiers longs lors des mises en œuvre de JSON en JavaScript.

Pour plus d’informations sur les types de champs, consultez le document sur les [Contraintes de type de champ XDM](./schema/field-constraints.md).

### Qu’est-ce que meta:AltId ?

`meta:altId` est l’identifiant unique d’un schéma. Le `meta:altId` fournit un identifiant de référence facile à utiliser dans les appels API. Cet identifiant évite d’avoir à être codé/décodé chaque fois qu’il est utilisé comme avec le format URI JSON.
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### Quelles sont les restrictions d’utilisation pour un type de données de mappage ?

XDM place les restrictions suivantes sur l’utilisation de ce type de données :

- Les types de carte DOIVENT être de type objet .
- Les propriétés des types de carte NE DOIVENT PAS ÊTRE définies (en d’autres termes, ils définissent des objets « vides »).
- Les types de mappage DOIVENT inclure un champ additionnelProperties.type qui décrit les valeurs qui peuvent être placées dans le mappage, soit une chaîne, soit un entier.
- La segmentation d’entités multiples peut uniquement être définie en fonction des clés de mappage et non des valeurs.
- Les mappages ne sont pas pris en charge pour les audiences de compte.

Pour plus d’informations, consultez la [restrictions d’utilisation des objets map](./ui/fields/map.md#restrictions).

>[!NOTE]
>
>Les cartes à plusieurs niveaux ou les cartes de cartes ne sont pas prises en charge.

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## Identity Management de schéma

Cette section contient les réponses aux questions courantes sur la définition et la gestion des identités dans vos schémas.

### Comment définir les identités pour mon schéma ?

Dans [!DNL Experience Platform], les identités sont utilisées pour identifier un sujet (généralement une personne en particulier), quelles que soient les sources de données interprétées. Elles sont définies dans les schémas en marquant les champs clés comme « Identité ». Les champs généralement utilisés pour l’identité comprennent l’adresse e-mail, le numéro de téléphone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=fr), l’identifiant CRM ou d’autres champs d’identification uniques.

Les champs peuvent être marqués comme identités à l’aide de l’API ou de l’interface utilisateur.

### Définition des identités dans l’API

Dans l’API, les identités sont établies en créant des descripteurs d’identité. Les descripteurs d’identité signalent qu’une propriété spécifique d’un schéma est un identifiant unique.

Les descripteurs d’identité sont créés par une requête POST au point d’entrée /descriptors. Une réponse réussie renvoie un état HTTP 201 (Created) avec un objet de réponse contenant les détails du nouveau descripteur.

Pour plus d’informations sur la création de descripteurs d’identité dans l’API, consultez le document sur la section des [descripteurs](api/descriptors.md) dans le guide de développement du [!DNL Schema Registry].

### Définition des identités dans l’interface utilisateur

Une fois votre schéma ouvert dans l’éditeur de schémas, sélectionnez le champ de la section **[!UICONTROL Structure]** de l’éditeur que vous souhaitez marquer comme identité. Sous **[!UICONTROL Propriétés du champ]** à droite, cochez la case **[!UICONTROL Identité]**.

Pour plus d’informations sur la gestion des identités dans l’interface utilisateur, consultez la section sur la [définition des champs d’identité](./tutorials/create-schema-ui.md#identity-field) dans le tutoriel de l’éditeur de schémas.

### Mon schéma a-t-il besoin d’une identité principale ?

Les identités principales sont facultatives, car les schémas peuvent en avoir une ou aucune. Cependant, un schéma doit avoir une identité principale afin de pouvoir être utilisé dans [!DNL Real-Time Customer Profile]. Pour plus d’informations, consultez la section [Identité](./tutorials/create-schema-ui.md#identity-field) du tutoriel de l’éditeur de schémas.

## Activation du profil de schéma

Cette section fournit des conseils sur l’activation des schémas à utiliser avec le profil client en temps réel.

### Comment activer un schéma pour l’utiliser dans [!DNL Real-Time Customer Profile] ?

Les schémas peuvent être utilisés dans [[!DNL Real-Time Customer Profile]](../profile/home.md) grâce à l’ajout d’une balise « union » dans l’attribut `meta:immutableTags` du schéma. L’activation d’un schéma à utiliser avec [!DNL Profile] peut se faire à l’aide de l’API ou de l’interface utilisateur.

### Activation d’un schéma existant pour [!DNL Profile] à l’aide de l’API

Effectuez une requête PATCH pour mettre à jour le schéma et ajoutez l’attribut `meta:immutableTags` sous forme de tableau contenant la valeur « union ». Si la mise à jour se déroule correctement, la réponse affichera le schéma mis à jour qui contient désormais la balise union.

Pour plus d’informations sur l’utilisation de l’API pour activer un schéma à utiliser dans [!DNL Real-Time Customer Profile], consultez le document sur les [unions](./api/unions.md) du guide de développement du [!DNL Schema Registry].

### Activation d’un schéma existant pour [!DNL Profile] à l’aide de l’interface utilisateur

Dans [!DNL Experience Platform], cliquez sur **[!UICONTROL Schémas]** dans le volet de navigation de gauche, et sélectionnez le nom du schéma que vous souhaitez activer dans la liste des schémas. Ensuite, dans la partie droite de l’éditeur, sous **[!UICONTROL Propriétés du schéma]**, sélectionnez **[!UICONTROL Profile]** pour l’activer.

Pour plus d’informations, consultez la section sur l’[utilisation dans le profil client en temps réel](./tutorials/create-schema-ui.md#profile) dans le tutoriel de l’[!UICONTROL éditeur de schémas].

### Lorsque les données Adobe Analytics sont importées en tant que source, le schéma créé automatiquement est-il activé pour Profile ?

Le schéma n’est pas automatiquement activé pour le profil client en temps réel. Vous devez activer explicitement le jeu de données pour Profil en fonction du schéma activé pour Profil. Consultez la documentation pour découvrir les [étapes et exigences nécessaires pour activer un jeu de données à utiliser dans le profil client en temps réel](../catalog/datasets/user-guide.md#enable-profile).

### Puis-je supprimer des schémas activés pour Profile ?

Vous ne pouvez pas supprimer un schéma une fois qu’il a été activé pour le profil client en temps réel. Une fois qu’un schéma est activé pour Profil, il ne peut pas être désactivé ni supprimé, et les champs ne peuvent pas être supprimés du schéma. Par conséquent, il est essentiel de planifier et de vérifier soigneusement la configuration du schéma avant de l’activer pour Profile. Vous pouvez toutefois supprimer un jeu de données activé pour Profil. Vous trouverez des informations ici : <https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

Si vous ne souhaitez plus qu’un schéma activé pour Profile soit utilisé, il est recommandé de renommer le schéma pour inclure **Ne pas utiliser** ou **Inactif**.

## Modification des schémas et restrictions

Cette section fournit des clarifications sur les règles de modification des schémas et la prévention des modifications avec rupture.

### Quand un schéma commence-t-il à éviter les modifications avec rupture ?

Des modifications avec rupture peuvent être apportées à un schéma tant qu’il n’a jamais été utilisé pour la création d’un jeu de données ou activé pour être utilisé dans [[!DNL Real-Time Customer Profile]](../profile/home.md). Une fois qu’un schéma a été utilisé pour la création d’un jeu de données ou activé pour être utilisé avec [!DNL Real-Time Customer Profile], les règles de l’[évolution des schémas](schema/composition.md#evolution) sont strictement appliquées par le système.

### Puis-je modifier directement un schéma d’union ?

Les schémas d’union sont en lecture seule et générés automatiquement par le système. Ils ne peuvent pas être modifiés directement. Les schémas d’union sont créés pour une classe spécifique lorsqu’une balise « union » est ajoutée au schéma qui met en œuvre cette classe.

Pour plus d’informations sur les unions dans XDM, consultez la section sur les [unions](./api/unions.md) dans le guide de l’API [!DNL Schema Registry].

### Comment dois-je formater mon fichier de données pour ingérer des données dans mon schéma ?

[!DNL Experience Platform] accepte les fichiers de données au format [!DNL Parquet] ou JSON. Le contenu de ces fichiers doit être conforme au schéma référencé par le jeu de données. Pour plus d’informations sur les bonnes pratiques en matière d’ingestion de fichiers de données, reportez-vous à la [présentation de l’ingestion par lots](../ingestion/home.md).

### Comment convertir un schéma en schéma en lecture seule ?

Vous ne pouvez actuellement pas convertir un schéma en lecture seule.

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
>Selon le type de ressource récupéré, cette erreur peut utiliser l’une des URI `type` suivantes :
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

Pour plus d’informations sur la création de chemins de recherche dans l’API, consultez les sections sur les [conteneurs](./api/getting-started.md#container) et l’[identification des ressources](api/getting-started.md#resource-identification) dans le guide du développement de [!DNL Schema Registry].

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

Ce message d’erreur s’affiche lorsque vous tentez de créer une ressource avec un titre déjà utilisé par une autre ressource. Les titres doivent être uniques pour tous les types de ressources. Par exemple, si vous essayez de créer un groupe de champs avec un titre déjà utilisé par un schéma, vous obtiendrez cette erreur.

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

Les ressources définies par votre organisation doivent doter leurs champs d’un espace de noms sous votre identifiant client afin d’éviter tout conflit avec d’autres ressources du secteur et de fournisseurs. Lors de la création d’un schéma à l’aide de groupes de champs standard, tous les champs personnalisés que vous ajoutez dans la structure de ces groupes de champs doivent également comporter un espace de noms sous votre identifiant client.

>[!NOTE]
>
>Selon la nature spécifique de l’erreur d’espace de noms, cette erreur peut utiliser l’une des URI `type` suivantes avec différents détails de message :
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

Vous trouverez des exemples détaillés de structures de données appropriées pour les ressources XDM dans le guide de l’API Schema Registry :

- [Créer une classe personnalisée](./api/classes.md#create)
- [Créer un groupe de champs personnalisé](./api/field-groups.md#create)
- [Créer un type de données personnalisé](./api/data-types.md#create)

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

Les requêtes GET dans l’API [!DNL Schema Registry] nécessitent un en-tête `Accept` pour que le système puisse déterminer le format de la réponse. Cette erreur se produit lorsqu’un en-tête `Accept` requis est non valide ou manquant.

Selon le point d’entrée que vous utilisez, la propriété `detailed-message` indique ce à quoi un en-tête `Accept` valide doit ressembler pour une réponse réussie. Assurez-vous d’avoir correctement saisi un en-tête `Accept` compatible avec la requête API que vous essayez de créer avant de réessayer.

>[!NOTE]
>
>Selon le point d’entrée utilisé, cette erreur peut utiliser l’une des URI `type` suivantes :
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

Pour obtenir la liste des en-têtes Accept compatibles pour les différentes requêtes API, veuillez vous référer aux sections correspondantes dans le [guide de développement du registre des schémas](./api/overview.md).

### Erreurs [!DNL Real-Time Customer Profile]

Les messages d’erreur suivants sont associés aux opérations impliquées dans l’activation des schémas de [!DNL Real-Time Customer Profile]. Pour plus d’informations, consultez la section sur les [unions](./api/unions.md) dans le guide de l’API [!DNL Schema Registry].

#### Il doit y avoir un descripteur d’identité de référence.

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

Ce message d’erreur s’affiche lorsque vous tentez d’activer un schéma pour [!DNL Profile] et qu’une de ses propriétés contient un descripteur de relation sans descripteur d’identité de référence. Ajoutez un descripteur d’identité de référence au champ de schéma en question pour résoudre cette erreur.

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

>[!NOTE]
>
>Pour cette erreur, le « schéma de destination » correspond au schéma de référence dans la relation.

Pour pouvoir activer des schémas contenant des descripteurs de relation à utiliser dans [!DNL Profile], l’espace de noms du champ source et l’espace de noms principal du champ de référence doivent être identiques. Ce message d’erreur s’affiche lorsque vous essayez d’activer un schéma qui contient un espace de noms incompatible avec son descripteur d’identité de référence.

Pour résoudre ce problème, il faut s’assurer que la valeur `xdm:namespace` du champ d’identité du schéma de référence correspond à celle de la propriété `xdm:identityNamespace` dans le descripteur d’identité de référence du champ source.

Pour obtenir une liste des codes d’espaces de noms d’identité standard, consultez la section sur les [espaces de noms standard](../identity-service/features/namespaces.md) dans la présentation des espaces de noms d’identité.

#### Le schéma doit inclure un identityMap ou une identité principale.

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

Avant d’activer un schéma pour Profile, vous devez d’abord [créer un descripteur d’identité principale](./api/descriptors.md#create) pour le schéma, ou inclure un champ de mappage d’identité pour qu’il agisse en tant qu’identité principale.

#### Impossible de fusionner les types de données incompatibles

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

Tous les schémas activés pour Profile appartenant à la même classe doivent pouvoir fusionner afin de construire le schéma d’union pour cette classe. Cette erreur s’affiche lorsque vous essayez d’ajouter un champ à un schéma dont le chemin est partagé par un autre schéma activé pour Profile et que le type de données est différent de celui de l’original. Comme les schémas sont activés pour Profile et qu’ils contiennent le même chemin de champ, Profile tente de fusionner ces deux champs en un seul lors de la création du schéma d’union. Comme les différents types de données ne peuvent pas être fusionnés, cela serait considéré comme un conflit de fusion, ce qui n’est pas autorisé.

Pour résoudre le problème, choisissez un autre nom pour le champ ou imbriquez-le sous un objet d’espace de noms unique afin d’éviter les conflits de fusion avec d’autres schémas activés pour Profile sous la même classe avec des champs similaires.

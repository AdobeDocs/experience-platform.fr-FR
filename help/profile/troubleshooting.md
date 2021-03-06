---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Guide de dépannage de Real-time Customer Profile
topic-legacy: guide
type: Documentation
description: Ce document fournit des réponses aux questions fréquentes sur Real-time Customer Profile, ainsi qu’un guide de dépannage pour les erreurs courantes lors de l’utilisation des données de profil à l’aide de Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 5%

---

# Guide de dépannage de Real-time Customer Profile

Ce document fournit des réponses aux questions fréquentes sur Real-time Customer Profile, ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

Le [!DNL Real-time Customer Profile] offre une vision holistique de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Cela permet aux marketeurs d’offrir aux clients des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes sur Real-time Customer Profile.

### Quels types de données sont acceptés pour Real-time Customer Profile ?

Profile accepte les données **record** et **de série temporelle**, à condition que les données en question contiennent au moins une valeur d’identité qui associe les données à une personne individuelle unique.

Comme tous les services Platform, Profile nécessite que ses données soient structurées sémantiquement sous un schéma de modèle de données d’expérience (XDM). En retour, une **identité Principale** doit être définie pour ce schéma et être activée pour une utilisation dans Profile.

Si vous ne connaissez pas XDM, commencez par la [présentation XDM](../xdm/home.md) pour en savoir plus. Voir ensuite le guide d’utilisation XDM pour savoir comment [définir des champs d’identité](../xdm/tutorials/create-schema-ui.md#identity-field) et [activer un schéma pour Profile](../xdm/tutorials/create-schema-ui.md#profile).

### Où les données de profil sont-elles stockées ?

Real-time Customer Profile conserve sa propre banque de données (appelée &quot;banque de profils&quot;), à l’écart du lac de données qui contient d’autres données Platform ingérées.

### Si j’ai déjà ingéré des données dans Platform, puis-je les rendre disponibles dans la banque de profils ?

Si des données ont été ingérées dans un jeu de données autre que Profile, vous devez ingérer à nouveau ces données dans un jeu de données activé par Profile afin de le rendre disponible dans la banque de données Profile. Il est possible d’activer un jeu de données existant pour Profile, mais toutes les données ingérées avant cette configuration n’apparaîtront toujours pas dans la banque de données Profile.

Si vous souhaitez ajouter des données précédemment ingérées à la banque de profils, suivez le [tutoriel sur la configuration du jeu de données](./tutorials/dataset-configuration.md) pour créer un jeu de données ou convertir un jeu de données existant à activer pour Profile, puis réinglez les données souhaitées dans ce jeu de données.

### Comment puis-je afficher mes données de profil ingérées ?

Il existe plusieurs méthodes d’affichage des données de profil, selon que vous utilisez l’API ou l’interface utilisateur.

#### Utilisation de l’API

Si vous connaissez les identifiants des entités de profil auxquelles vous souhaitez accéder, vous pouvez utiliser le point de terminaison `/entities` (Accès au profil) dans l’API Profile pour rechercher ces entités. Pour plus d’informations, reportez-vous à la section [entities](./api/entities.md) du guide de développement.

Vous pouvez également utiliser l’API Adobe Experience Platform Segmentation Service pour accéder aux profils individuels des clients qui sont qualifiés pour une adhésion à un segment. Pour plus d’informations, consultez la [présentation de Segmentation Service](../segmentation/home.md) .

#### Utilisation de l’interface utilisateur

Dans l’interface utilisateur de l’Experience Platform, l’onglet **[!UICONTROL Parcourir]** de l’espace de travail **[!UICONTROL Profils]** vous permet d’afficher le nombre total de profils et de rechercher des profils individuels en fonction de leur valeur d’identité. Pour plus d’informations, consultez le [guide d’utilisation du profil](./ui/user-guide.md) .

Vous pouvez également afficher une liste de vos segments sous l’onglet **[!UICONTROL Parcourir]** dans l’espace de travail **[!UICONTROL Segments]**. Après la sélection d’un segment, un exemple de profils qualifiés pour ce segment s’affiche. Vous pouvez ensuite sélectionner l’un de ces profils répertoriés pour en afficher les détails. Pour plus d’informations, consultez la [présentation de l’interface utilisateur de segmentation](../segmentation/ui/overview.md) .

## Codes d’erreur

Voici une liste des messages d’erreur que vous pouvez rencontrer lors de l’utilisation de l’API Real-time Customer Profile. Si l’erreur que vous rencontrez n’est pas répertoriée ici, vous pouvez la trouver dans le [Guide de dépannage de Platform](../landing/troubleshooting.md) général à la place.

### Impossible de rechercher le schéma de l’attribut calculé pour le chemin d’accès fourni

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Lors de la création d’un attribut calculé, cette erreur se produit lorsque le système n’a pas pu trouver le schéma fourni dans le payload de la requête. Assurez-vous que vous avez fourni l’ID de tenant correct dans la propriété `path` de la payload et que les valeurs de `schema.name` sont un nom de schéma valide.

Si vous ne connaissez pas votre ID de tenant, vous pouvez le récupérer en suivant les étapes du [guide de développement du registre des schémas](../xdm/api/getting-started.md).

### La fonction portant le même nom existe déjà pour le schéma spécifié ou definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Lors de la création d’un attribut calculé, cette erreur se produit lorsque la propriété `name` fournie est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Le schéma de retour de l’expression n’est pas identique au schéma de l’attribut calculé dans le schéma XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Lors de la création d’un attribut calculé, cette erreur se produit lorsque la propriété `name` fournie est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Requête de suppression non valide (Tâche du système de profil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Cette erreur se produit lorsqu’une charge utile non valide est fournie pour une tâche de suppression du système. Assurez-vous de fournir un jeu de données ou un identifiant de lot valide sous la propriété `dataSetID` ou `batchID` de la payload, respectivement. Pour plus d’informations, reportez-vous à la section [Création d’une requête de suppression](./api/profile-system-jobs.md#create-a-delete-request) du guide de développement de Profile.

### Lot introuvable pour le jeu de données de profil

```json
{
  "requestId":"LlTmQkhgHKFGHGHnIkmUxcIL4YTFSpQw",
  "errors":{
    "400":[
      {
        "code":"400",
        "message":"Batch not found for profile dataset '5da688d2c4e60518ad25b7b1'"
      }
    ]
  }
}
```

Cette erreur se produit lorsqu’un lot valide est introuvable lors de la tentative de création d’une requête de suppression pour les données de profil. Vérifiez que vous avez saisi l’identifiant correct pour un jeu de données activé par Profile avant de réessayer.

### La destination de projection n&#39;a pas encore été créée.

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Cette erreur se produit lorsque la requête `destinationId` fournie dans une requête `POST /config/projections` n’est pas valide. Vérifiez deux fois que vous avez fourni un ID de destination valide avant de réessayer. Pour créer une destination, suivez les étapes décrites dans le [Guide de développement de profil](./api/edge-projections.md#create-a-destination).

### Type de média non pris en charge

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Cette erreur se produit lors de l’envoi d’une demande de POST ou de PUT avec un en-tête Content-Type non valide. Vérifiez deux fois que vous fournissez une valeur Content-Type valide pour le point de terminaison que vous utilisez.

La plupart des points de terminaison Profile acceptent &quot;application/json&quot; pour leur en-tête Content-Type, avec les exceptions suivantes :

| Point d’entrée | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |

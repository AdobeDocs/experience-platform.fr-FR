---
keywords: Experience Platform ; profil ; profil client en temps réel ; dépannage ; API
title: Guide de dépannage du Profil client en temps réel
topic-legacy: guide
type: Documentation
description: Ce document fournit des réponses aux questions fréquentes sur le Profil client en temps réel, ainsi qu’un guide de dépannage pour les erreurs courantes lors de l’utilisation de données de Profil à l’aide de Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 3%

---

# Guide de dépannage de Real-time Customer Profile

Ce document fournit des réponses aux questions fréquentes sur le Profil client en temps réel, ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

[!DNL Real-time Customer Profile] permet de visualiser une vue holistique de chaque client en combinant des données provenant de plusieurs canaux, notamment en ligne, hors ligne, CRM et tiers. Cela permet aux spécialistes du marketing de proposer aux clients des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes sur le Profil client en temps réel.

### Quels types de données sont acceptés pour le Profil client en temps réel ?

Le profil accepte à la fois les données **record** et **séries chronologiques**, pour autant que les données en question contiennent au moins une valeur d&#39;identité qui associe les données à une personne unique.

Comme tous les services de plate-forme, le Profil exige que ses données soient structurées sémantiquement sous un schéma de modèle de données d’expérience (XDM). À son tour, ce schéma doit avoir une **identité Principale** définie et être activé pour utilisation dans le Profil.

Si XDM ne vous est pas familier, début avec l&#39;[aperçu XDM](../xdm/home.md) pour en savoir plus. Consultez ensuite le guide de l&#39;utilisateur XDM pour savoir comment [définir des champs d&#39;identité](../xdm/tutorials/create-schema-ui.md#identity-field) et [activer un schéma pour Profil](../xdm/tutorials/create-schema-ui.md#profile).

### Où les données de Profil sont-elles stockées ?

Le Profil client en temps réel conserve sa propre banque de données (appelée &quot;banque de Profils&quot;), distincte de Data Lake qui contient d’autres données de plateforme imbriquées.

### Si j&#39;ai déjà assimilé des données dans Platform, puis-je les rendre disponibles dans le magasin de Profils ?

Si des données ont été ingérées dans un jeu de données non Profil, vous devez réingérer ces données dans un jeu de données compatible Profil afin de les rendre disponibles dans le magasin de Profils. Il est possible d&#39;activer un jeu de données existant pour le Profil ; toutefois, les données ingérées avant cette configuration n&#39;apparaîtront toujours pas dans le Profil Store.

Si vous souhaitez ajouter des données précédemment ingérées au magasin de Profils, suivez le [didacticiel de configuration des jeux de données](./tutorials/dataset-configuration.md) pour créer un nouveau jeu de données ou convertir un jeu de données existant à activer pour le Profil, puis réingérer les données souhaitées dans ce jeu de données.

### Comment puis-je vue mes données de Profil imbriquées ?

Il existe plusieurs méthodes d’affichage des données de Profil, selon que vous utilisez l’API ou l’interface utilisateur.

#### Utilisation de l’API

Si vous connaissez les ID des entités de Profil auxquelles vous souhaitez accéder, vous pouvez utiliser le point de terminaison `/entities` (accès au Profil) dans l&#39;API de Profil pour rechercher ces entités. Pour plus d&#39;informations, consultez la section [entités](./api/entities.md) du guide du développeur.

Vous pouvez également utiliser l’API Adobe Experience Platform Segmentation Service pour accéder aux profils individuels des clients qui se sont qualifiés pour un abonnement de segment. Pour plus d&#39;informations, consultez la section [Présentation du service de segmentation](../segmentation/home.md).

#### Utilisation de l’interface utilisateur

Dans l’interface utilisateur de l’Experience Platform, l’onglet **[!UICONTROL Parcourir]** de l’espace de travail **[!UICONTROL Profils]** permet de vue du nombre total de profils et de rechercher des profils individuels en fonction de leur valeur d’identité. Pour plus d&#39;informations, consultez le [guide de l&#39;utilisateur du Profil](./ui/user-guide.md).

Vous pouvez également vue une liste de vos segments sous l&#39;onglet **[!UICONTROL Parcourir]** de l&#39;espace de travail **[!UICONTROL Segments]**. Après avoir sélectionné un segment, un exemple de profils qualifiés pour ce segment s’affiche. Vous pouvez ensuite sélectionner l’un de ces profils répertoriés pour en vue les détails. Pour plus d’informations, consultez la section [Présentation de l’interface utilisateur de segmentation](../segmentation/ui/overview.md).

## Codes d’erreur

Voici une liste de messages d’erreur que vous pouvez rencontrer lorsque vous utilisez l’API Profil client en temps réel. Si l&#39;erreur que vous rencontrez n&#39;est pas répertoriée ici, vous pouvez la trouver dans le guide général de dépannage de la [plate-forme](../landing/troubleshooting.md) à la place.

### Impossible de rechercher le schéma de l&#39;attribut calculé pour le chemin d&#39;accès fourni

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Lors de la création d’un attribut calculé, cette erreur se produit lorsque le système ne trouve pas le schéma fourni dans la charge utile de la demande. Vérifiez que vous avez fourni l’ID de client correct dans la propriété `path` de la charge utile et que les valeurs de `schema.name` sont un nom de schéma valide.

Si vous ne connaissez pas votre ID de client, vous pouvez le récupérer en suivant les étapes du [guide du développeur du registre de Schéma](../xdm/api/getting-started.md).

### Une fonction portant le même nom existe déjà pour le schéma spécifié ou definedOn.

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Lors de la création d&#39;un attribut calculé, cette erreur se produit lorsque la propriété `name` fournie est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Le schéma de retour de l&#39;expression n&#39;est pas identique au schéma de l&#39;attribut calculé dans le schéma XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Lors de la création d&#39;un attribut calculé, cette erreur se produit lorsque la propriété `name` fournie est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Demande de suppression non valide (tâche système de Profil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Cette erreur se produit lorsqu&#39;une charge utile non valide est fournie pour une tâche de suppression du système. Assurez-vous de fournir un jeu de données ou un ID de lot valide sous la propriété `dataSetID` ou `batchID` de la charge utile, respectivement. Pour plus d&#39;informations, consultez la section [création d&#39;une demande de suppression](./api/profile-system-jobs.md#create-a-delete-request) du guide du développeur de Profils.

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

Cette erreur se produit lorsqu&#39;un lot valide est introuvable lors de la tentative de création d&#39;une demande de suppression de données de Profil. Vérifiez que vous avez saisi l’ID correct pour un jeu de données compatible Profil avant de réessayer.

### La destination de projection n&#39;a pas encore été créée

```json
{
  "status":404,
  "title":"The projection destination has not yet been created.",
  "type":"http://ns.adobe.com/adobecloud/problem/missing-entity"
}
```

Cette erreur se produit lorsque la requête `destinationId` fournie dans une requête `POST /config/projections` n&#39;est pas valide. Vérifiez par doublon que vous avez fourni un ID de destination valide avant de réessayer. Pour créer une nouvelle destination, suivez les étapes décrites dans le [guide du développeur de Profils](./api/edge-projections.md#create-a-destination).

### Type de support non pris en charge

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Cette erreur se produit lors de l&#39;envoi d&#39;une demande de POST ou de PUT avec un en-tête Content-Type non valide. Vérifiez par doublon que vous fournissez une valeur Content-Type valide pour le point de terminaison que vous utilisez.

La plupart des points de terminaison de Profil acceptent &quot;application/json&quot; pour leur en-tête Content-Type, avec les exceptions suivantes :

| Point de terminaison | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |

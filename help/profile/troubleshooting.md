---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guide de dépannage de Real-time Customer Profile
topic: guide
translation-type: tm+mt
source-git-commit: 94fd6ee324b35acb7ef1185f7851d76d76f3e91c
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 9%

---


# Guide de dépannage de Real-time Customer Profile

Ce document fournit des réponses aux questions fréquentes sur le Profil client en temps réel, ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

Real-time Customer Profile est une banque d’entités de recherche générique qui fusionne les données de différentes ressources de données d’entreprise, puis fournit un accès à ces données sous la forme de profils client individuels et d’événements de série temporelle connexes. Cette fonctionnalité permet aux spécialistes marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions fréquentes sur le Profil client en temps réel.

### Quels types de données sont acceptés pour le Profil client en temps réel ?

Profil accepte à la fois les données **d’enregistrement** et les données de séries **** chronologiques, pour autant que les données en question contiennent au moins une valeur d’identité qui associe les données à une personne individuelle unique.

Comme tous les services Platform, le Profil exige que ses données soient structurées sémantiquement sous un schéma de modèle de données d’expérience (XDM). En retour, ce schéma doit avoir une identité **** principale définie et être activé pour une utilisation dans le Profil.

Si vous ne connaissez pas XDM, début de l&#39;aperçu [](../xdm/home.md) XDM pour en savoir plus. Ensuite, consultez le guide de l&#39;utilisateur XDM pour savoir comment [définir des champs](../xdm/tutorials/create-schema-ui.md#identity-field) d&#39;identité et [activer un schéma pour le Profil](../xdm/tutorials/create-schema-ui.md#profile).

### Où les données de Profil sont-elles stockées ?

Le Profil client en temps réel conserve sa propre banque de données (appelée &quot;banque de Profils&quot;), distincte de Data Lake qui contient d’autres données Platform ingérées.

### Si j&#39;ai déjà assimilé des données à Platform, puis-je les rendre disponibles dans le magasin de Profils ?

Si des données ont été ingérées dans un jeu de données non Profil, vous devez réingérer ces données dans un jeu de données compatible Profil afin de les rendre disponibles dans le magasin de Profils. Il est possible d&#39;activer un jeu de données existant pour le Profil ; toutefois, les données ingérées avant cette configuration n&#39;apparaîtront toujours pas dans le Profil Store.

Si vous souhaitez ajouter des données précédemment ingérées au magasin de Profils, suivez le didacticiel [de configuration du jeu de](./tutorials/dataset-configuration.md) données pour créer un nouveau jeu de données ou convertir un jeu de données existant à activer pour le Profil, puis réinglez les données de votre choix dans ce jeu de données.

### Comment puis-je vue mes données de Profil imbriquées ?

Il existe plusieurs méthodes d’affichage des données de Profil, selon que vous utilisez l’API ou l’interface utilisateur.

#### Utilisation de l’API

Si vous connaissez les ID des entités de Profil auxquelles vous voulez accéder, vous pouvez utiliser le point de terminaison `/entities` (accès au Profil) dans l&#39;API de Profil pour rechercher ces entités. Pour plus d&#39;informations, consultez la section sur [les entités](./api/entities.md) du guide du développeur.

Vous pouvez également utiliser l’API Adobe Experience Platform Segmentation Service pour accéder aux profils individuels des clients qui se sont qualifiés pour un abonnement de segment. See the [Segmentation Service overview](../segmentation/home.md) for more information.

#### Utilisation de l’interface utilisateur

Dans l’interface utilisateur de l’Experience Platform, l’onglet **[!UICONTROL Parcourir]** de l’espace de travail **[!UICONTROL Profils]** vous permet de vue du nombre total de profils et de rechercher des profils individuels en fonction de leur valeur d’identité. See the [Profile user guide](./ui/user-guide.md) for more information.

Vous pouvez également vue une liste de vos segments sous l’onglet **[!UICONTROL Parcourir]** de l’espace de travail **[!UICONTROL Segments]** . Après avoir sélectionné un segment, un exemple de profils qualifiés pour ce segment s’affiche. Vous pouvez ensuite sélectionner l’un de ces profils répertoriés pour en vue les détails. See the [Segmentation UI overview](../segmentation/ui/overview.md) for more information.

## Codes d’erreur

Voici une liste de messages d’erreur que vous pouvez rencontrer lorsque vous utilisez l’API Profil client en temps réel. Si l’erreur que vous rencontrez n’est pas répertoriée ici, vous pouvez la trouver dans le guide [général de dépannage de](../landing/troubleshooting.md) Platform à la place.

### Impossible de rechercher le schéma de l&#39;attribut calculé pour le chemin d&#39;accès fourni

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Lors de la création d’un attribut calculé, cette erreur se produit lorsque le système ne trouve pas le schéma fourni dans la charge utile de la demande. Assurez-vous que vous avez fourni l’ID de client correct dans la `path` propriété de la charge utile et que les valeurs de `schema.name` est un nom de schéma valide.

Si vous ne connaissez pas votre ID de client, vous pouvez le récupérer en suivant les étapes du guide [de développement du registre de](../xdm/api/getting-started.md)Schéma.

### Une fonction portant le même nom existe déjà pour le schéma spécifié ou definedOn.

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Lors de la création d’un nouvel attribut calculé, cette erreur se produit lorsque la `name` propriété fournie est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Le schéma de retour de l&#39;expression n&#39;est pas identique au schéma de l&#39;attribut calculé dans le schéma XDM

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Lors de la création d’un nouvel attribut calculé, cette erreur se produit lorsque la `name` propriété fournie est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Demande de suppression non valide (tâche système de Profil)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Cette erreur se produit lorsqu&#39;une charge utile non valide est fournie pour une tâche de suppression du système. Assurez-vous de fournir un jeu de données ou un ID de lot valide sous la propriété `dataSetID` ou la propriété `batchID` de la charge utile, respectivement. Pour plus d&#39;informations, consultez la section relative à la [création d&#39;une demande](./api/profile-system-jobs.md#create-a-delete-request) de suppression dans le guide du développeur de Profils.

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

Cette erreur se produit lorsque le `destinationId` contenu d’une `POST /config/projections` requête n’est pas valide. Vérifiez par Doublon que vous avez fourni un ID de destination valide avant de réessayer. Pour créer une nouvelle destination, suivez les étapes décrites dans le guide [des développeurs de](./api/edge-projections.md#create-a-destination)Profils.

### Type de support non pris en charge

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Cette erreur se produit lors de l&#39;envoi d&#39;une demande de POST ou de PUT avec un en-tête Content-Type non valide. Vérifiez par Doublon que vous fournissez une valeur Content-Type valide pour le point de terminaison que vous utilisez.

La plupart des points de terminaison de Profil acceptent &quot;application/json&quot; pour leur en-tête Content-Type, avec les exceptions suivantes :

| Point de terminaison | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |
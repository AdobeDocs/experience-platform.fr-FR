---
keywords: Experience Platform;profil;profil client en temps réel;dépannage;API
title: Guide de dépannage du profil client en temps réel
type: Documentation
description: Ce document fournit des réponses aux questions fréquentes sur le profil client en temps réel, ainsi qu’un guide de dépannage pour les erreurs courantes lors de l’utilisation des données de profil à l’aide d’Adobe Experience Platform.
exl-id: 0b340025-093b-41e4-8053-969a8e80e889
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 91%

---

# Guide de dépannage du profil client en temps réel

Ce document fournit des réponses aux questions fréquentes sur le profil client en temps réel, ainsi qu’un guide de dépannage pour les erreurs courantes. Pour toute question ou dépannage concernant les autres services d’Adobe Experience Platform, consultez le [guide de dépannage d’Experience Platform](../landing/troubleshooting.md).

[!DNL Real-Time Customer Profile] offre une vision holistique de chaque client en combinant des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Cette fonctionnalité permet aux professionnels du marketing d’offrir à leur audience des expériences coordonnées, cohérentes et pertinentes sur plusieurs canaux.

## FAQ

Vous trouverez ci-dessous une liste de réponses aux questions les plus fréquemment posées à propos du profil client en temps réel.

### Quels types de données sont acceptés pour le profil client en temps réel ?

Profile accepte aussi bien les données d’**enregistrement** que les données de **série temporelle**, tant que les données en question contiennent au moins une valeur d’identité qui les associe à une personne individuelle unique.

Comme tous les services Experience Platform, Profile nécessite que ses données soient structurées sémantiquement sous un schéma de modèle de données d’expérience (XDM). Ce schéma doit, à son tour, comporter une **identité principale** définie et activée pour une utilisation dans Profile.

Si vous ne connaissez pas XDM, commencez par consulter la [Présentation de XDM](../xdm/home.md) pour en savoir plus. Ensuite, consultez le guide d’utilisation XDM pour savoir comment [définir des champs d’identité](../xdm/tutorials/create-schema-ui.md#identity-field) et [activer un schéma pour Profile](../xdm/tutorials/create-schema-ui.md#profile).

### Où les données Profile sont-elles stockées ?

Le profil client en temps réel conserve sa propre banque de données (appelée « banque de profils ») à l’écart du lac de données qui contient d’autres données Experience Platform ingérées.

### Si j’ai déjà ingéré des données dans Experience Platform, puis-je les rendre disponibles dans la banque de profils ?

Si des données ont été ingérées dans un jeu de données non lié à Profile, vous devez ingérer à nouveau ces données dans un jeu de données activé pour Profile afin de le rendre disponible dans la banque de données de profils. Il est possible d’activer un jeu de données existant pour Profile, mais toutes les données ingérées avant cette configuration n’apparaîtront toujours pas dans la banque de profils.

Si vous souhaitez ajouter des données précédemment ingérées à la banque de profils, suivez le [tutoriel sur la configuration des jeux de données](./tutorials/dataset-configuration.md) pour créer un nouveau jeu de données ou convertir un jeu de données existant à activer pour Profile, puis ingérez à nouveau les données de votre choix dans ce jeu de données.

### Comment puis-je afficher mes données de profil ingérées ?

Il existe plusieurs façon d’afficher les données de Profile, selon que vous utilisez l’API ou l’interface utilisateur.

#### Utilisation de l’API

Si vous connaissez les identifiants des entités de profil auxquelles vous souhaitez accéder, vous pouvez utiliser le Point d’entrée `/entities` (Accès au profil) dans l’API Profile pour rechercher ces entités. Consultez la section sur les [entités](./api/entities.md) dans le guide de développement pour plus d’informations.

Vous pouvez également utiliser l’API Segmentation Service d’Adobe Experience Platform pour accéder aux profils individuels de la clientèle éligibles à l’appartenance à une audience. Pour plus d’informations, consultez la [présentation de Segmentation Service](../segmentation/home.md).

#### Utilisation de l’interface utilisateur

Dans l’interface utilisateur d’Experience Platform, l’onglet **[!UICONTROL Parcourir]** dans l’espace de travail **[!UICONTROL Profils]** vous permet d’afficher le nombre total de profils et de rechercher des profils individuels en fonction de leur valeur d’identité. Pour plus d’informations, consultez le [guide d’utilisation de Profile](./ui/user-guide.md).

Vous pouvez également afficher la liste de vos audiences sous l’onglet **[!UICONTROL Parcourir]** dans l’espace de travail **[!UICONTROL Audiences]**. Après avoir sélectionné une audience, un échantillon de profils éligibles à cette audience s’affiche. Vous pouvez ensuite sélectionner l’un des profils répertoriés pour en afficher les détails. Pour plus d’informations, consultez la [Présentation de l’interface utilisateur Segmentation](../segmentation/ui/overview.md),

## Codes d’erreur

Voici une liste des messages d’erreur que vous pouvez rencontrer lors de l’utilisation de l’API Real-Time Customer Profile. Si l&#39;erreur que vous rencontrez n&#39;est pas répertoriée ici, vous pouvez la trouver dans le [guide de dépannage d&#39;Experience Platform](../landing/troubleshooting.md).

### Impossible de rechercher le schéma de l’attribut calculé pour le chemin d’accès fourni

```json
{
  "code": "400",
  "message": "Could not lookup schema of the computed attribute for the provided path"
}
```

Lors de la création d’un nouvel attribut calculé, cette erreur se produit lorsque le système n’a pas pu trouver le schéma fourni dans la payload de la requête. Assurez-vous que vous avez fourni l’identifiant client correct dans les propriétés `path` de la payload et que les valeurs de `schema.name` sont des noms de schéma valides.

Si vous ne connaissez pas votre identifiant client, vous pouvez le récupérer en suivant les étapes présentées dans le [Guide de développement du registre des schémas](../xdm/api/getting-started.md).

### Une fonction portant le même nom existe déjà pour le schéma spécifié ou definedOn

```json
{
  "code": "400",
  "message": "Function with the same name already exists for the specified schema or definedOn"
}
```

Lors de la création d’un attribut calculé, cette erreur survient lorsque la propriété `name` donnée est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Le schéma de retour de l’expression n’est pas identique au schéma de l’attribut calculé dans le schéma XDM.

```json
{
  "code": "400",
  "message": "Return schema of the expression is not same as the schema of the computed attribute in the XDM schema"
}
```

Lors de la création d’un nouvel attribut calculé, cette erreur survient lorsque la propriété `name` donnée est déjà utilisée pour le schéma indiqué sous `schema.name`. Remplacez la valeur par un nom unique avant de réessayer.

### Requête de suppression non valide (Tâche système de Profile)

```json
{
  "code": "400",
  "message": "Invalid delete request (Profile System Job)"
}
```

Cette erreur se produit lorsqu’une payload non valide est fournie pour une tâche système de suppression. Assurez-vous de fournir un jeu de données ou un identifiant de lot valide sous la propriété `dataSetID` ou `batchID` de la payload. Pour plus d’informations, consultez la section sur la [création d’une requête de suppression](./api/profile-system-jobs.md#create-a-delete-request) dans le guide de développement de Profile.

### Lot introuvable pour le jeu de données du profil

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

Cette erreur se produit lorsqu’un lot valide est introuvable lors de la tentative de création d’une requête de suppression pour les données de Profile. Vérifiez que vous avez saisi l’identifiant correct pour un jeu de données activé pour Profile avant de réessayer.

### Type de média non pris en charge

```json
{
  "status": 415,
  "title": "HTTP 415 Unsupported Media Type",
  "type": "http://ns.adobe.com/adobecloud/problem/unsupported-media-type"
}
```

Cette erreur se produit lors de l’envoi d’une requête POST ou PUT avec un en-tête Type de contenu non valide. Vérifiez bien que vous fournissez une valeur Type de contenu valide pour le point d’entrée que vous utilisez.

La plupart des points d’entrée de Profile acceptent « application/json » pour leur en-tête Type de contenu, avec les exceptions suivantes :

| Point d’entrée | Content-Type |
| --- | --- |
| `/config/projections` | application/vnd.adobe.platform.projectionConfig+json; version=1 |
| `/config/destinations` | application/vnd.adobe.platform.projectionDestination+json; version=1 |

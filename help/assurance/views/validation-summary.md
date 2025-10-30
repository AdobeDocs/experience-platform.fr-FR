---
title: Affichage de l’éditeur de validation
description: Ce guide détaille les informations sur la vue Éditeur de validation dans Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 5%

---

# Vue de l’éditeur de validation

L’éditeur de validation vous permet de gérer rapidement et facilement les fonctions JavaScript pour valider les événements dans une session Adobe Experience Platform Assurance. Chaque fonction reçoit les événements d’une session Assurance. Vous pouvez écrire des fonctions pour valider la configuration du client, les conditions d’événement, les tests et les cas d’utilisation.

## Prise en main de l’éditeur de validation

Après [configuration d’Assurance](../tutorials/implement-assurance.md), dans la vue **[!UICONTROL Home]**, sélectionnez **[!UICONTROL Validation Editor]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Écrire une fonction de validation

Cette fonctionnalité vous permet de créer, modifier ou supprimer des fonctions de validation pour vos sessions Adobe Experience Platform Assurance.

1. Sélectionnez **[!UICONTROL Create a New Validation]**.
2. Saisissez un **nom** pour identifier la validation, puis fournissez un **catégorie** et une **description**.
3. Modifiez le code dans l’éditeur pour valider les événements de votre session Assurance.

Une fois les tests de fonction terminés, sélectionnez **[!UICONTROL Publish]** pour enregistrer votre validation.

### Définition de l’événement

| Clé | Type | Description |
| :--- | :--- | :--- |
| `uuid` | Chaîne | Identifiant universel unique de l’événement. |
| `timestamp` | Nombre | Date et heure du client lorsque l’événement a été envoyé à Assurance. |
| `eventNumber` | Nombre | Utilisé pour commander lorsque l’événement a été envoyé. Cette clé est utile lorsque les événements ont le même horodatage. |
| `vendor` | Chaîne | Chaîne d’identification du fournisseur au format de nom de domaine inverse (par exemple, com.adobe.assurance). |
| `type` | Chaîne | Utilisé pour indiquer le type d’événement. |
| `payload` | Objet | Définit les données de l’événement et contient des propriétés uniques et communes. Certaines propriétés courantes incluent `ACPExtensionEventSource` et `ACPExtensionEventType`. |
| `annotations` | Tableau | Tableau d’objets d’annotation. |

### Définition de l’annotation

| Clé | Type | Description |
| :--- | :--- | :--- |
| `uuid` | Chaîne | Identifiant universel unique de l’annotation. |
| `type` | Chaîne | Utilisé pour indiquer le type d’annotation, il s’agit généralement du nom du module externe (par exemple, Analytics). |
| `payload` | Objet | Définit les données qui doivent compléter l’événement. Pour Adobe Analytics, c’est là que se trouvent les données d’accès post-traitées. |

### Résultats de la validation

La fonction de validation doit renvoyer un objet contenant les éléments suivants :

| Clé | Type | Description |
| :--- | :--- | :--- |
| `message` | Chaîne | Message de validation à afficher dans le résumé des résultats. |
| `events` | Tableau | Tableau d’UUID d’événement à signaler comme correspondants ou non correspondants. |
| `links` | Tableau | Tableau d’objets `ValidationResultLink` à référencer dans la documentation et d’autres ressources `{( type: 'doc'`&vert;`'product', url: String )}` |
| `result` | Chaîne | Il s’agit du résultat de la validation qui doit être l’une des chaînes énumérées : « correspondant », « non correspondant », « inconnu » |

## Afficher les résultats de la validation

Les résultats de la fonction s’affichent dans la section des résultats située sous l’éditeur de code. Si le résultat de la validation est `unknown` ou `not matched` et que le tableau `events` comporte un ou plusieurs `uuids`, les événements sont mis en surbrillance dans la chronologie avec les couleurs suivantes :

* Vert - correspondant
* Orange - inconnu
* Rouge - sans correspondance

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Résolution des problèmes

Vous pouvez ajouter des `console.log()` dans votre fonction pour imprimer des éléments dans la Developer Console. Vous pouvez également utiliser la propriété message de l’objet de résultat pour déboguer les messages dans le panneau des résultats.

Si une erreur se produit dans l’éditeur de code JavaScript, un statut d’erreur et la raison s’affichent.

Pour en savoir plus sur les validations, rendez-vous sur le site GitHub [Validations Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins). Vous y trouverez des exemples de validations détenues par Adobe. Voir le [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) pour des descriptions plus détaillées des validations.

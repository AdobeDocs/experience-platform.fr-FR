---
title: Vue de l’éditeur de validation
description: Ce guide contient des informations détaillées sur la vue Éditeur de validation dans Adobe Experience Platform Assurance.
exl-id: 09be531c-8dc3-48b8-814f-b7a06adf1da3
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 4%

---

# Vue de l’éditeur de validation

L’éditeur de validation vous permet de gérer rapidement et facilement les fonctions JavaScript pour valider les événements dans une session Adobe Experience Platform Assurance. Chaque fonction reçoit les événements dans une session d’assurance. Vous pouvez créer des fonctions pour valider la configuration client, les conditions d’événement, les tests et les cas d’utilisation.

## Prise en main de l’éditeur de validation

Après avoir [configuré Assurance](../tutorials/implement-assurance.md), dans la vue **[!UICONTROL Accueil]**, sélectionnez **[!UICONTROL Éditeur de validation]**.

![Validation-Editor-Screen-Shot](https://user-images.githubusercontent.com/6597105/198680074-f548a646-6f2f-4a65-82fd-0f1687d869bf.png)

## Écrire une fonction de validation

Cette fonctionnalité vous permet de créer, de modifier ou de supprimer des fonctions de validation pour vos sessions Adobe Experience Platform Assurance.

1. Sélectionnez **[!UICONTROL Créer une validation]**.
2. Saisissez un **nom** pour identifier la validation, puis fournissez une **catégorie** et une **description**.
3. Modifiez le code de l’éditeur pour valider les événements de votre session d’assurance.

Une fois les tests de fonction terminés, sélectionnez **[!UICONTROL Publish]** pour enregistrer votre validation.

### Définition d’un événement

| Clé | Type | Description |
| :--- | :--- | :--- |
| `uuid` | Chaîne | Identifiant unique universel pour l’événement. |
| `timestamp` | Nombre | Horodatage du client lorsque l’événement a été envoyé à Assurance. |
| `eventNumber` | Nombre | Utilisé pour classer lorsque l’événement a été envoyé. Cette clé est utile lorsque les événements ont le même horodatage. |
| `vendor` | Chaîne | Chaîne d’identification du fournisseur au format de nom de domaine inverse (par exemple, com.adobe.assurance). |
| `type` | Chaîne | Utilisé pour indiquer le type d’événement. |
| `payload` | Objet | Définit les données de l’événement et contient des propriétés uniques et communes. Certaines propriétés courantes sont `ACPExtensionEventSource` et `ACPExtensionEventType`. |
| `annotations` | Tableau | Tableau d’objets d’annotation. |

### Définition d’annotation

| Clé | Type | Description |
| :--- | :--- | :--- |
| `uuid` | Chaîne | Identifiant unique universel de l’annotation. |
| `type` | Chaîne | Utilisé pour indiquer le type d’annotation et correspond généralement au nom du module externe (par exemple, analytics). |
| `payload` | Objet | Définit les données qui doivent compléter l’événement. Pour Adobe Analytics, il s’agit de l’emplacement où les données de l’accès post-traitement sont contenues. |

### Résultats de la validation

La fonction de validation doit renvoyer un objet contenant les éléments suivants :

| Clé | Type | Description |
| :--- | :--- | :--- |
| `message` | Chaîne | Message de validation à afficher dans les résultats du résumé. |
| `events` | Tableau | Un tableau d’événements à signaler comme correspondant ou non. |
| `links` | Tableau | Un tableau d’objets `ValidationResultLink` pour référencer la documentation et d’autres ressources `{( type: 'doc'|'product', url: String )}` |
| `result` | Chaîne | Il s’agit du résultat de la validation et il doit s’agir de l’une des chaînes énumérées : &quot;correspondance&quot;, &quot;sans correspondance&quot;, &quot;inconnue&quot;. |

## Affichage des résultats de la validation

Les résultats de la fonction sont affichés dans la section des résultats située sous l’éditeur de code. Si le résultat de la validation est `unknown` ou `not matched` et que le tableau `events` comporte un ou plusieurs `uuids`, les événements sont mis en surbrillance dans la chronologie avec les couleurs suivantes :

* Vert - Correspondant
* Orange - inconnu
* Rouge - sans correspondance

![Timeling-Validation-Highlights-Screen-Shot](https://user-images.githubusercontent.com/6597105/198681412-93d10a5a-3212-4e85-850a-aeaf5caf0521.png)

## Dépannage

Vous pouvez ajouter `console.log()` dans votre fonction pour imprimer des éléments sur la console de développement. Vous pouvez également utiliser la propriété message de l’objet result pour déboguer les messages dans le panneau des résultats.

Si une erreur se produit dans l’éditeur de code de JavaScript, un état d’erreur s’affiche avec la raison.

Pour en savoir plus sur les validations, consultez la page [Validations Adobe Experience Platform Assurance](https://github.com/adobe/griffon-validation-plugins) GitHub. Vous y trouverez des exemples de validations détenues par Adobe. Consultez le [wiki](https://github.com/adobe/griffon-validation-plugins/wiki) pour obtenir des descriptions plus détaillées des validations.

---
title: Suppression de ressources
description: Découvrez comment supprimer des ressources de balises dans Adobe Experience Platform.
exl-id: c8e26720-1976-48ec-8490-3d4ce587831e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 93%

---

# Suppression de ressources

La suppression d’une ressource entraîne la suppression définitive de cette ressource dans Adobe Experience Platform. Si vous souhaitez supprimer une ressource d’une bibliothèque de balises spécifique tout en souhaitant que cette ressource puisse être utilisée dans d’autres bibliothèques, consultez le guide sur la [suppression de ressources d’une bibliothèque](remove-resources-from-library.md).

Vous pouvez supprimer des éléments de données, des règles, des extensions, des hôtes, des environnements et des propriétés. Une fois supprimées, il n’est pas possible de récupérer ces ressources.

Les ressources qui sont ajoutées aux bibliothèques (éléments de données, règles et extensions) revêtent des considérations spéciales lorsque vous les supprimez.

## Préparer la suppression d’une ressource

Les ressources existent dans différents états et elles dépendent les unes des autres. Avant de supprimer une ressource, vous devez vous assurer qu’elle est dans un état lui permettant d’être supprimée.

La préparation de la suppression d’une ressource comprend deux étapes de base :

1. Résoudre les dépendances
1. Supprimer des bibliothèques

### Résoudre les dépendances

Les règles, les éléments de données et les extensions sont interdépendants. Par conséquent, la plupart du temps, lorsque vous en supprimez un, il existe un effet domino et vous avez alors d’autres éléments à supprimer.

#### Règles

Les règles dépendent d’autres ressources (extensions et éléments de données), mais elles ne contiennent aucune ressource qui en dépend. La suppression d’une règle implique que vous ne pouvez plus l’utiliser dans une bibliothèque ou même l’afficher, mais vous n’aurez aucune dépendance à supprimer ultérieurement.

#### Éléments de données

Les éléments de données dépendent des extensions. Cependant, contrairement aux règles, les éléments de données peuvent comporter des règles et des extensions qui dépendent d’eux. Si vous supprimez un élément de données, toutes les règles ou extensions qui en dépendent seront affectées.

Après suppression, l’élément de données ne renvoie plus la valeur correcte au moment de l’exécution. Il renvoie alors soit une chaîne vide, soit le nom de l’élément de données supprimé encapsulé dans %% (par exemple : `%data-element-name%`). Il est possible de configurer ce comportement dans Property Settings (Paramètres de propriété).

Vous pouvez résoudre ces dépendances avant ou après la suppression de l’élément de données.

#### Extensions

Toutes les autres ressources (règles, composants de règles et éléments de données) sont fournies par des extensions.

Le comportement des composants de règles et des éléments de données dépend d’extensions, et c’est également le cas pour leur affichage dans l’interface utilisateur de collecte de données. Si vous supprimez l’extension avant de résoudre les dépendances, vous ne pourrez plus afficher ces ressources orphelines. Ces ressources orphelines apparaissent dans les vues Liste, mais vous recevrez une erreur si vous essayez d’ouvrir la vue détaillée.

C’est pourquoi vous devez faire particulièrement attention lorsque vous supprimez des extensions et résoudre les dépendances avant de les supprimer.

### Supprimer des bibliothèques

Avant de pouvoir supprimer une ressource, vous devez la supprimer des bibliothèques qui la contiennent. Ce processus diffère selon l’état de la bibliothèque.

#### Développement

1. Ouvrez la bibliothèque.
1. Supprimez la ressource.
1. Enregistrez la bibliothèque.
1. Supprimez la ressource.

#### Envoyé ou approuvé

1. Rejetez la bibliothèque (la renvoyer vers Développement).
1. Suivez les étapes ci-dessus pour supprimer une ressource d’une bibliothèque de développement.

#### Production

1. Désactivez la ressource.
1. Publiez la ressource désactivée jusqu’à Production.
1. Supprimez la ressource.

## Supprimer une ressource

Dans la vue Liste appropriée, sélectionnez la ressource à supprimer, puis cliquez sur **[!UICONTROL Delete]**.

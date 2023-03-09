---
keywords: Experience Platform;accueil;rubriques les plus consultées;balises administratives;balises
title: Présentation des balises d’administration
description: Ce document fournit des informations sur les balises administratives dans Adobe Experience Platform
source-git-commit: f184e94350a79936cbbd9072791650af99fa945f
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# Présentation des balises

Les balises sont une fonctionnalité de Adobe Experience Platform qui permet aux administrateurs de gérer les taxonomies de métadonnées afin de classer les objets commerciaux pour une découverte et une catégorisation plus simples. Les balises sont des métadonnées qui peuvent être considérées comme des mots-clés pouvant être jointes à un segment, un jeu de données, un parcours ou d’autres objets pour permettre aux recherches de trouver cet objet et les objets associés. Les balises sont classées en deux types : catégorisés et non classés.

Pour fournir plus de contexte et définir l’objectif d’une balise, les catégories organisent les balises en ensembles utiles. Un administrateur définit les balises classées que les utilisateurs peuvent ajouter aux objets. De nouvelles balises qui ne contiennent pas de catégories peuvent également être créées en ligne dans les workflows où des balises sont appliquées. Ces balises s’affichent dans la section non classée de l’inventaire des balises. Les balises peuvent être appliquées par les administrateurs et les utilisateurs, quelle que soit la personne qui les a créées. Tous les types de balises peuvent être sélectionnés lors de l’affectation à un objet, d’une recherche ou d’un filtrage.

## Terminologie des balises

Le balisage implique les composants suivants :

| Terminologie | Définition |
| --- | --- |
| Archivé | État d’une balise qui conserve les associations actuelles avec les objets mais qui limite l’application de la balise à d’autres objets.  Les balises archivées sont masquées dans le sélecteur de balises. |
| Objet | Élément Experience Cloud auquel une balise peut être appliquée.  Exemples : Segment, Parcours, jeu de données. |
| Balises | Les balises sont des métadonnées et peuvent être considérées comme des mots-clés qui peuvent être joints à un segment, un jeu de données, un parcours ou d’autres objets pour permettre aux recherches de trouver cet objet et les objets associés. |
| Catégorie de balise | Les catégories de balises regroupent les balises dans des ensembles significatifs afin de fournir un plus grand contexte ou de décrire l’objectif de la balise.  Les administrateurs gèrent les catégories de balises et les balises au sein des catégories. |
| Balise non classée | Une nouvelle balise créée en ligne où les balises sont appliquées. Ces balises peuvent être créées et appliquées par n’importe quel utilisateur, mais elles ne sont pas liées à une catégorie.  Les administrateurs peuvent déplacer ces balises vers une catégorie afin de s’aligner sur d’autres balises similaires. |

## Inventaire des balises

La gestion des balises et des catégories à l’aide de l’inventaire des balises est disponible dans la navigation de l’Experience Platform et de Journey Optimizer. Les modifications apportées aux balises de l’inventaire sont répercutées dans tous les objets qui prennent en charge les balises. Tous les utilisateurs peuvent accéder à l’inventaire des balises et le parcourir, mais la gestion des balises se limite aux administrateurs système et produit.

L’inventaire des balises comporte trois niveaux de hiérarchie, ce qui permet aux utilisateurs de gérer les catégories de balises, les balises d’une catégorie et les balises individuelles. Lors de la gestion d’une balise individuelle, les utilisateurs peuvent afficher et accéder à n’importe quel objet auquel cette balise est actuellement appliquée.

### Catégories de balises

Les catégories regroupent les balises dans des ensembles significatifs afin de fournir un plus grand contexte ou de décrire l’objectif de la balise. Sur toute balise comportant une catégorie, le nom de la catégorie suivi d’un signe deux-points précède le nom de la balise.

Les actions suivantes sont possibles lors de l’utilisation de catégories de balises :

* [Créer une catégorie de balise](./ui/tags-categories.md#create-tag-category)
* [Modifier la catégorie de balise](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Supprimer une catégorie de balise](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Gestion des balises dans une catégorie

>[!NOTE]
>
>Pour gérer les balises d’Experience Cloud, vous devez être un administrateur système ou un administrateur de produit pour Adobe Experience Platform pour votre entreprise, qui s’abonne à Experience Cloud.

Dans une catégorie (ou le groupe &quot;Non classé&quot; par défaut), vous pouvez créer et gérer des balises. Les actions suivantes sont possibles lors de la gestion des balises :

* [Création d&#39;une balise](./ui/managing-tags.md#create-a-tag-create-tag)
* [Modification d’une balise](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Déplacer une balise entre des catégories](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archivage d’une balise](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Restaurer une balise archivée](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Suppression d’une balise](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Affichage des objets balisés](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)

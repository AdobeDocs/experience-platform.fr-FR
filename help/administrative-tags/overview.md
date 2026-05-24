---
keywords: Experience Platform;accueil;rubriques les plus consultées;balises unifiées;balises;
title: Présentation des balises unifiées
description: Ce document est consacré aux balises unifiées dans Adobe Experience Platform.
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
TQID: https://experienceleague.adobe.com/1frhbFeXBd9yoDeo42vdtAHRmH9l-uvbnvPG-xgDf1w
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 580
ht-degree: 98%

---

# Présentation des balises unifiées

Les balises sont une fonctionnalité d’Adobe Experience Platform qui permet à l’administration de gérer les taxonomies de métadonnées et de classer les objets d’entreprise pour une découverte et un classement plus simples. Pensez aux balises comme à des mots-clés : associez-les à un segment, un jeu de données, un parcours, etc. pour identifier ces objets. Vous pourrez ensuite rechercher cet objet et les objets associés grâce à leur balise. Il existe deux catégories de balises : classées et non classées.

Pour offrir plus de contexte et définir la finalité d’une balise, les catégories classent les balises en jeux utiles. L’administration définit les balises classées que les utilisateurs et utilisatrices peuvent ajouter aux objets. De nouvelles balises n’appartenant à aucune catégorie peuvent également être créées en ligne dans les workflows où des balises sont appliquées. Ces balises s’affichent dans la section non classée de l’inventaire des balises. L’administration, les utilisateurs et les utilisatrices peuvent tous appliquer les balises, quelle que soit la personne qui les a créées. Lors de l’affectation d’une balise à un objet, d’une recherche ou d’un filtrage, tous les types de balises sont disponibles.

## Terminologie propre aux balises

Le balisage implique les composants suivants :

| Terminologie | Définition |
| --- | --- |
| Archivé | État d’une balise qui conserve les associations actuelles avec les objets mais qui limite l’application de la balise à d’autres objets.  Les balises archivées sont masquées dans le sélecteur de balises. |
| Objet | Élément Experience Cloud auquel une balise peut être appliquée.  Exemples : segment, parcours, jeu de données. |
| Balise | Les balises sont des métadonnées et peuvent être considérées comme des mots-clés qui peuvent être rattachés à un segment, un jeu de données, un parcours ou d’autres objets pour permettre aux recherches de trouver cet objet et les objets associés. |
| Catégorie de balises | Les catégories de balises regroupent les balises dans des jeux significatifs pour fournir un plus grand contexte ou décrire la finalité de la balise.  Les administrateurs et administratrices gèrent les catégories de balises et les balises dans des catégories. |
| Balise non classée | Une nouvelle balise créée en ligne où les balises sont appliquées. Ces balises peuvent être créées et appliquées par n’importe quel utilisateur ou utilisatrice, mais elles ne sont pas liées à une catégorie.  Les administrateurs et administratrices peuvent déplacer ces balises vers une catégorie afin de s’aligner sur d’autres balises similaires. |

## Inventaire des balises

La gestion des balises et des catégories de balises à l’aide de l’inventaire des balises est disponible dans la navigation d’Experience Platform et de Journey Optimizer. Les modifications apportées aux balises de l’inventaire sont répercutées dans tous les objets qui prennent en charge les balises. Tous les utilisateurs et utilisatrices peuvent accéder à l’inventaire des balises et le parcourir, mais seuls les administrateurs et administraices système et produit sont responsables de la gestion des balises.

L’inventaire des balises comporte trois niveaux de hiérarchie, ce qui permet aux utilisateurs et utilisatrices de gérer les catégories de balises, les balises d’une catégorie et les balises individuelles. Lors de la gestion d’une balise individuelle, les utilisateurs et utilisatrices peuvent afficher et accéder à n’importe quel objet auquel cette balise est actuellement appliquée.

### Catégories de balises

Les catégories regroupent les balises dans des jeux significatifs afin de fournir un plus grand contexte ou de décrire la finalité de la balise. Sur toute balise appartenant à une catégorie, le nom de la catégorie suivi du signe deux-points précède le nom de la balise.

Les actions suivantes sont possibles lors de l’utilisation de catégories de balises :

* [Créer une catégorie de balises](./ui/tags-categories.md#create-tag-category)
* [Modifier la catégorie de balises](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Supprimer une catégorie de balises](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Gérer les balises d’une catégorie

>[!NOTE]
>
>Pour gérer les balises d’Experience Cloud, vous devez être administrateur ou administratrice système ou produit d’Adobe Experience Platform pour votre organisation abonnée à Experience Cloud.

Dans une catégorie (ou le groupe « Non classé » par défaut), vous pouvez créer et gérer des balises. Les actions suivantes sont possibles lors de la gestion des balises :

* [Créer une balise](./ui/managing-tags.md#create-a-tag-create-tag)
* [Modifier une balise](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Déplacer une balise entre catégories](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Archiver une balise](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Restaurer une balise archivée](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Supprimer une balise](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Afficher les objets balisés](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)

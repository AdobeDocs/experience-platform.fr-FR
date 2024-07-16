---
title: Informations personnalisables pour la création de rapports d’applications étendues
description: Découvrez comment utiliser des requêtes SQL pour générer des informations pour vos tableaux de bord personnalisés.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 2%

---

# Informations personnalisables pour la création de rapports d’application étendue

Utilisez des requêtes SQL personnalisées pour extraire efficacement des informations à partir de différents jeux de données structurés. Les utilisateurs techniques peuvent utiliser le mode Requête pour effectuer des analyses complexes avec SQL, puis partager cette analyse avec des utilisateurs non techniques par le biais de graphiques sur votre tableau de bord personnalisé ou les exporter dans des fichiers CSV. Cette méthode de création d’informations est bien adaptée aux tableaux avec des relations claires et permet une plus grande personnalisation dans vos insights et filtres qui peuvent s’adapter à des cas d’utilisation de niche.

>[!IMPORTANT]
>
>Le mode Requête pro n’est disponible que pour les utilisateurs qui ont acheté le [SKU de Distiller de données](../../../query-service/data-distiller/overview.md).

Pour générer des informations à partir de SQL, vous devez d’abord créer un tableau de bord.

## Création d’un tableau de bord personnalisé {#create-custom-dashboard}

Pour créer un tableau de bord personnalisé, sélectionnez **[!UICONTROL Tableaux de bord]** dans le panneau de navigation de gauche pour ouvrir l’espace de travail Tableaux de bord . Sélectionnez ensuite **[!UICONTROL Créer un tableau de bord]**.

![Inventaire du tableau de bord avec l’option Créer un tableau de bord mise en surbrillance.](../../images/customizable-insights/create-dashboard.png)

La boîte de dialogue **[!UICONTROL Créer un tableau de bord]** s’affiche. Deux options permettent de choisir la méthode de création de votre tableau de bord. Pour créer vos insights, vous pouvez utiliser un modèle de données existant avec le [[!UICONTROL mode de conception guidée]](../../user-defined-dashboards.md) ou votre propre code SQL avec le [!UICONTROL mode de requête pro].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

L’utilisation d’un modèle de données existant présente les avantages de fournir une structure structurée, efficace et évolutive adaptée aux besoins spécifiques de votre entreprise. Pour savoir comment [créer des insights à partir d’un modèle de données existant](../../user-defined-dashboards.md#create-widget), consultez le guide personnalisé du tableau de bord.

Les statistiques générées à partir des requêtes SQL offrent une flexibilité et une personnalisation bien plus grandes. Les techniciens peuvent utiliser le mode Requête pour effectuer une analyse complexe sur SQL, puis partager cette analyse avec des utilisateurs non techniques grâce à cette fonctionnalité de tableau de bord. Sélectionnez **[!UICONTROL Query Pro mode]** suivi de **[!UICONTROL Save]**.

>[!NOTE]
>
>Une fois la sélection effectuée, vous ne pouvez pas la modifier dans ce tableau de bord. Vous devez créer un tableau de bord avec une méthode de création de tableau de bord différente.

![ La boîte de dialogue [!UICONTROL Créer un tableau de bord] avec le mode pro Requête et l’option Enregistrer en surbrillance.](../../images/customizable-insights/query-pro-mode.png)

## Création d’un graphique {#create-a-chart}

Pour obtenir des instructions détaillées sur la création d’un graphique avec SQL, reportez-vous au [guide de requête en mode pro](./query-pro-mode.md).

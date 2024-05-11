---
title: Informations personnalisables pour la création de rapports d’applications étendues
description: Découvrez comment utiliser des requêtes SQL pour générer des informations pour vos tableaux de bord personnalisés.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Informations personnalisables pour la création de rapports d’application étendue

Utilisez des requêtes SQL personnalisées pour extraire efficacement des informations à partir de différents jeux de données structurés. Les utilisateurs techniques peuvent utiliser le mode Requête pour effectuer des analyses complexes avec SQL, puis partager cette analyse avec des utilisateurs non techniques par le biais de graphiques sur votre tableau de bord personnalisé ou les exporter dans des fichiers CSV. Cette méthode de création d’informations est bien adaptée aux tableaux avec des relations claires et permet une plus grande personnalisation dans vos insights et filtres qui peuvent s’adapter à des cas d’utilisation de niche.

>[!IMPORTANT]
>
>Le mode Requête pro n’est disponible que pour les utilisateurs qui ont acheté le [SKU Distiller des données](../../../query-service/data-distiller/overview.md).

Pour générer des informations à partir de SQL, vous devez d’abord créer un tableau de bord.

## Création d’un tableau de bord personnalisé {#create-custom-dashboard}

Pour créer un tableau de bord personnalisé, sélectionnez **[!UICONTROL Tableaux de bord]** dans le panneau de navigation de gauche pour ouvrir l’espace de travail Tableaux de bord . Ensuite, sélectionnez **[!UICONTROL Créer un tableau de bord]**.

![L’inventaire des tableaux de bord avec l’option Créer un tableau de bord est mis en surbrillance.](../../images/customizable-insights/create-dashboard.png)

La variable **[!UICONTROL Créer un tableau de bord]** s’affiche. Deux options permettent de choisir la méthode de création de votre tableau de bord. Pour créer vos insights, vous pouvez utiliser un modèle de données existant avec la variable [[!UICONTROL Mode de conception guidée]](../../user-defined-dashboards.md) ou votre propre code SQL avec la fonction [!UICONTROL Mode Requête pro].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

L’utilisation d’un modèle de données existant présente les avantages de fournir une structure structurée, efficace et évolutive adaptée aux besoins spécifiques de votre entreprise. Pour apprendre à [créer des insights à partir d’un modèle de données existant ;](../../user-defined-dashboards.md#create-widget), reportez-vous au guide personnalisé du tableau de bord.

Les statistiques générées à partir des requêtes SQL offrent une flexibilité et une personnalisation bien plus grandes. Les techniciens peuvent utiliser le mode Requête pour effectuer une analyse complexe sur SQL, puis partager cette analyse avec des utilisateurs non techniques grâce à cette fonctionnalité de tableau de bord. Sélectionner **[!UICONTROL Mode Requête pro]** suivie de **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Une fois la sélection effectuée, vous ne pouvez pas la modifier dans ce tableau de bord. Vous devez créer un tableau de bord avec une méthode de création de tableau de bord différente.

![La variable [!UICONTROL Créer un tableau de bord] Boîte de dialogue avec le mode Query Pro et Enregistrer en surbrillance.](../../images/customizable-insights/query-pro-mode.png)

## Création d’un graphique {#create-a-chart}

Voir [guide du mode query pro](./query-pro-mode.md) pour obtenir des instructions détaillées sur la création d’un graphique avec SQL.

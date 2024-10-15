---
title: En savoir plus
description: Découvrez les différentes options d'affichage pour vos données analysées par SQL. Depuis votre tableau de bord personnalisé, vous pouvez afficher les résultats tabulés de votre analyse ou télécharger les données traitées au format CSV.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Afficher plus {#view-more}

Une fois que vous avez créé un [aperçu personnalisé](./overview.md) avec le [ mode de requête pro ](./overview.md#query-pro-mode), vous pouvez afficher vos données de graphique dans différents formats. Vous pouvez afficher une forme de tableau des résultats ou télécharger les données sous la forme d’un fichier CSV à afficher dans une feuille de calcul.

## Résultats tabulés {#tabulated-results}

Pour chaque graphique créé en mode de requête pro via SQL, vous pouvez visualiser les résultats tabulés de votre analyse dans l’interface utilisateur de l’Experience Platform.

Dans votre tableau de bord personnalisé, sélectionnez les ellipses (`...`) de n’importe quel widget pour accéder aux options [!UICONTROL Afficher plus] et [!UICONTROL Afficher SQL] .

![Un tableau de bord personnalisé avec un menu déroulant des ellipses d’informations et les options Afficher plus et Afficher SQL mises en surbrillance.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## Télécharger le fichier CSV {#download-csv}

La fonction [!UICONTROL Afficher plus] affiche sous forme tabulaire les points de données spécifiques du graphique. Pour simplifier le processus de partage et de manipulation des données, vous pouvez télécharger les données traitées au format CSV à partir de cette boîte de dialogue. Sélectionnez **[!UICONTROL Télécharger CSV]** pour télécharger vos données.

>[!NOTE]
>
>Le téléchargement CSV est limité aux 500 premiers enregistrements.

![Boîte de dialogue affichant un aperçu de votre aperçu et des résultats tabulés de votre SQL qui ont généré l’insight.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

## Tri par colonne {#sort-column}

Lors de l’affichage des résultats tabulés, vous pouvez utiliser la fonctionnalité de tri pour trier par colonne dans l’ordre croissant ou décroissant. Dans votre tableau de bord personnalisé, sélectionnez les ellipses (`...`) sur n’importe quelle table pour accéder à l’option [!UICONTROL Afficher plus] .

![Un tableau de bord personnalisé avec un menu déroulant représentant des ellipses de table et l’option Afficher plus mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

Vous pouvez trier les colonnes en sélectionnant le menu déroulant en regard de leur nom, puis en sélectionnant **[!UICONTROL Tri croissant]** ou **[!UICONTROL Tri décroissant]**.

>[!NOTE]
>
>Les options [!UICONTROL Tri croissant] et [!UICONTROL Tri décroissant] s’affichent uniquement pour les colonnes qui ont été configurées avec la [fonctionnalité de tri](./overview.md#advanced-attributes).

![Une liste déroulante de colonnes de tableau présentant les options Tri croissant et Tri décroissant mises en surbrillance.](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## Redimensionner une colonne {#resize-column}

Vous pouvez redimensionner les colonnes dans les résultats tabulés afin d’améliorer la lisibilité des données. Dans votre tableau de bord personnalisé, sélectionnez les ellipses (`...`) de votre table pour accéder à l’option [!UICONTROL Afficher plus] . Utilisez le menu déroulant en regard du nom de la colonne pour la redimensionner, puis sélectionnez **[!UICONTROL Redimensionner la colonne]**.

![Une liste déroulante de colonnes de tableau présentant l’option Redimensionner la colonne mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

Sélectionnez le curseur et faites-le glisser vers la gauche ou la droite pour ajuster la taille de la colonne selon les besoins.

![Tableau présentant la barre de redimensionnement de colonne surlignée.](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## Pagination des tableaux {#table-pagination}

La pagination est automatiquement appliquée à vos tables dans la fonction [!UICONTROL Afficher plus], ce qui évite d’avoir à modifier manuellement vos requêtes SQL. Cette fonctionnalité garantit que vos données sont présentées dans un format plus gérable, ce qui facilite le processus de navigation dans les jeux de données volumineux.

Vous pouvez afficher jusqu’à 500 enregistrements par page. Pour parcourir les enregistrements, utilisez le **[!UICONTROL >]** situé au bas de la page.

![ Résultats tabulés avec les résultats et la pagination mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment afficher les résultats tabulés de l’analyse SQL de votre graphique personnalisé et télécharger les données sous forme de fichier CSV. Consultez le document d’affichage SQL pour savoir comment [afficher le code SQL derrière vos insights personnalisés](./view-sql.md).

Vous pouvez également apprendre à générer des graphiques à partir de modèles de données existants dans l’interface utilisateur de Adobe Experience Platform avec le [guide de mode de conception guidé](../standard-dashboards.md).

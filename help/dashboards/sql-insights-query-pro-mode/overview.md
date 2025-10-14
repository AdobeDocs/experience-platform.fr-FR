---
title: Rapports SQL Insights pour les applications étendues
description: Découvrez comment utiliser des requêtes SQL pour générer des informations pour vos tableaux de bord personnalisés.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '1510'
ht-degree: 0%

---

# SQL Insights pour les rapports d’applications étendues

Utilisez des requêtes SQL personnalisées pour extraire efficacement des informations à partir de différents jeux de données structurés. Les utilisateurs techniques peuvent utiliser le mode Requête pour effectuer des analyses complexes avec SQL, puis partager cette analyse avec des utilisateurs non techniques par le biais de graphiques sur votre tableau de bord personnalisé ou les exporter dans des fichiers CSV. Cette méthode de création d’informations est bien adaptée aux tableaux avec des relations claires et permet une plus grande personnalisation dans vos insights et filtres qui peuvent s’adapter à des cas d’utilisation de niche.

>[!IMPORTANT]
>
>Le mode Requête pro n’est disponible que pour les utilisateurs qui ont acheté le [SKU de Distiller de données](../../query-service/data-distiller/overview.md).

Pour générer des informations à partir de SQL, vous devez d’abord créer un tableau de bord.

## Création d’un tableau de bord personnalisé {#create-custom-dashboard}

Pour créer un tableau de bord personnalisé, sélectionnez **[!UICONTROL Tableaux de bord]** dans le panneau de navigation de gauche pour ouvrir l’espace de travail Tableaux de bord . Sélectionnez ensuite **[!UICONTROL Créer un tableau de bord]**.

![Inventaire du tableau de bord avec l’option Créer un tableau de bord mise en surbrillance.](../images/sql-insights-query-pro-mode/create-dashboard.png)

La boîte de dialogue **[!UICONTROL Créer un tableau de bord]** s’affiche. Deux options permettent de choisir la méthode de création de votre tableau de bord. Pour créer vos insights, vous pouvez utiliser un modèle de données existant avec le [[!UICONTROL mode de conception guidée]](../standard-dashboards.md) ou votre propre code SQL avec le [!UICONTROL mode de requête pro].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

L’utilisation d’un modèle de données existant présente les avantages de fournir une structure structurée, efficace et évolutive adaptée aux besoins spécifiques de votre entreprise. Pour savoir comment [créer des insights à partir d’un modèle de données existant](../standard-dashboards.md#create-widget), consultez le guide personnalisé du tableau de bord.

Les statistiques générées à partir des requêtes SQL offrent une flexibilité et une personnalisation bien plus grandes. Les techniciens peuvent utiliser le mode Requête pour effectuer une analyse complexe sur SQL, puis partager cette analyse avec des utilisateurs non techniques grâce à cette fonctionnalité de tableau de bord. Sélectionnez **[!UICONTROL Query Pro mode]** suivi de **[!UICONTROL Save]**.

>[!NOTE]
>
>Une fois la sélection effectuée, vous ne pouvez pas la modifier dans ce tableau de bord. Vous devez créer un tableau de bord avec une méthode de création de tableau de bord différente.

![&#x200B; La boîte de dialogue [!UICONTROL Créer un tableau de bord] avec le mode pro Requête et l’option Enregistrer en surbrillance.](../images/sql-insights-query-pro-mode/query-pro-mode.png)

## Présentation du mode Query Pro {#query-pro-mode}

Le mode Query Pro est un workflow basé sur l’éditeur SQL qui vous guide tout au long du processus de génération d’informations avec des requêtes SQL personnalisées dans l’interface utilisateur de Adobe Experience Platform. Avant de pouvoir générer des informations avec des requêtes SQL personnalisées, vous devez d’abord créer un tableau de bord.

## Composer SQL {#compose-sql}

Une fois que vous avez choisi de créer un tableau de bord avec le mode query pro, la boîte de dialogue **[!UICONTROL Entrer SQL]** s’affiche. Sélectionnez une base de données (modèle de données d’insights) à interroger dans le menu déroulant, puis saisissez une requête appropriée pour votre jeu de données dans l’éditeur de requêtes pro.

>[!NOTE]
>
>Le mode Requête pro n’est disponible que pour les utilisateurs qui ont acheté le SKU de Data Distiller. Le [[!UICONTROL mode de conception guidée]](../standard-dashboards.md) est disponible pour tous les utilisateurs afin de créer des insights à partir d’un modèle de données existant.

Pour plus d’informations sur les éléments de son interface utilisateur, consultez le [guide d’utilisation de Query Editor](../../query-service/ui/user-guide.md#query-authoring).

![La boîte de dialogue [!UICONTROL Entrer SQL] avec le menu déroulant du jeu de données et l’icône d’exécution mise en surbrillance. La boîte de dialogue comporte une requête SQL renseignée et l’onglet Paramètres de requête s’affiche.](../images/sql-insights-query-pro-mode/enter-sql-database-dropdown.png)

### Paramètres de requête {#query-parameters}

Pour inclure [global](./filters/global-filter.md) ou [filtres de date](./filters/date-filter.md), votre requête **doit** utiliser des paramètres de requête. Lors de la composition de votre instruction en mode query pro, vous devez fournir des exemples de valeurs si votre requête utilise des paramètres de requête. Les exemples de valeurs vous permettent d’exécuter l’instruction SQL et de créer le graphique. Notez que les exemples de valeurs que vous fournissez lors de la composition de votre instruction sont remplacés par les valeurs réelles que vous sélectionnez pour la date ou le filtre global au moment de l’exécution.

>[!IMPORTANT]
>
>Si vous souhaitez utiliser un filtre global, vous devez placer un paramètre de requête dans votre SQL, puis associer ce paramètre de requête au filtre global dans le compositeur de widgets. Dans la capture d’écran ci-dessous, `CONSENT_VALUE_FILTER` est utilisé dans le SQL comme paramètre de requête pour un filtre global. Pour plus d’informations sur la façon de procéder, consultez la [documentation sur les filtres globaux](./filters/global-filter.md#enable-global-filter) .

Pour exécuter votre requête, sélectionnez l’icône d’exécution (![Icône d’exécution.](/help/images/icons/play.png)). L’éditeur de requêtes affiche l’onglet des résultats. Ensuite, pour confirmer votre configuration et ouvrir le compositeur de widget, sélectionnez **[!UICONTROL Sélectionner]**.

>[!TIP]
>
>Si votre requête utilise des paramètres de requête, exécutez la requête une fois pour préremplir toutes les clés de paramètre de requête utilisées. La requête échoue, mais l’interface utilisateur affiche automatiquement l’onglet Paramètres de requête et répertorie toutes les clés incluses. Ajoutez les valeurs appropriées pour vos clés.

![&#x200B; La boîte de dialogue [!UICONTROL Enter SQL] avec une entrée SQL, l’onglet Results (Résultats) affiché et Sélectionner surligné.](../images/sql-insights-query-pro-mode/enter-sql-select.png)

## Renseigner le widget {#populate-widget}

Le compositeur de widgets est maintenant renseigné avec les colonnes du code SQL exécuté. Le type de tableau de bord est indiqué dans le coin supérieur gauche ; dans ce cas, il s’agit de [!UICONTROL Saisie SQL manuelle]. Sélectionnez l’icône en forme de crayon (![Une icône en forme de crayon.](/help/images/icons/edit.png)) pour modifier le SQL à tout moment.

>[!TIP]
>
>Les attributs disponibles sont des colonnes issues du SQL exécuté.

Pour créer votre widget, utilisez les attributs répertoriés dans la colonne [!UICONTROL Attributs]. Vous pouvez utiliser la barre de recherche pour rechercher des attributs ou faire défiler la liste.

![Le compositeur de widget avec la méthode de création et la colonne d’attribut mise en surbrillance.](../images/sql-insights-query-pro-mode/creation-method-and-attribute-column.png)

### Ajouter des attributs {#add-attributes}

Pour ajouter un attribut à votre widget, sélectionnez l’icône plus (![A plus).](/help/images/icons/add-circle.png)) en regard d’un nom d’attribut. Le menu déroulant qui s&#39;affiche vous permet d&#39;ajouter un attribut au graphique à partir des options déterminées par votre SQL. Les différents types de graphique disposent de différentes options, telles qu’une liste déroulante des axes X et Y.

Dans cet exemple de graphique en anneau, les options sont taille et couleur. La couleur ventile les résultats du graphique en anneau et la taille correspond à la mesure utilisée. Ajoutez un attribut au champ [!UICONTROL Color] pour diviser les résultats en différentes couleurs en fonction de leur composition.

>[!TIP]
>
>Sélectionnez l’icône de flèche vers le haut et vers le bas (![Icône de flèche vers le haut et vers le bas.](/help/images/icons/switch.png)) pour changer la disposition des axes X et Y sur les graphiques à barres ou en courbes.

![Le compositeur de widget avec la liste déroulante des icônes supplémentaires et les flèches de commutation surlignées.](../images/sql-insights-query-pro-mode/add-icon-and-switch-arrows.png)

Pour modifier le type de graphique ou de graphique de votre widget, sélectionnez l’une des options disponibles dans la liste déroulante [!UICONTROL Marques] . Les options incluent [!UICONTROL Line], [!UICONTROL Donut], [!UICONTROL Big number] et [!UICONTROL Bar]. Une fois cette option sélectionnée, une visualisation d’aperçu des paramètres actuels de votre widget est générée.

![Le compositeur de widget avec l’aperçu du widget mis en surbrillance.](../images/sql-insights-query-pro-mode/widget-preview.png)

## Attributs de tableau avancés {#advanced-attributes}

Pour appliquer des fonctionnalités de tri automatique pour toutes les colonnes de vos tableaux, sélectionnez **[!UICONTROL Modifier]** pour modifier l’intégralité de votre tableau de bord.

![Tableau de bord personnalisé avec modification mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-edit-dashboard.png)

Sélectionnez les points de suspension (`...`) dans le graphique de tableau où vous souhaitez ajouter le tri des colonnes, puis sélectionnez **[!UICONTROL Modifier]**.

![Tableau présentant le menu de points de suspension avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-edit.png)

Pour activer le tri pour n&#39;importe quelle colonne, cochez les cases **[!UICONTROL Trier]** .

![Page de modification de tableau avec cases à cocher triables en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-sortable.png)

Sélectionnez l’icône Propriétés (![Icône Propriétés .](/help/images/icons/properties.png)) dans le rail de droite pour ouvrir le panneau [!UICONTROL Propriétés]. Dans le panneau **[!UICONTROL Propriétés]**, utilisez la liste déroulante pour sélectionner la colonne **[!UICONTROL Tri par défaut]**, puis utilisez la liste déroulante pour sélectionner la **[!UICONTROL direction du tri]**. Enfin, sélectionnez **[!UICONTROL Enregistrer et fermer]**.

![Le compositeur de widget avec l’icône de propriétés, le tri par défaut, la direction de tri et l’enregistrement et la fermeture en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-properties.png)

Pour plus d&#39;informations sur l&#39;utilisation des fonctionnalités de tri, de redimensionnement des colonnes et de pagination, reportez-vous à la section [Afficher plus](./view-more.md).

## Propriétés du widget {#properties}

Sélectionnez l’icône Propriétés (![Icône Propriétés .](/help/images/icons/properties.png)) dans le rail de droite pour ouvrir le panneau des propriétés. Dans le panneau [!UICONTROL Propriétés], saisissez un nom pour le widget dans le champ de texte **[!UICONTROL Titre du widget]**. Vous pouvez également renommer différents aspects de votre graphique.

>[!NOTE]
>
>Les champs spécifiques disponibles dans la barre latérale des propriétés varient en fonction du type de graphique que vous modifiez.

![Le compositeur de widget avec l’icône de propriétés et le champ Titre du widget mis en surbrillance.](../images/sql-insights-query-pro-mode/widget-properties-title-text.png)

## Enregistrement du widget {#save-widget}

L’enregistrement dans le compositeur de widgets enregistre le widget localement dans votre tableau de bord. Si vous souhaitez enregistrer votre travail et reprendre ultérieurement, sélectionnez **[!UICONTROL Enregistrer]**. Une icône de coche sous le nom du widget indique que le widget a été enregistré. Lorsque votre widget vous satisfait, vous pouvez également sélectionner **[!UICONTROL Enregistrer et fermer]** pour le mettre à la disposition de tous les autres utilisateurs ayant accès à votre tableau de bord. Sélectionnez Annuler pour abandonner votre travail et revenir à votre tableau de bord personnalisé.

![Le compositeur de widget avec Enregistrer, Widget enregistré et Enregistrer et fermer en surbrillance.](../images/sql-insights-query-pro-mode/insight-saved.png)

## Modifier votre tableau de bord et vos graphiques {#edit}

Sélectionnez **[!UICONTROL Modifier]** pour modifier l’intégralité de votre tableau de bord ou l’une de vos insights. En mode d’édition, vous pouvez redimensionner des widgets, modifier votre code SQL ou créer et appliquer des filtres globaux et temporels. Ces filtres limitent les données affichées dans vos widgets de tableau de bord. Il s’agit d’un moyen pratique de mettre rapidement à jour et d’affiner vos informations pour différents cas d’utilisation.

![Tableau de bord personnalisé avec modification mise en surbrillance.](../images/sql-insights-query-pro-mode/edit-dashboard.png)

Sélectionnez **[!UICONTROL Ajouter un filtre]** pour créer un [[!UICONTROL filtre de date]](#create-date-filter) ou un [[!UICONTROL filtre global]](#create-global-filter). Une fois créés, tous les filtres globaux et de date sont disponibles à partir de [l’icône de filtre](#select-global-filter) (![Icône de filtre.](/help/images/icons/filter.png)) de votre tableau de bord.

![Un tableau de bord personnalisé avec le menu déroulant Ajouter un filtre en surbrillance.](../images/sql-insights-query-pro-mode/add-filter.png)

## Modification, duplication ou suppression d’un insight

Consultez le guide Tableau de bord personnalisé pour obtenir des instructions sur la façon de [modifier, dupliquer ou supprimer un widget existant](../standard-dashboards.md#duplicate).

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment écrire des requêtes SQL dans l’interface utilisateur de Adobe Experience Platform pour générer des graphiques pour vos tableaux de bord personnalisés. Ensuite, vous devez apprendre à enrichir davantage vos données en [créant un filtre de date](./filters/date-filter.md) ou [créant un filtre global](./filters/global-filter.md).

Vous pouvez également en savoir plus sur d’autres fonctionnalités de statistiques personnalisées, y compris [les différentes options d’affichage pour vos données analysées par SQL](./view-more.md) ou sur la manière [d’afficher le code SQL derrière vos insights personnalisés](./view-sql.md).

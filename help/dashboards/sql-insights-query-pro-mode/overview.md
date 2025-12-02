---
title: Informations SQL pour les rapports d’application étendus
description: Découvrez comment utiliser les requêtes SQL pour générer des informations pour vos tableaux de bord personnalisés.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 9f4ce2a3a8af72342683c859caa270662b161b7d
workflow-type: tm+mt
source-wordcount: '1445'
ht-degree: 0%

---

# Informations SQL pour la création de rapports d’application étendue

Utilisez des requêtes SQL personnalisées pour extraire efficacement des informations à partir de divers jeux de données structurés. Les techniciens peuvent utiliser query pro mode pour effectuer des analyses complexes avec SQL, puis partager ces analyses avec des utilisateurs non techniques par le biais de graphiques sur votre tableau de bord personnalisé ou les exporter dans des fichiers CSV. Cette méthode de création d’insight est bien adaptée aux tableaux avec des relations claires et permet un plus grand degré de personnalisation de vos informations et filtres qui peut s’adapter aux cas d’utilisation de niche.

>[!IMPORTANT]
>
>Le mode Query Pro n’est disponible que pour les utilisateurs qui ont acheté le [SKU de Data Distiller](../../query-service/data-distiller/overview.md).

Pour générer des informations à partir de SQL, vous devez d’abord créer un tableau de bord.

## Créer un tableau de bord personnalisé {#create-custom-dashboard}

Pour créer un tableau de bord personnalisé, sélectionnez **[!UICONTROL Dashboards]** dans le panneau de navigation de gauche pour ouvrir l’espace de travail Tableaux de bord . Ensuite, sélectionnez **[!UICONTROL Create dashboard]**.

![Inventaire des tableaux de bord avec l’option Créer un tableau de bord mise en surbrillance.](../images/sql-insights-query-pro-mode/create-dashboard.png)

La boîte de dialogue **[!UICONTROL Create dashboard]** s’affiche. Vous pouvez choisir la méthode de création de votre tableau de bord selon deux options. Pour créer vos informations, vous pouvez utiliser un modèle de données existant avec le [[!UICONTROL Guided design mode]](../standard-dashboards.md) ou votre propre code SQL avec le [!UICONTROL Query pro mode].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

L’utilisation d’un modèle de données existant a l’avantage de fournir un cadre structuré, efficace et évolutif adapté aux besoins spécifiques de votre entreprise. Pour savoir comment [créer des informations à partir d’un modèle de données existant](../standard-dashboards.md#create-widget), reportez-vous au guide du tableau de bord personnalisé.

Les informations générées à partir de requêtes SQL offrent une flexibilité et une personnalisation bien supérieures. Les techniciens peuvent utiliser query pro mode pour effectuer des analyses complexes sur SQL, puis partager ces analyses avec des utilisateurs n&#39;ayant pas de connaissances techniques grâce à cette fonctionnalité de tableau de bord. Sélectionnez **[!UICONTROL Query pro mode]** suivi de **[!UICONTROL Save]**.

>[!NOTE]
>
>Une fois une sélection effectuée, vous ne pouvez plus la modifier dans ce tableau de bord. Vous devez créer un tableau de bord avec une méthode de création de tableau de bord différente.

![La boîte de dialogue [!UICONTROL Create dashboard] avec le mode Query Pro et Enregistrer mis en surbrillance.](../images/sql-insights-query-pro-mode/query-pro-mode.png)

## Présentation du mode Query Pro {#query-pro-mode}

Query Pro Mode est un workflow basé sur l’éditeur SQL qui vous guide tout au long du processus de génération d’informations avec des requêtes SQL personnalisées dans l’interface utilisateur de Adobe Experience Platform. Avant de pouvoir générer des informations avec des requêtes SQL personnalisées, vous devez d’abord créer un tableau de bord.

## Composer SQL {#compose-sql}

Une fois que vous avez choisi de créer un tableau de bord avec le mode query pro, la boîte de dialogue **[!UICONTROL Enter SQL]** s’affiche. Sélectionnez une base de données (modèle de données d’informations) à interroger dans le menu déroulant, puis saisissez une requête appropriée pour votre jeu de données dans l’éditeur de pro de requête.

>[!NOTE]
>
>Le mode Query Pro n’est disponible que pour les utilisateurs qui ont acheté le SKU de Data Distiller. L’[[!UICONTROL Guided design mode]](../standard-dashboards.md) est disponible pour tous les utilisateurs et utilisatrices afin de créer des informations à partir d’un modèle de données existant.

Consultez le [guide d’utilisation de Query Editor](../../query-service/ui/user-guide.md#query-authoring) pour plus d’informations sur ses éléments d’interface utilisateur.

![La boîte de dialogue [!UICONTROL Enter SQL] avec le menu déroulant du jeu de données et l’icône d’exécution en surbrillance, une requête SQL est renseignée dans la boîte de dialogue et l’onglet des paramètres de requête s’affiche.](../images/sql-insights-query-pro-mode/enter-sql-database-dropdown.png)

### Paramètres de requête {#query-parameters}

Pour inclure des filtres [globaux](./filters/global-filter.md) ou [date](./filters/date-filter.md) votre requête **doit** utiliser des paramètres de requête. Lors de la composition de votre instruction en mode Query Pro, vous devez fournir des exemples de valeurs si votre requête utilise des paramètres de requête. Les exemples de valeurs permettent d’exécuter l’instruction SQL et de créer le graphique. Notez que les exemples de valeurs que vous fournissez lors de la composition de votre instruction sont remplacés par les valeurs réelles que vous sélectionnez pour la date ou le filtre global au moment de l’exécution.

>[!IMPORTANT]
>
>Si vous souhaitez utiliser un filtre global, vous devez placer un paramètre de requête dans votre SQL, puis lier ce paramètre de requête au filtre global dans le compositeur de widgets. Dans la capture d’écran ci-dessous, `CONSENT_VALUE_FILTER` est utilisé dans le SQL comme paramètre de requête pour un filtre global. Consultez la [documentation sur les filtres globaux](./filters/global-filter.md#enable-global-filter) pour plus d’informations sur la procédure à suivre.

Pour exécuter votre requête, sélectionnez l’icône d’exécution (![ L’icône d’exécution .](/help/images/icons/play.png)). Le Query Editor affiche l’onglet des résultats . Ensuite, pour confirmer votre configuration et ouvrir le compositeur de widgets, sélectionnez **[!UICONTROL Select]**.

>[!TIP]
>
>Si votre requête utilise des paramètres de requête, exécutez une seule fois la requête pour pré-remplir toutes les clés de paramètre de requête utilisées. La requête échouera, mais l’interface utilisateur affiche automatiquement l’onglet Paramètres de requête et répertorie toutes les clés incluses. Ajoutez les valeurs appropriées pour vos clés.

![Boîte de dialogue [!UICONTROL Enter SQL] avec entrée SQL, onglet Résultats affiché et Sélectionner en surbrillance.](../images/sql-insights-query-pro-mode/enter-sql-select.png)

## Renseigner le widget {#populate-widget}

Le compositeur de widget est maintenant renseigné avec les colonnes du SQL exécuté. Le type de tableau de bord est indiqué en haut à gauche. Dans ce cas, il s’agit de [!UICONTROL Manual SQL Entry]. Sélectionnez l’icône en forme de crayon (![une icône en forme de crayon.](/help/images/icons/edit.png)) pour modifier le code SQL à tout moment.

>[!TIP]
>
>Les attributs disponibles sont des colonnes extraites du code SQL exécuté.

Pour créer votre widget, utilisez les attributs répertoriés dans la colonne [!UICONTROL Attributes] . Vous pouvez utiliser la barre de recherche pour rechercher des attributs ou faire défiler la liste.

![Le compositeur de widget avec la méthode de création et la colonne d’attribut mises en surbrillance.](../images/sql-insights-query-pro-mode/creation-method-and-attribute-column.png)

### Ajouter des attributs {#add-attributes}

Pour ajouter un attribut à votre widget, sélectionnez l’icône plus (![A icône plus.](/help/images/icons/add-circle.png)) à côté d’un nom d’attribut. Le menu déroulant qui s’affiche vous permet d’ajouter un attribut au graphique à partir des options déterminées par votre SQL. Différents types de graphique comportent différentes options, telles qu’une liste déroulante des axes X et Y.

Dans cet exemple de graphique en anneau, les options sont la taille et la couleur. La couleur répartit les résultats du graphique en anneau et la taille correspond à la mesure réelle utilisée. Ajoutez un attribut au champ [!UICONTROL Color] pour fractionner les résultats en différentes couleurs en fonction de la composition de cet attribut.

>[!TIP]
>
>Sélectionnez l’icône des flèches vers le haut et vers le bas (![Icône des flèches vers le haut et vers le bas.](/help/images/icons/switch.png)) pour changer la disposition des axes X et Y sur les graphiques en barres ou en courbes.

![Le compositeur de widget avec la liste déroulante d’icône d’ajout et les flèches de basculement mises en surbrillance.](../images/sql-insights-query-pro-mode/add-icon-and-switch-arrows.png)

Pour modifier le type de graphique ou de graphique de votre widget, sélectionnez l’une des options disponibles dans la liste déroulante [!UICONTROL Marks] . Les options disponibles sont [!UICONTROL Line], [!UICONTROL Donut], [!UICONTROL Big number] et [!UICONTROL Bar]. Une fois sélectionné, un aperçu des paramètres actuels de votre widget est généré.

![Le compositeur de widgets avec l’aperçu du widget mis en surbrillance.](../images/sql-insights-query-pro-mode/widget-preview.png)

## Attributs de tableau avancés {#advanced-attributes}

Pour appliquer des fonctionnalités de tri automatique à l’une ou à l’ensemble des colonnes de vos tableaux, sélectionnez **[!UICONTROL Edit]** pour modifier l’ensemble du tableau de bord.

![Tableau de bord personnalisé avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-edit-dashboard.png)

Dans le graphique en tableau, sélectionnez les points de suspension (`...`) auxquels vous souhaitez ajouter un tri des colonnes, puis sélectionnez **[!UICONTROL Edit]**.

![Tableau présentant le menu représentant des points de suspension avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-edit.png)

Pour activer le tri pour n’importe quelle colonne, cochez les cases **[!UICONTROL Sortable]**.

![Page d’édition du tableau avec les cases à cocher triables mises en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-sortable.png)

Sélectionnez l’icône des propriétés (![ Icône Propriétés .](/help/images/icons/properties.png)) dans le rail de droite pour ouvrir le panneau [!UICONTROL Properties]. Dans le panneau **[!UICONTROL Properties]**, utilisez la liste déroulante pour sélectionner la colonne **[!UICONTROL Default sort]**, puis utilisez la liste déroulante pour sélectionner la **[!UICONTROL Sort direction]**. Enfin, sélectionnez **[!UICONTROL Save and close]**.

![Le compositeur de widget avec l’icône de propriétés, le tri par défaut, l’ordre de tri, l’enregistrement et la fermeture mis en surbrillance.](../images/sql-insights-query-pro-mode/advanced-table-properties.png)

Pour en savoir plus sur l’utilisation des fonctionnalités de tri, de redimensionnement des colonnes et de pagination, voir [En savoir plus](./view-more.md).

## Propriétés du widget {#properties}

Sélectionnez l’icône des propriétés (![ Icône Propriétés .](/help/images/icons/properties.png)) dans le rail de droite pour ouvrir le panneau propriétés . Dans le panneau [!UICONTROL Properties], saisissez le nom du widget dans le champ de texte **[!UICONTROL Widget title]** . Vous pouvez également renommer divers aspects de votre graphique.

>[!NOTE]
>
>Les champs spécifiques disponibles dans la barre latérale des propriétés varient en fonction du type de graphique que vous modifiez.

![Le compositeur de widget avec l’icône de propriétés et le champ Titre du widget mis en surbrillance.](../images/sql-insights-query-pro-mode/widget-properties-title-text.png)

## Enregistrer le widget {#save-widget}

L’enregistrement dans le compositeur de widgets enregistre le widget localement dans votre tableau de bord. Si vous souhaitez enregistrer votre travail et reprendre ultérieurement, sélectionnez **[!UICONTROL Save]**. Une icône représentant une coche sous le nom du widget indique que le widget a été enregistré. Lorsque vous êtes satisfait(e) de votre widget, vous pouvez également sélectionner **[!UICONTROL Save and close]** pour rendre le widget disponible pour tous les autres utilisateurs ayant accès à votre tableau de bord. Sélectionnez Annuler pour abandonner votre travail et revenir à votre tableau de bord personnalisé.

![Le compositeur de widgets avec Enregistrer, Widget enregistré et Enregistrer et fermer en surbrillance.](../images/sql-insights-query-pro-mode/insight-saved.png)

## Modifier votre tableau de bord et vos graphiques {#edit}

Sélectionnez **[!UICONTROL Edit]** pour modifier l’ensemble de votre tableau de bord ou l’un de vos insights. En mode d’édition, vous pouvez redimensionner des widgets, modifier votre code SQL ou créer et appliquer des filtres globaux et temporels. Ces filtres limitent les données affichées dans les widgets de votre tableau de bord. Il s’agit d’un moyen pratique de mettre rapidement à jour et d’affiner vos informations pour différents cas d’utilisation.

![Tableau de bord personnalisé avec l’option Modifier mise en surbrillance.](../images/sql-insights-query-pro-mode/edit-dashboard.png)

Sélectionnez **[!UICONTROL Add filter]** pour créer un [[!UICONTROL Date filter]](#create-date-filter) ou un [[!UICONTROL Global filter]](#create-global-filter). Une fois créés, tous les filtres globaux et de date sont disponibles à partir de [l’icône de filtre](#select-global-filter) (![une icône de filtre.](/help/images/icons/filter.png)) de votre tableau de bord.

![Tableau de bord personnalisé avec le menu déroulant Ajouter un filtre mis en surbrillance.](../images/sql-insights-query-pro-mode/add-filter.png)

## Modification, duplication ou suppression d’une insight

Consultez le guide du tableau de bord personnalisé pour obtenir des instructions sur la [modification, duplication ou suppression d’un widget existant](../standard-dashboards.md#duplicate).

## Étapes suivantes

Vous êtes arrivé au bout de ce document. À présent, vous savez comment écrire des requêtes SQL dans l’interface utilisateur de Adobe Experience Platform pour générer des graphiques pour vos tableaux de bord personnalisés. Vous devez ensuite apprendre à enrichir davantage vos données en [créant un filtre de date](./filters/date-filter.md) ou [créant un filtre global](./filters/global-filter.md).

Vous pouvez également en savoir plus sur d’autres fonctionnalités d’informations personnalisées, notamment [les différentes options d’affichage de vos données analysées SQL](./view-more.md) ou sur la manière d’[afficher le code SQL derrière vos informations personnalisées](./view-sql.md).

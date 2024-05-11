---
title: Mode Query Pro
description: Découvrez comment utiliser les requêtes SQL dans l’interface utilisateur de Adobe Experience Platform pour générer des graphiques pour vos tableaux de bord personnalisés.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Mode Requête pro {#query-pro-mode}

Le mode Query Pro est un workflow basé sur l’éditeur SQL qui vous guide tout au long du processus de génération d’informations avec des requêtes SQL personnalisées dans l’interface utilisateur de Adobe Experience Platform. Avant de pouvoir générer des informations avec des requêtes SQL personnalisées, vous devez d’abord [création d’un tableau de bord](./overview.md#create-custom-dashboard).

## Composer SQL {#compose-sql}

Une fois que vous avez choisi de créer un tableau de bord avec le mode query pro , la variable **[!UICONTROL Saisir SQL]** s’affiche. Sélectionnez une base de données (modèle de données d’insights) à interroger dans le menu déroulant, puis saisissez une requête appropriée pour votre jeu de données dans l’éditeur de requêtes pro.

>[!NOTE]
>
>Le mode Requête pro n’est disponible que pour les utilisateurs qui ont acheté le SKU de Data Distiller. La variable [[!UICONTROL Mode de conception guidée]](../../user-defined-dashboards.md) est disponible pour tous les utilisateurs afin de créer des insights à partir d’un modèle de données existant.

Voir [Guide d’utilisation de Query Editor](../../../query-service/ui/user-guide.md#query-authoring) pour plus d’informations sur ses éléments d’interface utilisateur.

![La variable [!UICONTROL Saisir SQL] boîte de dialogue avec le menu déroulant du jeu de données et l’icône d’exécution mise en surbrillance. La boîte de dialogue comporte une requête SQL renseignée et l’onglet paramètres de requête s’affiche.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### Paramètres de requête {#query-parameters}

À inclure [global](./filters/global-filter.md) ou [filtres de date](./filters/date-filter.md) votre requête **must** utilisez les paramètres de requête. Lors de la composition de votre instruction en mode query pro, vous devez fournir des exemples de valeurs si votre requête utilise des paramètres de requête. Les exemples de valeurs vous permettent d’exécuter l’instruction SQL et de créer le graphique. Notez que les exemples de valeurs que vous fournissez lors de la composition de votre instruction sont remplacés par les valeurs réelles que vous sélectionnez pour la date ou le filtre global au moment de l’exécution.



>[!IMPORTANT]
>
>Si vous souhaitez utiliser un filtre global, vous devez placer un paramètre de requête dans votre SQL, puis associer ce paramètre de requête au filtre global dans le compositeur de widgets. Dans la capture d’écran ci-dessous, `CONSENT_VALUE_FILTER` est utilisé dans SQL comme paramètre de requête pour un filtre global. Voir [documentation sur les filtres globaux](./filters/global-filter.md#enable-global-filter) pour plus d’informations sur la manière de procéder.

Pour exécuter votre requête, sélectionnez l’icône d’exécution (![Icône d’exécution.](../../images/customizable-insights/run-icon.png)). L’éditeur de requêtes affiche l’onglet des résultats. Ensuite, pour confirmer votre configuration et ouvrir le compositeur de widget, sélectionnez **[!UICONTROL Sélectionner]**.

>[!TIP]
>
>Si votre requête utilise des paramètres de requête, exécutez la requête une fois pour préremplir toutes les clés de paramètre de requête utilisées. La requête échoue, mais l’interface utilisateur affiche automatiquement l’onglet Paramètres de requête et répertorie toutes les clés incluses. Ajoutez les valeurs appropriées pour vos clés.

![La variable [!UICONTROL Saisir SQL] avec une entrée SQL, l’onglet des résultats s’affichait et l’option Sélectionner mise en surbrillance.](../../images/customizable-insights/enter-sql-select.png)

## Renseigner le widget {#populate-widget}

Le compositeur de widgets est maintenant renseigné avec les colonnes du code SQL exécuté. Le type de tableau de bord est indiqué en haut à gauche, dans ce cas, il s’agit de [!UICONTROL Entrée SQL manuelle]. Sélectionnez l’icône de crayon (![Une icône en forme de crayon.](../../images/customizable-insights/edit-icon.png)) pour modifier le SQL à tout moment.

>[!TIP]
>
>Les attributs disponibles sont des colonnes issues du SQL exécuté.

Pour créer votre widget, utilisez les attributs répertoriés dans le [!UICONTROL Attributs] colonne . Vous pouvez utiliser la barre de recherche pour rechercher des attributs ou faire défiler la liste.

![Le compositeur de widget avec la méthode de création et la colonne d’attribut mise en surbrillance.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### Ajout d’attributs {#add-attributes}

Pour ajouter un attribut à votre widget, cliquez sur l’icône plus (![Une icône plus.](../../images/customizable-insights/add-icon.png)) en regard d’un nom d’attribut. Le menu déroulant qui s&#39;affiche vous permet d&#39;ajouter un attribut au graphique à partir des options déterminées par votre SQL. Les différents types de graphique disposent de différentes options, telles qu’une liste déroulante des axes X et Y.

Dans cet exemple de graphique en anneau, les options sont taille et couleur. La couleur ventile les résultats du graphique en anneau et la taille correspond à la mesure utilisée. Ajoutez un attribut à la variable [!UICONTROL Couleur] pour fractionner les résultats en différentes couleurs en fonction de leur composition.

>[!TIP]
>
>Sélectionnez l’icône des flèches haut et bas (![Icône Flèche vers le haut et le bas.](../../images/customizable-insights/switch-axis-icon.png)) pour changer la disposition des axes X et Y sur les graphiques à barres ou en courbes.

![compositeur de widgets avec la liste déroulante des icônes supplémentaires et les flèches de commutation surlignées.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

Pour modifier le type de graphique ou de graphique de votre widget, sélectionnez l’une des options disponibles du [!UICONTROL Marques] menu déroulant. Les options incluent [!UICONTROL Ligne], [!UICONTROL Anneau], [!UICONTROL Grand nombre], et [!UICONTROL Barre]. Une fois cette option sélectionnée, une visualisation d’aperçu des paramètres actuels de votre widget est générée.

![Le compositeur de widgets avec l’aperçu de widget mis en surbrillance.](../../images/customizable-insights/widget-preview.png)

## Propriétés du widget {#properties}

Cliquez sur l’icône Propriétés (![Icône Propriétés.](../../images/customizable-insights/properties-icon.png)) dans le rail de droite pour ouvrir le panneau des propriétés. Dans le [!UICONTROL Propriétés] , saisissez un nom pour le widget dans le **[!UICONTROL Titre du widget]** Champ de texte. Vous pouvez également renommer différents aspects de votre graphique.

>[!NOTE]
>
>Les champs spécifiques disponibles dans la barre latérale des propriétés varient en fonction du type de graphique que vous modifiez.

![Le compositeur de widgets avec l’icône de propriétés et le champ Titre du widget mis en surbrillance.](../../images/customizable-insights/widget-properties-title-text.png)

## Enregistrement du widget {#save-widget}

L’enregistrement dans le compositeur de widgets enregistre le widget localement dans votre tableau de bord. Si vous souhaitez enregistrer votre travail et reprendre ultérieurement, sélectionnez **[!UICONTROL Enregistrer]**. Une icône de coche sous le nom du widget indique que le widget a été enregistré. Lorsque vous êtes satisfait de votre widget, vous pouvez également sélectionner **[!UICONTROL Enregistrer et fermer]** pour rendre le widget disponible pour tous les autres utilisateurs ayant accès à votre tableau de bord. Sélectionnez Annuler pour abandonner votre travail et revenir à votre tableau de bord personnalisé.

![Le compositeur de widgets avec Enregistrer, Widget enregistré et Enregistrer et fermer en surbrillance.](../../images/customizable-insights/insight-saved.png)

## Modifier votre tableau de bord et vos graphiques {#edit}

Sélectionner **[!UICONTROL Modifier]** pour modifier l’intégralité du tableau de bord ou l’une de vos informations. En mode d’édition, vous pouvez redimensionner des widgets, modifier votre code SQL ou créer et appliquer des filtres globaux et temporels. Ces filtres limitent les données affichées dans vos widgets de tableau de bord. Il s’agit d’un moyen pratique de mettre rapidement à jour et d’affiner vos informations pour différents cas d’utilisation.

![Tableau de bord personnalisé avec l’option Modifier mise en surbrillance.](../../images/customizable-insights/edit-dashboard.png)

Sélectionner **[!UICONTROL Ajouter un filtre]** pour créer une [[!UICONTROL Filtre de date]](#create-date-filter) ou [[!UICONTROL Filtre global]](#create-global-filter). Une fois créés, tous les filtres de date et globaux sont disponibles à partir de [l’icône de filtre](#select-global-filter) (![Icône de filtre.](../../images/customizable-insights/filter.png)) de votre tableau de bord.

![Un tableau de bord personnalisé avec le menu déroulant Ajouter un filtre en surbrillance.](../../images/customizable-insights/add-filter.png)

## Modification, duplication ou suppression d’un insight

Consultez le guide Tableau de bord personnalisé pour obtenir des instructions sur la manière de [modification, duplication ou suppression d’un widget existant](../../user-defined-dashboards.md#duplicate).

## Étapes suivantes

Après avoir lu ce document, vous savez maintenant comment écrire des requêtes SQL dans l’interface utilisateur de Adobe Experience Platform pour générer des graphiques pour vos tableaux de bord personnalisés. Ensuite, vous devriez apprendre à enrichir davantage vos données en [création d’un filtre de date](./filters/date-filter.md), ou [création d’un filtre global](./filters/global-filter.md).

Vous pouvez également en savoir plus sur les autres fonctionnalités de statistiques personnalisées, notamment [les différentes options d&#39;affichage pour vos données analysées par SQL](./view-more.md) ou comment [afficher le code SQL derrière vos insights personnalisés ;](./view-sql.md).

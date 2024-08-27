---
title: Tableaux de bord personnalisés
description: Découvrez comment créer et gérer des tableaux de bord personnalisés dans lesquels vous pouvez créer, ajouter et modifier des widgets personnalisés pour visualiser des mesures clés.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: 2ddfa221ecdebad81343516935e81691021e1fbc
workflow-type: tm+mt
source-wordcount: '1624'
ht-degree: 3%

---

# Tableaux de bord personnalisés

Utilisez les tableaux de bord Adobe Experience Platform pour accélérer les insights et personnaliser la visualisation par le biais de la fonctionnalité Tableaux de bord . Utilisez cette fonction pour créer et gérer des tableaux de bord personnalisés dans lesquels vous pouvez créer, ajouter et modifier des widgets personnalisés afin de visualiser les mesures clés pertinentes pour votre entreprise.


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Création d’un tableau de bord personnalisé

Pour créer un tableau de bord personnalisé, accédez d’abord à l’inventaire du tableau de bord. Sélectionnez **[!UICONTROL Tableaux de bord]** dans le volet de navigation de gauche de l’interface utilisateur de Platform, puis **[!UICONTROL Créer un tableau de bord]**.

![Inventaire du tableau de bord avec des tableaux de bord dans le volet de navigation de gauche et &quot;Créer un tableau de bord&quot; en surbrillance.](./images/user-defined-dashboards/create-dashboard.png)

Avant d’ajouter un tableau de bord personnalisé, l’inventaire des tableaux de bord est vide et affiche le message &quot;Aucun tableau de bord trouvé&quot;. message. Une fois créés, tous vos tableaux de bord sont répertoriés dans l’inventaire des tableaux de bord.

<!-- >[!NOTE]
>
>To edit an existing dashboard, select the dashboard name from the inventory list followed by the pencil icon (![A pencil icon.](/help/images/icons/edit.png))
>![A custom inventory listed in the dashboard inventory.](./images/user-defined-dashboards/dashbaord-inventory.png "A custom inventory listed in the dashboard inventory."){width="100" zoomable="yes"} -->

La boîte de dialogue [!UICONTROL Créer un tableau de bord] s’affiche. Saisissez un nom explicite et convivial pour la collection de widgets que vous avez l’intention de créer, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Boîte de dialogue Créer un tableau de bord.](./images/user-defined-dashboards/create-dashboard-dialog.png)

Les utilisateurs qui ont acheté le SKU de Data Distiller ont la possibilité d’utiliser des requêtes SQL personnalisées pour créer leurs informations. Consultez le [guide de création de SQL Insight](./data-distiller/sql-insights/overview.md) pour obtenir des instructions sur ce processus.

Le tableau de bord vierge nouvellement créé s’affiche avec le nom de votre choix dans le coin supérieur gauche de la vue.

## Créer un widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Nombre maximal de widgets"
>abstract="Le service Tableau de bord prend en charge jusqu’à dix widgets. Une fois que vous avez ajouté dix widgets à votre tableau de bord, l’option [!UICONTROL Ajouter un nouveau widget] est désactivée et apparaît en gris."

Dans la nouvelle vue de tableau de bord, sélectionnez **[!UICONTROL Ajouter un nouveau widget]** pour lancer le processus de création de widget.

>[!IMPORTANT]
>
>Chaque tableau de bord prend en charge jusqu’à dix widgets. Une fois que vous avez ajouté dix widgets à votre tableau de bord, l’option [!UICONTROL Ajouter un nouveau widget] est désactivée et apparaît en gris.

![ Le nouveau tableau de bord vide avec l’ajout d’un nouveau widget surligné.](./images/user-defined-dashboards/add-new-widget.png)

### Compositeur de widgets

L’espace de travail du compositeur de widgets s’affiche. Ensuite, sélectionnez **[!UICONTROL Sélectionner les données]** pour choisir le modèle de données à partir duquel ajouter des attributs à vos widgets.

![Espace de travail du compositeur de widgets.](./images/user-defined-dashboards/widget-composer.png)

#### Sélectionner le modèle de données {#select-data-model}

La boîte de dialogue [!UICONTROL Select data model] s’affiche. Sélectionnez un modèle de données dans la colonne de gauche pour afficher la liste de prévisualisation de tous les tableaux disponibles. Le modèle de données préconfiguré pour Real-Time Customer Data Platform est appelé [!UICONTROL CDPInsights].

>[!TIP]
>
>Sélectionnez l’icône d’information (![Icône d’information.](/help/images/icons/info.png)) pour afficher le nom complet du modèle de données s’il est trop long à afficher dans le rail de données.

![Boîte de dialogue Sélectionner les données.](./images/user-defined-dashboards/select-data-model-dialog.png)

La liste d’aperçu fournit des détails sur les tables contenues dans le modèle de données. Le tableau ci-dessous fournit une description des champs de la colonne et de leurs valeurs potentielles.

| Champ de colonne | Description |
|---|---|
| [!UICONTROL Titre] | Nom de la table. |
| [!UICONTROL Type de table] | Type de tableau. Les types potentiels incluent : `fact`, `dimension` et `none`. |
| [!UICONTROL Enregistrements] | Le nombre d&#39;enregistrements associés à la table choisie. |
| [!UICONTROL Recherches] | Le nombre de tables jointes à la table choisie. |
| [!UICONTROL Attributs] | Le nombre d’attributs de la table choisie. |

Sélectionnez **[!UICONTROL Suivant]** pour confirmer le choix du modèle de données. La vue suivante affiche la liste des tableaux disponibles dans le rail de gauche. Sélectionnez un tableau pour afficher une ventilation complète des données contenues dans le tableau sélectionné.

### Renseigner le widget {#populate-widget}

Le panneau [!UICONTROL Aperçu] contient des onglets pour [!UICONTROL Exemples d’enregistrements] et [!UICONTROL Attributs]. L’onglet [!UICONTROL Exemples d’enregistrements] fournit un sous-ensemble des enregistrements de la table sélectionnée dans une vue tabulée. L’onglet [!UICONTROL Attributs] fournit le nom d’attribut, le type de données et la table source pour chaque attribut associé à la table sélectionnée.

Sélectionnez un tableau dans la liste disponible dans le rail de gauche pour fournir des données pour votre widget, puis sélectionnez **[!UICONTROL Sélectionner]** pour revenir au compositeur de widget.

![ La boîte de dialogue de sélection des données avec sélection mise en surbrillance.](./images/user-defined-dashboards/select-a-table.png)

Le compositeur de widgets est maintenant renseigné avec les données du tableau de votre choix.

Le modèle de données et le tableau actuellement sélectionné sont affichés dans la partie supérieure du rail de gauche, et les attributs disponibles pour créer votre widget sont répertoriés dans la colonne [!UICONTROL Attributs]. Vous pouvez utiliser la barre de recherche pour rechercher des attributs au lieu de faire défiler la liste, ou modifier le modèle de données sélectionné en sélectionnant l’icône en forme de crayon (![ icône en forme de crayon).](/help/images/icons/edit.png)) dans le rail de gauche.

![Widget renseigné avec des données dans le compositeur de widget.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Ajout et filtrage d’attributs {#add-and-filter-attributes}

Sélectionnez l’icône d’ajout (![Icône d’ajout.](/help/images/icons/add-circle.png)) en regard d’un nom d’attribut pour ajouter un attribut à votre widget. Le menu déroulant qui s’affiche vous permet d’ajouter un attribut en tant qu’axe X, axe Y, couleur ou filtre pour votre widget. L’attribut [!UICONTROL Color] vous permet de différencier les résultats des marques des axes X et Y en fonction de la couleur. Pour ce faire, il divise les résultats en différentes couleurs en fonction de leur composition d’un troisième attribut.

>[!TIP]
>
>Si vous souhaitez retourner la disposition des axes X et Y, sélectionnez l’icône de flèche vers le haut et vers le bas (![Icône de flèche vers le haut et vers le bas.](/help/images/icons/switch.png)) pour changer leur arrangement.

![Le compositeur de widget avec la liste déroulante des icônes supplémentaires mise en surbrillance.](./images/user-defined-dashboards/attributes-dropdown.png)

Pour modifier le type de graphique ou de graphique de votre widget, sélectionnez la liste déroulante [!UICONTROL Marques] et choisissez l’une des options disponibles. Les options incluent des barres, des points, des coches, des lignes ou une zone. Une fois cette option sélectionnée, une visualisation d’aperçu des paramètres actuels de votre widget est générée.

![Le compositeur de widget avec la liste déroulante Marques mise en surbrillance.](./images/user-defined-dashboards/marks-dropdown.png)

En ajoutant un attribut comme filtre, vous pouvez sélectionner les valeurs à inclure ou à exclure du widget. Après avoir ajouté un filtre à partir de la liste des attributs, la boîte de dialogue [!UICONTROL Filtre] s’affiche dans laquelle vous pouvez sélectionner ou désélectionner des valeurs à l’aide de leur case à cocher.

![ La boîte de dialogue de filtrage permettant de filtrer les valeurs de votre widget.](./images/user-defined-dashboards/filter-dialog.png)

#### Filtrage des données historiques {#filter-historical-data}

Pour filtrer les données historiques des insights générés par votre widget, ajoutez l’attribut `date_key` comme filtre et sélectionnez **[!UICONTROL Date récente]** suivi de **[!UICONTROL Appliquer]**. Ce filtre permet de s’assurer que les données utilisées pour obtenir des informations proviennent de l’instantané système le plus récent.

![Boîte de dialogue [!UICONTROL Filtre : date_key] avec [!UICONTROL Date récente] et [!UICONTROL Appliquer] mise en surbrillance.](./images/user-defined-dashboards/recent-date.png)

Vous pouvez également créer une période personnalisée en fonction de laquelle filtrer vos données. Sélectionnez **[!UICONTROL Sélectionner des dates]** pour étendre la boîte de dialogue avec une liste de dates disponibles. Utilisez la case à cocher **[!UICONTROL Sélectionner tout]** pour activer ou désactiver toutes les options disponibles, ou cochez la case pour chaque jour individuellement. Enfin, sélectionnez **[!UICONTROL Appliquer]** pour confirmer vos choix.

>[!NOTE]
>
>Si l’attribut `date_key` a déjà été ajouté en tant que filtre, sélectionnez les points de suspension suivis de **[!UICONTROL Modifier]** dans la liste déroulante des options pour modifier la période de filtrage.

![Boîte de dialogue [!UICONTROL Filtre : date_key] avec cases à cocher de jour individuelles cochées et non cochées.](./images/user-defined-dashboards/select-dates.png)

### Propriétés du widget

Sélectionnez l’icône Propriétés (![Icône Propriétés .](/help/images/icons/properties.png)) dans le rail de droite pour ouvrir le panneau des propriétés. Dans le panneau [!UICONTROL Propriétés], saisissez un nom pour le widget dans le champ de texte [!UICONTROL Titre du widget].

![Panneau Propriétés avec l’icône de propriétés et le champ Titre du widget surligné.](./images/user-defined-dashboards/properties-panel.png)

Dans le panneau des propriétés du widget, vous pouvez modifier plusieurs aspects de votre widget. Vous disposez d’un contrôle total pour modifier l’emplacement de la légende du widget. Pour déplacer la légende, sélectionnez la liste déroulante [!UICONTROL Emplacements de légende] et choisissez l’emplacement de votre choix dans la liste des options disponibles. Vous pouvez également renommer l’étiquette associée à la légende et l’axe X ou Y en saisissant un nouveau nom dans le champ de texte [!UICONTROL Titre de la légende] ou le champ de texte [!UICONTROL Libellé de l’axe] respectivement.

#### Enregistrement du widget {#save-widget}

L’enregistrement dans le compositeur de widgets enregistre le widget localement dans votre tableau de bord. Si vous souhaitez enregistrer votre travail et reprendre ultérieurement, sélectionnez **[!UICONTROL Enregistrer]**. Une icône de coche sous le nom du widget indique que le widget a été enregistré. Lorsque votre widget vous satisfait, vous pouvez également sélectionner **[!UICONTROL Enregistrer et fermer]** pour le mettre à la disposition de tous les autres utilisateurs ayant accès à votre tableau de bord. Sélectionnez **[!UICONTROL Annuler]** pour abandonner votre travail et revenir à votre tableau de bord personnalisé.

![Nouvelle confirmation d’enregistrement de widget.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Sélectionnez l’icône Propriétés (![Icône Propriétés .](/help/images/icons/properties.png)) en regard du nom du tableau de bord pour afficher des détails sur sa création. Vous pouvez modifier le nom de votre tableau de bord dans la boîte de dialogue qui s’affiche.

Les widgets peuvent être réorganisés et redimensionnés dans cet espace de travail. Sélectionnez **[!UICONTROL Enregistrer]** pour conserver le nom et la mise en page de votre tableau de bord.

![Le tableau de bord défini par l’utilisateur avec un widget personnalisé et le bouton d’enregistrement mis en surbrillance.](./images/user-defined-dashboards/user-defined-dashboard.png)

Pour s’assurer que chaque requête d’un tableau de bord des insights Adobe Real-Time Customer Data Platform dispose de suffisamment de ressources pour s’exécuter efficacement, l’API effectue le suivi de l’utilisation des ressources en attribuant des emplacements simultanés à chaque requête. Le système peut traiter jusqu’à quatre requêtes simultanées. Par conséquent, quatre emplacements de requête simultanés sont disponibles à tout moment. Les requêtes sont placées dans une file d’attente en fonction des emplacements de simultanéité, puis patientez dans la file d’attente jusqu’à ce que suffisamment d’emplacements de simultanéité soient disponibles.

### Modification, duplication ou suppression d’un widget {#duplicate}

Une fois que vous avez créé un widget, vous pouvez modifier, dupliquer ou supprimer des widgets entiers de votre tableau de bord personnalisé.

>[!TIP]
>
>Pour basculer entre l’un de vos tableaux de bord personnalisés existants, sélectionnez Tableaux de bord dans la barre de navigation de gauche, puis sélectionnez le nom du tableau de bord dans la liste de stock.

Sélectionnez l’icône en forme de crayon (![Une icône en forme de crayon.](/help/images/icons/edit.png)) en haut à droite de votre tableau de bord personnalisé pour passer en mode de modification.

![Un tableau de bord personnalisé avec l’icône en forme de crayon mise en surbrillance.](./images/user-defined-dashboards/edit-mode.png)

Sélectionnez ensuite les ellipses situées en haut à droite du widget que vous souhaitez modifier, copier ou supprimer. Sélectionnez l’action appropriée dans le menu déroulant.

![Un widget dans un tableau de bord personnalisé avec les ellipses et le widget Dupliquer en surbrillance.](./images/user-defined-dashboards/duplicate.png)

>[!NOTE]
>
>La duplication vous permet de personnaliser les attributs d’un insight afin de créer un widget unique sans avoir à partir de zéro. Si vous dupliquez un widget, il apparaît dans votre tableau de bord personnalisé. Vous pouvez ensuite sélectionner les ellipses de votre nouveau widget, suivies de **[!UICONTROL Modifier]**, pour personnaliser vos informations.

## Étapes suivantes et ressources supplémentaires

En lisant ce document, vous comprenez mieux comment créer un tableau de bord personnalisé et comment créer, modifier et mettre à jour des widgets personnalisés pour ce tableau de bord.

Pour découvrir les mesures et visualisations préconfigurées disponibles pour les tableaux de bord [profils](./guides/profiles.md#standard-widgets), [segments](./guides/audiences.md#standard-widgets) et [destinations](./guides/destinations.md#standard-widgets), consultez la liste des widgets standard dans leur documentation respective.

Pour mieux comprendre les tableaux de bord en Experience Platform, regardez la vidéo suivante :

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)

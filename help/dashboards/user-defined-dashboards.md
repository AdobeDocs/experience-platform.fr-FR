---
title: Tableaux de bord définis par l’utilisateur
description: Découvrez comment créer et gérer des tableaux de bord personnalisés dans lesquels vous pouvez créer, ajouter et modifier des widgets personnalisés pour visualiser des mesures clés.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: bf2b35e3366c71c51c58b6257cc55f7c9b0cd9c7
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 0%

---

# Tableaux de bord définis par l’utilisateur (bêta)

>[!IMPORTANT]
>
>La fonctionnalité de tableaux de bord définis par l’utilisateur est en version bêta. Ses fonctionnalités et sa documentation peuvent faire l’objet de modifications.

Les tableaux de bord Adobe Experience Platform vous permettent d’accélérer les insights et de personnaliser la visualisation par le biais de la fonctionnalité de tableaux de bord définis par l’utilisateur. Cette fonctionnalité vous permet de créer et de gérer des tableaux de bord personnalisés dans lesquels vous pouvez créer, ajouter et modifier des widgets personnalisés pour visualiser les mesures clés pertinentes pour votre entreprise.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Créer des tableaux de bord personnalisés

Pour créer un tableau de bord personnalisé, accédez d’abord à l’inventaire du tableau de bord. Sélectionner **[!UICONTROL Tableaux de bord]** dans le volet de navigation de gauche de l’interface utilisateur de Platform, suivi de **[!UICONTROL Créer un tableau de bord]**.

![L’inventaire des tableaux de bord avec les tableaux de bord dans le volet de navigation de gauche et &quot;Créer un tableau de bord&quot; est mis en surbrillance.](./images/user-defined-dashboards/create-dashboard.png)

Avant d’ajouter un tableau de bord personnalisé, l’inventaire des tableaux de bord est vide et affiche le message &quot;Aucun tableau de bord trouvé&quot;.  (Jeton récupéré) s’affiche.  Une fois créés, tous vos tableaux de bord définis par l’utilisateur sont répertoriés dans l’inventaire des tableaux de bord.

Le [!UICONTROL Créer un tableau de bord] s’affiche. Saisissez un nom explicite et convivial pour la collection de widgets que vous souhaitez créer, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Boîte de dialogue Créer un tableau de bord .](./images/user-defined-dashboards/create-dashboard-dialog.png)

Le tableau de bord vierge nouvellement créé s’affiche avec le nom de votre choix dans le coin supérieur gauche de la vue.

## Création d’un widget

Dans la nouvelle vue de tableau de bord, sélectionnez **[!UICONTROL Ajouter un nouveau widget]** pour lancer le processus de création du widget.

![Le nouveau tableau de bord vide avec l’option Ajouter un nouveau widget mise en surbrillance.](./images/user-defined-dashboards/add-new-widget.png)

### Compositeur de widgets

L’espace de travail du compositeur de widgets s’affiche. Ensuite, sélectionnez **[!UICONTROL Sélectionner des données]** pour choisir le modèle de données à partir duquel ajouter des attributs à vos widgets.

![Espace de travail du compositeur de widgets.](./images/user-defined-dashboards/widget-composer.png)

Le [!UICONTROL Sélectionner des données] s’affiche. Sélectionnez un modèle de données dans la colonne de gauche pour afficher la liste de tous les tableaux disponibles.

>[!NOTE]
>
>Actuellement, les tableaux de bord définis par l’utilisateur ne prennent en charge que le modèle de données de profil. D’autres options seront prises en charge.

![La boîte de dialogue Sélectionner les données .](./images/user-defined-dashboards/select-data-dialog.png)

La liste d’aperçu fournit des détails sur les tables contenues dans le modèle de données. Le tableau ci-dessous fournit une description des champs de la colonne et de leurs valeurs potentielles.

| Champ de colonne | Description |
|---|---|
| [!UICONTROL Titre] | Nom de la table. |
| [!UICONTROL Type de tableau] | Type de tableau. Les types potentiels sont les suivants : `fact`, `dimension`, et `none`. |
| [!UICONTROL Recherches] | Le nombre de tables jointes à la table choisie. |

Sélectionner **[!UICONTROL Suivant]** pour confirmer votre choix du modèle de données. La vue suivante affiche la liste des tableaux disponibles dans le rail de gauche. Sélectionnez un tableau pour afficher une ventilation complète des données contenues dans le tableau sélectionné.

Le [!UICONTROL Aperçu] contient des onglets pour [!UICONTROL Exemples d’enregistrements] et [!UICONTROL Attributs]. Le [!UICONTROL Exemples d’enregistrements] fournit un sous-ensemble des enregistrements de la table sélectionnée dans une vue tabulée. Le [!UICONTROL Attributs] fournit le nom de l’attribut, le type de données et la table source pour chaque attribut associé au tableau sélectionné.

Sélectionnez un tableau dans la liste disponible dans le rail de gauche pour fournir des données à votre widget et sélectionnez **[!UICONTROL Sélectionner]** pour revenir au compositeur de widget.

![La boîte de dialogue de sélection des données avec la sélection mise en surbrillance.](./images/user-defined-dashboards/select-a-table.png)

Le compositeur de widgets est maintenant renseigné avec les données du tableau de votre choix.

Le modèle de données et le tableau actuellement sélectionné sont affichés dans la partie supérieure du rail de gauche, et les attributs disponibles pour créer votre widget sont répertoriés dans la colonne Attributs.

![Widget renseigné avec des données dans le compositeur de widgets.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Vous pouvez modifier le modèle de données sélectionné en cliquant sur l’icône représentant un crayon (![Icône Crayon.](./images/user-defined-dashboards/edit-icon.png)) dans le rail de gauche.

Sélectionnez l’icône d’ajout (./images/user-defined-dashboards/add-icon.png) en regard d’un nom d’attribut pour ajouter un attribut à l’axe X ou Y.

![Le compositeur de widgets avec la liste déroulante d’icône d’ajout mise en surbrillance pour ajouter des attributs à un axe de widget.](./images/user-defined-dashboards/attributes-dropdown.png)

Sélectionnez ensuite le type de graphique ou de graphique dans le [!UICONTROL Marques] pour générer une visualisation d’aperçu des paramètres actuels de votre widget. Dans le [!UICONTROL Propriétés] sur le côté droit de l’écran, saisissez un nom pour le widget dans le champ [!UICONTROL Titre du widget] Champ de texte.

![Le compositeur de widgets avec la liste déroulante Marques et le champ de texte Titre du widget sont mis en surbrillance.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Lorsque vous êtes satisfait de votre widget, sélectionnez **[!UICONTROL Enregistrer]**. Une icône de coche sous le nom du widget indique que le widget a été enregistré.

>[!NOTE]
>
>L’enregistrement dans le compositeur de widgets enregistre le widget localement dans votre tableau de bord. Si vous quittez l’éditeur de tableau de bord sans enregistrer le tableau de bord, le widget n’est pas enregistré dans le tableau de bord.

![Nouvelle confirmation d’enregistrement du widget.](./images/user-defined-dashboards/save-confirmation.png)

Sélectionner **[!UICONTROL Annuler]** pour revenir à votre tableau de bord personnalisé.

![compositeur de widgets avec un exemple de widget créé.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Sélectionnez l’icône de paramètre en regard du nom du tableau de bord pour afficher les détails sur sa création. Vous pouvez modifier le nom de votre tableau de bord dans la boîte de dialogue qui s’affiche.

Les widgets peuvent être réorganisés et redimensionnés dans cet espace de travail. Sélectionner **[!UICONTROL Enregistrer]** pour conserver le nom et la mise en page de votre tableau de bord.

![Le tableau de bord défini par l’utilisateur avec un widget personnalisé et le bouton d’enregistrement mis en surbrillance.](./images/user-defined-dashboards/user-defined-dashboard.png)

## Étapes suivantes

En lisant ce document, vous comprenez mieux comment créer un tableau de bord personnalisé et comment créer, modifier et mettre à jour des widgets personnalisés pour ce tableau de bord.

Pour découvrir les mesures et visualisations préconfigurées disponibles pour la variable [profils](./guides/profiles.md#standard-widgets), [segments](./guides/segments.md#standard-widgets), et [destinations](./guides/destinations.md#standard-widgets) pour les tableaux de bord, consultez la liste des widgets standard dans leur documentation respective.

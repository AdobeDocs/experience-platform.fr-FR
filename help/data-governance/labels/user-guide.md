---
keywords: Experience Platform;accueil;rubriques populaires;gouvernance des données;libellé d’utilisation des données;policy service;guide de l’utilisateur des libellés d’utilisation des données
solution: Experience Platform
title: Gestion des libellés d’utilisation des données dans l’interface utilisateur
description: Ce guide détaille la procédure d’utilisation des libellés d’utilisation des données dans l’interface utilisateur d’Adobe Experience Platform.
exl-id: aa44d5cc-416a-4ef2-be14-b4f32aec162c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 71%

---

# Gestion des libellés d’utilisation des données dans l’interface utilisateur {#user-guide}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_description"
>title="Gouverner l’utilisation des données dans Experience Platform"
>abstract="<h2>Description</h2><p>La structure de gouvernance des données dans Experience Platform vous permet de libeller les attributs et les schémas en fonction des restrictions d’utilisation des données et de configurer des politiques qui identifient et respectent ces restrictions pour des actions marketing spécifiques.</p>"

Ce guide d’utilisation détaille la procédure d’utilisation des libellés d’utilisation des données dans l’interface utilisateur [!DNL Experience Platform].

## Gérer les libellés {#manage-labels}

Pour appliquer des libellés à vos données, vous avez besoin de l’autorisation **[!UICONTROL Manage Usage Labels]** pour les utiliser sur le sandbox de production par défaut appelé « prod ». Pour créer un libellé personnalisé, vous devez également disposer de droits d’administration sur le profil de produit. Chaque organisation ne dispose que d’une seule liste de libellés applicables. Vous **ne pouvez pas** supprimer les libellés. Vous pouvez plutôt les supprimer des jeux de données ou des champs auxquels ils sont appliqués.

Veuillez consulter le guide sur la façon de [configurer des autorisations](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=fr) ou la [vue d’ensemble du contrôle d’accès](../../access-control/home.md) pour plus d’informations sur l’attribution d’une autorisation. Si vous n’avez pas accès à Admin Console de votre organisation, contactez l’administrateur ou l’administratrice de cette dernière.

## Gérer les libellés au niveau du schéma

Vous pouvez ajouter des libellés directement à un schéma ou à des champs de ce schéma. Tous les champs appliqués au niveau du schéma se propagent à tous les jeux de données basés sur ce schéma.

>[!NOTE]
>
>Si vos politiques d’utilisation des données ont été créées avant l’attribution d’une étiquette à votre champ, vous pouvez rencontrer une boîte de dialogue de violation de la politique de gouvernance lorsque vous appliquez des étiquettes à votre nouveau schéma. Cette boîte de dialogue indique que l’application de ce libellé enfreindra une politique d’utilisation existante. Utilisez le diagramme de parenté des données pour comprendre quelles autres modifications de configuration doivent être apportées avant de pouvoir ajouter le libellé à votre champ de schéma.
>
>![Boîte de dialogue Non-respect des règles de gouvernance des données détecté avec le résumé des violations et le diagramme de traçabilité des données en surbrillance.](../images/labels/policy-violation-dialog.png)
>
>Pour plus d’informations sur les violations de politique[&#x200B; consultez la &#x200B;](../enforcement/auto-enforcement.md#data-usage-violation) documentation sur les violations de politique d’utilisation des données .

Pour gérer les libellés d’utilisation des données au niveau du schéma, vous devez sélectionner un schéma existant ou en créer un nouveau. Après vous être connecté à Adobe Experience Platform, sélectionnez **[!UICONTROL Schemas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail **[!UICONTROL Schemas]**. Cette page répertorie tous les schémas créés appartenant à votre organisation, ainsi que des détails utiles relatifs à chaque schéma.

![Interface utilisateur d’Adobe Experience Platform avec l’onglet Schéma en surbrillance.](../images/labels/schema-tab.png)

La section suivante décrit les étapes à suivre pour créer un schéma auquel appliquer des libellés. Si vous souhaitez modifier les libellés d’un schéma existant, sélectionnez le schéma dans la liste et passez à l’étape [Ajouter des libellés d’utilisation des données au schéma](#add-labels).

### Créer un schéma

Pour créer un schéma, sélectionnez **[!UICONTROL Create schema]** dans le coin supérieur droit de l’espace de travail **[!UICONTROL Schemas]**. Veuillez consulter le guide sur [comment créer un schéma à l’aide de l’éditeur de schémas](../../xdm/tutorials/create-schema-ui.md#create) pour obtenir des instructions complètes. Vous pouvez également [créer un schéma à l’aide de l’API Schema Registry](../../xdm/tutorials/create-schema-api.md) si nécessaire.

### Ajouter des libellés d’utilisation des données à un schéma {#add-labels-to-schema}

Après avoir créé un nouveau schéma ou sélectionné un schéma existant dans la liste de l’onglet [!UICONTROL Browse] de l’espace de travail [!UICONTROL Schemas] , sélectionnez un champ de votre schéma dans l’éditeur de schémas. Dans la barre latérale [!UICONTROL Field properties], sélectionnez **[!UICONTROL Apply Access and Data Governance Labels]**.

![L’onglet Structure de l’espace de travail Schémas affiche la visualisation de votre schéma avec Appliquer l’accès et les étiquettes de gouvernance des données en surbrillance.](../images/labels/schema-label-governance.png)

Une boîte de dialogue s’affiche, vous permettant d’appliquer et de gérer des libellés d’utilisation des données au niveau du schéma et du champ. Veuillez consulter le tutoriel XDM pour obtenir des instructions complètes sur [comment ajouter ou modifier des libellés d’utilisation des données pour les schémas XDM](../../xdm/tutorials/labels.md#select-schema-field).

### Ajouter des libellés d’utilisation des données à un jeu de données spécifique {#add-labels-to-dataset}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataGovernance_instructions"
>title="Instructions"
>abstract="<ol><li>Sélectionnez <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/user-guide.html?lang=fr">Jeux de données</a> dans le volet de navigation de gauche, puis cliquez sur le jeu de données dont vous souhaitez restreindre les données.</li><li>Dans la vue des détails du jeu de données, sélectionnez l’onglet <b>Gouvernance des données</b>.</li><li>Sélectionnez les champs du jeu de données que vous souhaitez restreindre, puis cliquez sur <b>Modifier les libellés de gouvernance</b> pour libeller les données en fonction des restrictions d’utilisation.</li><li>Une fois les données libellées, sélectionnez <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=fr">Stratégies</a> dans le volet de navigation de gauche et cliquez sur <b>Créer une stratégie</b>.</li><li>Créez une <a href="https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/user-guide.html?lang=fr#create-governance-policy">Stratégie de gouvernance des données</a>, puis sélectionnez les libellés d’utilisation des données que la stratégie appliquera à la stratégie.</li><li>Sélectionnez la ou les actions marketing que la stratégie refusera pour toutes les données contenant ces libellés. Une fois la stratégie créée, sélectionnez-la dans la liste et activez-la à l’aide du bouton (bascule) du rail de droite.</li><li>Pour chaque politique activée, Experience Platform empêche l’utilisation des données contenant les libellés spécifiés pour la ou les actions marketing définies. Cette implémentation a lieu automatiquement lorsque vous tentez d’activer des données libellées vers une destination avec des actions marketing associées (cas d’utilisation).</li></ol>"

>[!IMPORTANT]
>
>Les libellés ne peuvent plus être appliqués aux champs au niveau du jeu de données. Ce workflow a été abandonné au profit de l’application des libellés au niveau du schéma. Les libellés précédemment appliqués au niveau de l’objet du jeu de données seront toujours pris en charge par l’interface utilisateur d’Experience Platform jusqu’au 31 mai 2024. Pour garantir la cohérence de vos libellés sur tous les schémas, les libellés précédemment attachés aux champs au niveau du jeu de données doivent être migrés au niveau du schéma par vous-même au cours de l’année à venir. Consultez la documentation pour obtenir des instructions sur la [Migration des libellés précédemment appliqués du jeu de données au niveau du schéma](../e2e.md#migrate-labels).

Les libellés peuvent être appliqués à l’ensemble du jeu de données à partir de l’onglet **[!UICONTROL Data Governance]** de l’espace de travail **[!UICONTROL Datasets]** . L’espace de travail vous permet de gérer les libellés d’utilisation des données au niveau du jeu de données.

![Onglet [!UICONTROL Data Governance] de l’espace de travail [!UICONTROL Datasets] avec Gouvernance des données en surbrillance.](../images/labels/dataset-governance.png)

Pour modifier les libellés d’utilisation des données au niveau du jeu de données, commencez par sélectionner l’icône en forme de crayon (![une icône en forme de crayon.](/help/images/icons/edit.png)) dans la ligne du nom du jeu de données.

![Onglet [!UICONTROL Data Governance] de l’espace de travail [!UICONTROL Datasets] avec l’icône de modification en forme de crayon en surbrillance.](../images/labels/dataset-level-edit.png)

La boîte de dialogue **[!UICONTROL Edit Governance Labels]** s’ouvre. Dans la boîte de dialogue, cochez les cases en regard des libellés que vous souhaitez appliquer au jeu de données. Souvenez-vous que ces libellés seront hérités par tous les champs du jeu de données. L’en-tête **[!UICONTROL Applied Labels]** est mis à jour au fur et à mesure que vous cochez chaque case, affichant les libellés que vous avez choisis. Une fois que vous avez sélectionné les libellés de votre choix, sélectionnez **[!UICONTROL Save Changes]**.

![La boîte de dialogue Modifier les libellés de gouvernance affiche les cases à cocher des libellés et Enregistrer les modifications en surbrillance.](../images/labels/apply-labels-dataset.png)

L’espace de travail **[!UICONTROL Data Governance]** réapparaît, affichant les libellés que vous avez appliqués au niveau du jeu de données dans la ligne initiale du tableau. Vous pouvez également voir les libellés, indiqués par des cartes individuelles, hérités de chacun des champs du jeu de données.

![Onglet [!UICONTROL Data Governance] de l’espace de travail [!UICONTROL Datasets] avec les libellés appliqués au niveau du jeu de données et les libellés hérités des champs du jeu de données mis en surbrillance.](../images/labels/applied-dataset-labels.png)

### Suppression des libellés dʼun jeu de données {#remove-labels-from-a-dataset}

Les libellés ajoutés au niveau du jeu de données comportent un « x » en regard de leur carte. Vous pouvez ainsi supprimer les libellés du jeu de données entier. Les libellés hérités en regard de chaque champ ne comportent pas de « x » et apparaissent grisés. Ces **libellés hérités sont en lecture seule**, ils ne peuvent donc pas être supprimés ou modifiés au niveau du champ.

<!-- ## View labels at the dataset field level {#view-labels-at-dataset-field-level} -->

<!-- To view labels inherited by the dataset from the schema level, select **[!UICONTROL Datasets]** to navigate to the datasets workspace and select the relevant dataset from the list. 

![The Browse tab of the Datasets workspace with Datasets highlighted in the left sidebar.](../images/labels/dataset-navigation.png)

Next, select the **[!UICONTROL Data Governance]** tab to show the labels that have been applied to the dataset. You can also see that the labels are inherited down to each of the fields within the dataset.

![Dataset Labels inherited by fields](../images/labels/dataset-labels-applied.png)

The inherited labels beside each field do not have an "x" next to them and appear "greyed out" with no ability to remove or edit. This is because **inherited fields are read-only**, meaning they cannot be removed at the field level. -->

<!--Beleive can cut above here  -->

Le bouton (bascule) **[!UICONTROL Show Inherited Labels]** est activé par défaut, ce qui vous permet de voir les libellés hérités du schéma à ses champs. Si vous désactivez cette option, les libellés hérités du jeu de données sont masqués.

![L’onglet Gouvernance des données de l’espace de travail des jeux de données affiche en surbrillance le bouton (bascule) Afficher les libellés hérités.](../images/labels/inherited-labels.png)

<!-- Labels applied to the dataset appear in read-only form within the **[!UICONTROL Data Governance]** view for that dataset. 

![The Data Governance tab of the Datasets workspace with labels highlighted.](../images/labels/read-only-governance-labels.png) -->

>[!NOTE]
>
>Les libellés appliqués avant que la fonction d’étiquetage du jeu de données ne soit obsolète peuvent être supprimés du jeu de données. Pour ce faire, recherchez le jeu de données approprié et sélectionnez l’icône d’annulation sur le libellé.
>![L’onglet Gouvernance des données de l’espace de travail des jeux de données affiche en surbrillance un libellé pouvant être supprimé.](../images/labels/remove-governance-labels.png)
>Consultez la documentation pour obtenir des instructions sur la [Migration des libellés précédemment appliqués du jeu de données au niveau du schéma](../e2e.md#migrate-labels).

## Gérer les libellés personnalisés {#manage-custom-labels}

>[!CONTEXTUALHELP]
>id="platform_governance_createlabels"
>title="Créer des libellés"
>abstract="Les libellés vous permettent de classer les jeux de données et les champs en fonction des politiques d’utilisation qui s’appliquent à ces données. Experience Platform fournit un ensemble standard de libellés que vous pouvez utiliser, mais vous pouvez également créer des libellés personnalisés spécifiques à votre organisation."

Vous pouvez créer vos propres libellés d’utilisation personnalisés dans l’espace de travail **[!UICONTROL Policies]** de l’interface utilisateur de [!DNL Experience Platform]. Sélectionnez **[!UICONTROL Policies]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Labels]** pour afficher une liste des libellés existants. À partir de là, sélectionnez **[!UICONTROL Create label]**.

![L’espace de travail Politiques affiche en surbrillance l’option de création d’une politique.](../images/labels/create-label-btn.png)

La boîte de dialogue **[!UICONTROL Create label]** s’affiche. À partir de là, renseignez les informations suivantes pour le nouveau libellé :

* **[!UICONTROL Name]** : identifiant unique du libellé. Cette valeur est utilisée à des fins de recherche et doit donc être courte et concise.
* **[!UICONTROL Friendly name]** : un nom d’affichage convivial pour ce libellé.
* **[!UICONTROL Description]** : (facultatif) description du libellé pour fournir un contexte supplémentaire.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Create]**.

![La boîte de dialogue Créer un libellé de l’espace de travail Politiques est mise en surbrillance.](../images/labels/create-label-dialog.png)

La boîte de dialogue se ferme et le nouveau libellé personnalisé apparaît dans la liste, sous l’onglet **[!UICONTROL Labels]** .

![L’onglet Libellés de l’espace de travail Politiques affiche en surbrillance le nouveau libellé personnalisé.](../images/labels/label-created.png)

Le libellé peut désormais être sélectionné sous **[!UICONTROL Custom Labels]** lors de la modification des libellés d’utilisation des jeux de données et des champs ou lors de la création de politiques d’utilisation des données.

![La boîte de dialogue Appliquer l’accès et les étiquettes de gouvernance des données affiche en surbrillance les étiquettes personnalisées.](../images/labels/add-custom-label.png)

## Étapes suivantes

Maintenant que vous avez ajouté des libellés d’utilisation des données aux niveaux du jeu de données et du champ, vous pouvez commencer à ingérer des données dans [!DNL Experience Platform]. Pour en savoir plus, commencez par lire la [documentation sur l’ingestion de données](../../ingestion/home.md).

Désormais, vous pouvez également définir des politiques d’utilisation des données en fonction des libellés que vous avez appliqués. Pour plus d’informations, consultez la [présentation des politiques d’utilisation des données](../policies/overview.md).

<!-- The workflow of this video is now outdated. This can be enabled once the video has been updated

## Additional resources

The following video is intended to support your understanding of Data Governance, and outlines how to apply labels to a dataset and individual fields.

>[!VIDEO](https://video.tv.adobe.com/v/3422795?captions=fre_fr&quality=12&enable10seconds=on&speedcontrol=on) -->

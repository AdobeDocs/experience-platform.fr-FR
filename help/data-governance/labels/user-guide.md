---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de l’utilisateur des étiquettes d’utilisation des données
topic: labels
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 0%

---


# Guide de l’utilisateur des étiquettes d’utilisation des données

Ce guide d’utilisateur décrit les étapes à suivre pour utiliser des libellés d’utilisation des données (également appelés libellés DULE) dans l’interface [!DNL Experience Platform] utilisateur. Avant d&#39;utiliser le guide, veuillez consulter l&#39;aperçu [de la gouvernance des](../home.md) données pour une présentation plus robuste du cadre DULE.

## Gestion des étiquettes d’utilisation des données au niveau du jeu de données

Pour gérer les étiquettes d’utilisation des données au niveau des jeux de données, vous devez sélectionner un jeu de données existant ou en créer un nouveau. Après vous être connecté à l’Adobe Experience Platform, sélectionnez **[!UICONTROL Datasets]** dans le volet de navigation de gauche pour ouvrir l’espace de travail _Datasets_ . Cette page liste tous les jeux de données créés appartenant à votre organisation, ainsi que des détails utiles relatifs à chaque jeu de données.

![Onglet Jeu de données dans l’espace de travail de données](../images/labels/datasets.png)

La section suivante décrit la procédure à suivre pour créer un nouveau jeu de données auquel appliquer des étiquettes. Si vous souhaitez modifier les étiquettes d&#39;un jeu de données existant, sélectionnez le jeu de données dans la liste et passez à l&#39;avant pour [ajouter des étiquettes d&#39;utilisation des données au jeu](#add-labels)de données.

### Créer un jeu de données

>[!NOTE]
>
>Dans cet exemple, un jeu de données est créé à l’aide d’un schéma de modèle de données d’expérience (XDM) préconfiguré. Pour plus d&#39;informations sur les schémas XDM, consultez la présentation [et les](../../xdm/home.md) bases de la composition [des schémas de](../../xdm/schema/composition.md)XDM System.

Pour créer un jeu de données, cliquez sur **[!UICONTROL Créer un jeu de données]** dans le coin supérieur droit de l’espace de travail _[!UICONTROL DataSet]_.

![](../images/labels/create_dataset.png)

L’écran _[!UICONTROL Créer un jeu de données]_s’affiche. A partir de là, cliquez sur**[!UICONTROL  Créer un jeu de données à partir du Schéma ]**.

![Créer un jeu de données à partir d&#39;un Schéma](../images/labels/dataset_create.png)

L&#39;écran _[!UICONTROL Sélectionner un Schéma]_s&#39;affiche, qui liste tous les schémas disponibles que vous pouvez utiliser pour créer un jeu de données. Cliquez sur le bouton radio en regard d’un schéma pour le sélectionner. La section_[!UICONTROL  Schémas]_ sur le côté droit affiche des détails supplémentaires sur le schéma sélectionné. Once you have selected a schema, click **[!UICONTROL Next]**.

![Sélectionner un Schéma de données](../images/labels/dataset_schema.png)

L’écran _Configurer un jeu de données_ s’affiche. Indiquez un **nom** (obligatoire) et une **description** (facultative, mais recommandée) pour votre nouveau jeu de données, puis cliquez sur **[!UICONTROL Terminer]**.

![Configurer un jeu de données avec le nom et la description](../images/labels/dataset_configure.png)

La page Activité _[!UICONTROL des]_jeux de données s&#39;affiche, affichant des informations sur le jeu de données nouvellement créé. Dans cet exemple, le jeu de données est nommé &quot;Membres de fidélité&quot;. Par conséquent, la barre de navigation supérieure affiche_ Jeux de données > Membres _de fidélité.

![Page Activité des jeux de données](../images/labels/dataset_activity.png)

### Ajouter les étiquettes d’utilisation des données au jeu de données {#add-labels}

Après avoir créé un nouveau jeu de données ou sélectionné un jeu de données existant dans la liste de l&#39;espace de travail _[!UICONTROL Datasets]_, cliquez sur**[!UICONTROL  Data Governance ]**pour ouvrir l&#39;espace de travail_[!UICONTROL  Data Governance]_ . L’espace de travail vous permet de gérer les étiquettes d’utilisation des données au niveau du jeu de données et au niveau du champ.

![Onglet Gouvernance des données de jeux de données](../images/labels/dataset_data_governance.png)

Pour modifier les libellés d’utilisation des données au niveau du jeu de données, cliquez sur l’icône représentant un crayon en regard du nom du jeu de données.

![Modification des étiquettes de niveau jeu de données](../images/labels/dataset_labels_edit_button.png)

La boîte de dialogue _[!UICONTROL Modifier les étiquettes]_de gouvernance s&#39;ouvre. Dans la boîte de dialogue, cochez les cases en regard des étiquettes que vous souhaitez appliquer au jeu de données. N’oubliez pas que ces étiquettes seront héritées par tous les champs du jeu de données. L&#39;en-tête Libellés__ appliqués se met à jour lorsque vous cochez chaque case, en affichant les étiquettes que vous avez sélectionnées. Une fois que vous avez sélectionné les étiquettes de votre choix, cliquez sur **[!UICONTROL Enregistrer les modifications]**.

<img alt="Appliquer les étiquettes de gouvernance au niveau des jeux de données" src="../images/labels/apply-labels-dataset.png" width="700"><br>

L’espace de travail _[!UICONTROL Data Governance]_réapparaît, affichant les étiquettes que vous avez appliquées au niveau du jeu de données. Vous pouvez également constater que les étiquettes sont héritées jusqu’à chacun des champs du jeu de données.

![Étiquettes des jeux de données héritées par les champs](../images/labels/dataset_inherited_labels.png)

Un &quot;x&quot; apparaît en regard des libellés au niveau du jeu de données, ce qui vous permet de supprimer les libellés. Les libellés hérités à côté de chaque champ n’ont pas de &quot;x&quot; en regard d’eux et apparaissent &quot;grisés&quot; sans possibilité de suppression ou de modification. En effet, les champs **hérités sont en lecture seule**, ce qui signifie qu’ils ne peuvent pas être supprimés au niveau du champ.

La bascule **[!UICONTROL Afficher les étiquettes]** héritées est activée par défaut, ce qui vous permet de voir tous les libellés hérités du jeu de données vers ses champs. La désactivation masque les étiquettes héritées dans le jeu de données.

![Masquer les étiquettes héritées](../images/labels/hide_inherited_labels.png)

## Gestion des étiquettes d’utilisation des données au niveau du champ de jeu de données

En poursuivant le processus d’ [ajout et de modification des libellés d’utilisation des données au niveau](#add-labels)du jeu de données, vous pouvez également gérer des libellés de niveau champ dans l’espace de travail _[!UICONTROL de gouvernance]_des données pour ce jeu de données.

Pour appliquer des étiquettes d’utilisation de données à un champ individuel, cochez la case en regard du nom du champ, puis cliquez sur **[!UICONTROL Modifier les étiquettes]** de gouvernance.

![Modifier les étiquettes de champs](../images/labels/fields_single_field.png)

La boîte de dialogue _[!UICONTROL Modifier les étiquettes]_de gouvernance s&#39;affiche. La boîte de dialogue affiche les en-têtes présentant les champs sélectionnés, les étiquettes appliquées et les étiquettes héritées. Notez que les étiquettes héritées (C2 et C5) sont grisées dans la boîte de dialogue. Il s’agit d’étiquettes en lecture seule héritées du niveau du jeu de données et ne peuvent donc être modifiées qu’au niveau du jeu de données.

<img alt="Modifier les étiquettes de gouvernance pour un champ individuel" src="../images/labels/field-label-inheritance.png" width="700"><br>

Sélectionnez des étiquettes de niveau champ en cochant la case en regard de chaque étiquette que vous souhaitez utiliser. Lorsque vous sélectionnez des libellés, l’en-tête Libellés __appliqués se met à jour pour afficher les libellés appliqués aux champs affichés dans l’en-tête Champs__ sélectionnés. Une fois que vous avez terminé de sélectionner des étiquettes au niveau des champs, cliquez sur **[!UICONTROL Enregistrer les modifications]**.

<img alt="Appliquer des étiquettes au niveau des champs" src="../images/labels/apply-labels-field.png" width="700"><br>

L&#39;espace de travail _[!UICONTROL Data Governance]_réapparaît, qui affiche désormais les étiquettes de niveau champ sélectionnées dans la ligne en regard du nom du champ. Notez que l’étiquette de niveau champ est associée à un &quot;x&quot;, ce qui vous permet de supprimer l’étiquette.

![Champ présentant les libellés de niveau champ](../images/labels/fields_show_field_level_labels.png)

Vous pouvez répéter ces étapes pour continuer à ajouter et à modifier des libellés de niveau champ pour d’autres champs, y compris la sélection de plusieurs champs pour appliquer simultanément des libellés de niveau champ.

![Sélectionnez plusieurs champs pour appliquer simultanément des libellés de niveau champ.](../images/labels/fields_select_multiple.png)

Il est important de se souvenir que l&#39;héritage passe du niveau supérieur au niveau inférieur uniquement (jeu de données → champs), ce qui signifie que les étiquettes appliquées au niveau du champ ne sont pas propagées à d&#39;autres champs ou jeux de données.

## Étapes suivantes

Maintenant que vous avez ajouté des étiquettes d’utilisation des données au niveau du jeu de données et du champ, vous pouvez commencer à assimiler des données dans [!DNL Experience Platform]. Pour en savoir plus, début en lisant la documentation [sur l&#39;assimilation des](../../ingestion/home.md)données.

Vous pouvez également désormais définir des stratégies d’utilisation des données en fonction des étiquettes que vous avez appliquées. Pour plus d’informations, voir la présentation [des stratégies d’utilisation des](../policies/overview.md)données.

## Ressources supplémentaires

La vidéo suivante est destinée à vous aider à comprendre [!DNL Data Governance]comment appliquer des étiquettes à un jeu de données et à des champs individuels.

>[!VIDEO](https://video.tv.adobe.com/v/29709?quality=12&enable10seconds=on&speedcontrol=on)

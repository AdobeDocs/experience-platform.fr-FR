---
solution: Experience Platform
title: Guide de l’interface utilisateur d’Audiences
description: Composition d’audience dans l’interface utilisateur de Adobe Experience Platform fournit un espace de travail riche qui vous permet d’interagir avec les éléments de données Profile. L’espace de travail propose des commandes intuitives pour créer et modifier des audiences pour votre organisation.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 13492b90552d16334030792323956ea18ca928dc
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 74%

---

# Guide de l’interface utilisateur de composition d’audience

Composition d’audience fournit un espace de travail pour créer et modifier des audiences à l’aide de blocs utilisés pour représenter différentes actions.

![Interface utilisateur de composition d’audiences.](../images/ui/audience-composition/audience-composition.png)

Pour modifier les détails de la composition, y compris le titre et la description, sélectionnez l’option ![curseur](../images/ui/audience-composition/sliders.png) bouton .

Le **[!UICONTROL Propriétés de composition]** s’affiche. Vous pouvez insérer des détails sur votre composition, y compris le titre et la description, ici.

![La fenêtre contextuelle Propriétés de composition s’affiche.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Si vous le faites **not** Si vous donnez un titre à votre composition, celle-ci aura le titre &quot;Composition&quot; suivi de la date et de l’heure de création par défaut.

Après avoir mis à jour les détails de votre composition, sélectionnez **[!UICONTROL Enregistrer]** pour confirmer ces mises à jour. Le canevas de composition de l’audience réapparaît.

Le canevas de composition de l’audience se compose de quatre types de blocs différents : **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclure]](#exclude-block)**, **[[!UICONTROL Classement]](#rank-block)**, et **[[!UICONTROL Partage]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

Le type de bloc **[!UICONTROL Audience]** permet d’ajouter les sous-audiences de votre choix pour composer votre nouvelle audience plus grande. Par défaut, un bloc **[!UICONTROL Audience]** est inclus dans la partie supérieure du canevas de composition.

Lorsque vous sélectionnez la variable **[!UICONTROL Audience]** bloc, le rail de droite affiche des commandes d’étiquetage de l’audience, d’ajout d’audiences au bloc et de création de règles personnalisées pour le bloc d’audience.

>[!NOTE]
>
>Vous pouvez ajouter des audiences. **ou** créez une règle personnalisée. Ces deux fonctionnalités **cannot** être utilisés ensemble.

![Les détails du bloc Audience s’affichent.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Ajouter une audience] {#add-audience}

Pour ajouter des audiences au bloc Audience . select **[!UICONTROL Ajouter une audience]**.

![Le bouton Ajouter une audience est mis en surbrillance.](../images/ui/audience-composition/add-audience.png)

Une liste d’audiences s’affiche. Sélectionnez les audiences que vous souhaitez inclure, puis **[!UICONTROL Ajouter]** pour les ajouter à votre bloc d’audience.

![Une liste d’audiences s’affiche. Dans cette boîte de dialogue, vous pouvez sélectionner l’audience à ajouter.](../images/ui/audience-composition/select-audience.png)

Les audiences sélectionnées s’affichent maintenant dans le rail de droite lorsque le bloc **[!UICONTROL Audience]** est sélectionné. À partir de là, vous pouvez modifier le type de fusion des audiences combinées.

![Les types de fusion possibles pour les audiences sont mis en surbrillance.](../images/ui/audience-composition/merge-types.png)

| Type de fusion | Description |
| ---------- | ----------- |
| [!UICONTROL Union] | Les audiences sont combinées en une seule audience. Il s’agit de l’équivalent d’une opération OR. |
| [!UICONTROL Intersection] | Les audiences sont combinées, avec seulement les audiences partagées dans **toutes** celles ajoutées. Il s’agit de l’équivalent d’une opération AND. |
| [!UICONTROL Exclure le chevauchement] | Les audiences sont combinées, avec seulement les audiences partagées dans **une, mais pas toutes** celles ajoutées. Il s’agit de l’équivalent d’une opération XOR. |

### [!UICONTROL Créer une règle] {#build-rule}

Pour ajouter une règle personnalisée au bloc Audience, sélectionnez **[!UICONTROL Créer une règle]**.

![Le bouton Créer la règle est mis en surbrillance.](../images/ui/audience-composition/build-rule.png)

Le créateur de segments s’affiche. Vous pouvez utiliser le créateur de segments pour créer une règle personnalisée que l’audience doit suivre. Vous trouverez plus d’informations sur l’utilisation du créateur de segments dans la section [Guide du créateur de segments](./segment-builder.md).

![L’interface utilisateur du créateur de segments s’affiche.](../images/ui/audience-composition/segment-builder.png)

Après avoir ajouté une règle personnalisée, sélectionnez **[!UICONTROL Enregistrer]** pour ajouter la règle à votre audience.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Exclure] {#exclude-block}

Le type de bloc **[!UICONTROL Exclure]** permet d’exclure des sous-audiences ou attributs spécifiés de votre nouvelle audience plus grande.

Pour ajouter un bloc **[!UICONTROL Exclure]**, sélectionnez l’icône **+**, puis **[!UICONTROL Exclure]**.

![L’option Exclure est sélectionnée.](../images/ui/audience-composition/add-exclude-block.png)

Le bloc **[!UICONTROL Exclure]** est ajouté. Lorsque ce bloc est sélectionné, les détails de l’exclusion apparaissent dans le rail de droite. Le libellé du bloc et le type d’exclusion sont inclus. Vous pouvez exclure [par audience](#exclude-audience) ou [par attribut](#exclude-attribute).

![Le bloc Exclure, mettant en surbrillance les deux types d’exclusion disponibles.](../images/ui/audience-composition/exclude.png)

### Exclure par audience {#exclude-audience}

Si vous excluez par audience, vous pouvez sélectionner les audiences à exclure en sélectionnant **[!UICONTROL Ajouter une audience]**.

![Le bouton Ajouter une audience est sélectionné, ce qui vous permet de choisir l’audience que vous souhaitez exclure.](../images/ui/audience-composition/add-excluded-audience.png)

Une liste d’audiences s’affiche. Sélectionnez **[!UICONTROL Ajouter]** pour ajouter les audiences que vous souhaitez exclure à votre bloc d’exclusion.

![Une liste d’audiences s’affiche. Dans cette boîte de dialogue, vous pouvez sélectionner l’audience à ajouter.](../images/ui/audience-composition/select-audience.png)

### Exclure par attribut {#exclude-attribute}

Si vous excluez par attribut, vous pouvez sélectionner les attributs à exclure en sélectionnant l’icône de ![filtre](../images/ui/audience-composition/filter-attribute.png) dans la section **[!UICONTROL Règle d’exclusion]**.

![La section d’attribut est mise en surbrillance, vous indiquant où sélectionner l’attribut à exclure.](../images/ui/audience-composition/exclude-attribute.png)

Une liste d’attributs de profil s’affiche. Sélectionnez le type d’attribut à exclure, puis **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc d’exclusion.

![Une liste d’attributs s’affiche.](../images/ui/audience-composition/select-attribute-exclude.png)

<!-- ## [!UICONTROL Join] {#join-block}

The **[!UICONTROL Join]** block type allows you to add in external audiences from datasets that have not yet been processed by Adobe Experience Platform.

To add a **[!UICONTROL Join]** block, select the **+** icon, followed by **[!UICONTROL Join]**.

![The Join option is selected.](../images/ui/audience-composition/add-join-block.png)

When you select the block, details about the join are shown in the right rail, including the block's label and the option to add audiences to the enrichment dataset.

![The join block is highlighted, including details about the join block.](../images/ui/audience-composition/join.png)

After selecting **[!UICONTROL Add Audience]**, a list of audiences appears. Select the audiences you want to include, followed by **[!UICONTROL Add]** to add them to your join block.

![A list of audiences appears. You can select which audience you want to add from this dialog.](../images/ui/audience-composition/select-audience.png)

Your selected audiences now appear within the right rail when the **[!UICONTROL Join]** block is selected. 

![The audiences that were added as part of the Join are shown.](../images/ui/audience-composition/selected-audiences.png) -->

## [!UICONTROL Classement] {#rank-block}

Le **[!UICONTROL Classement]** le type block permet de classer et de trier les profils en fonction d’un attribut spécifié et d’inclure ces profils de classement dans votre composition.

Pour ajouter un bloc **[!UICONTROL Classement]**, sélectionnez l’icône **+**, puis **[!UICONTROL Classement]**.

![L’option « Classement » est sélectionnée.](../images/ui/audience-composition/add-rank-block.png)

Lorsque vous sélectionnez le bloc, les détails du classement s’affichent dans le rail de droite, notamment le libellé du bloc, l’attribut de classement, l’ordre de classement et un bouton permettant de limiter le nombre de profils à classer.

![Le bloc de classement est mis en surbrillance, ainsi que les détails le concernant.](../images/ui/audience-composition/rank.png)

Pour sélectionner l’attribut par lequel classer les audiences, sélectionnez l’icône de ![filtre](../images/ui/audience-composition/filter-attribute.png).

![L’icône de filtre est mise en surbrillance et indique les éléments à sélectionner pour accéder à l’écran de sélection des attributs de profil.](../images/ui/audience-composition/select-rank-attribute.png)

Une liste d’attributs de profil s’affiche. Dans cette fenêtre contextuelle, vous pouvez sélectionner le type d’attribut selon lequel vous souhaitez classer votre audience. Cliquez sur **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc de classement. Notez que l’attribut sélectionné peut **only** être des nombres.

![Une liste d’attributs s’affiche.](../images/ui/audience-composition/select-attribute-rank.png)

Après avoir sélectionné l’attribut, vous pouvez sélectionner l’ordre de classement. Il s’agit d’un ordre croissant (du plus bas au plus élevé) ou décroissant (du plus élevé au plus bas).

En outre, vous pouvez limiter le nombre d’audiences renvoyées en activant le bouton **[!UICONTROL Ajouter une limite de profil]**. Lorsque ce bouton est activé, vous pouvez définir le nombre maximal d’audiences renvoyées dans le champ **[!UICONTROL Profils inclus]**.

![Le bouton« Ajouter une limite de profil » est mis en surbrillance, ce qui vous permet de limiter le nombre d’audiences renvoyées.](../images/ui/audience-composition/add-profile-limit.png)

## [!UICONTROL Fractionner] {#split-block}

Le type de bloc **[!UICONTROL Fractionner]** vous permet de fractionner votre nouvelle audience en différentes sous-audiences. Vous pouvez fractionner cette audience en fonction d’un pourcentage ou d’un attribut.

Pour ajouter un bloc **[!UICONTROL Fractionner]**, sélectionnez l’icône **+**, puis **[!UICONTROL Fractionner]**.

![L’option « Fractionner » est sélectionnée.](../images/ui/audience-composition/add-split-block.png)

### Fractionner par pourcentage {#split-percentage}

Lors du fractionnement par pourcentage, les audiences sont réparties de manière aléatoire en fonction du nombre de chemins et des pourcentages fournis.

Par exemple, vous pouvez avoir trois chemins, chacun avec un pourcentage de profils différent.

![La répartition en nombre d’audiences et de pourcentages enregistrés s’affiche.](../images/ui/audience-composition/percentages.png)

### Fractionner par attribut {#split-attribute}

Lors du fractionnement par attribut, les audiences sont fractionnées en fonction des attributs fournis. Pour sélectionner l’attribut du fractionnement, sélectionnez le bloc **[!UICONTROL Fractionner]**, puis l’icône de ![filtrage](../images/ui/audience-composition/filter-attribute.png).

![Le bouton de filtrage est sélectionné et indique comment filtrer par attribut.](../images/ui/audience-composition/select-split-attribute.png)

Une liste d’attributs de profil s’affiche. Sélectionnez le type d’attribut, puis **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc de fractionnement.

![Une liste d’attributs s’affiche.](../images/ui/audience-composition/select-attribute-exclude.png)

Après avoir sélectionné l’attribut, vous pouvez choisir les profils qui appartiendront à une sous-audience en ajoutant les valeurs dans le champ **[!UICONTROL Valeurs]**.

![Les valeurs par lesquelles vous souhaitez fractionner les attributs sont ajoutées.](../images/ui/audience-composition/attribute-split-values.png)

En outre, vous pouvez activer le bouton **[!UICONTROL Autres profils]** pour créer une sous-audience composée de tous les profils non sélectionnés.

![Le bouton « Autres profils » est mis en surbrillance.](../images/ui/audience-composition/split-other-profiles.png)

## Publier votre audience

Après avoir composé votre audience, vous pouvez l’enregistrer et la publier en sélectionnant **[!UICONTROL Publier]**.

![Le bouton « Publier » est mis en surbrillance et vous montre comment enregistrer et publier votre audience.](../images/ui/audience-composition/publish.png)

En cas d’erreur lors de la création de l’audience, une alerte s’affiche, vous indiquant comment résoudre le problème.

![Le bouton « Publier » est mis en surbrillance et vous montre comment enregistrer et publier votre audience.](../images/ui/audience-composition/audience-alert.png)

## Étapes suivantes

La composition d’audiences fournit un processus riche qui vous permet de créer des audiences à partir des différents types de blocs. Pour en savoir plus sur d’autres parties de l’interface utilisateur de Segmentation Service, veuillez lire le [Guide d’utilisation de Segmentation Service](./overview.md).

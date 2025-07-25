---
solution: Experience Platform
title: Guide de l’interface utilisateur d’Audiences
description: La Composition d’audience dans l’interface utilisateur d’Adobe Experience Platform fournit un espace de travail riche qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail propose des commandes intuitives pour créer et modifier des audiences pour votre organisation.
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 65a3b5b904a9dfc6a2fbc09ab869e5642e088363
workflow-type: tm+mt
source-wordcount: '2362'
ht-degree: 78%

---

# Guide de l’interface utilisateur de la Composition d’audience

>[!AVAILABILITY]
>
>Pour utiliser cette fonctionnalité, vous devez disposer des autorisations suivantes :
>
>- Gestion des segments
>- Gestion des profils
>- Gestion des politiques de fusion
>
>Vous trouverez plus d’informations sur les autorisations dans Experience Platform dans la [présentation du contrôle d’accès](../../access-control/home.md#permissions).

>[!NOTE]
>
>Ce guide explique comment créer des audiences à l’aide de la Composition d’audience. Pour savoir comment créer des audiences par le biais de définitions de segment à l’aide du Créateur de segments, veuillez lire le [Guide de l’interface utilisateur du Créateur de segments](./segment-builder.md).

La Composition d’audience offre un espace de travail permettant de créer et de modifier des audiences à l’aide de blocs utilisés pour représenter différentes actions.

![Interface utilisateur de la Composition d’audience.](../images/ui/audience-composition/audience-composition.png)

Pour modifier les détails de la composition, y compris le titre et la description, sélectionnez le bouton ![curseur](/help/images/icons/properties.png).

La fenêtre contextuelle **[!UICONTROL Propriétés de la composition]** s’affiche. Vous pouvez insérer ici des détails sur votre composition, y compris le titre et la description.

![La fenêtre contextuelle Propriétés de la composition s’affiche.](../images/ui/audience-composition/composition-properties.png)

>[!NOTE]
>
>Si vous ne donnez **pas** à votre composition un titre, elle aura un titre de « Composition » suivi par la date et l’heure de création par défaut. En outre, chaque composition **doit** possède son propre nom unique.

Après avoir mis à jour les détails de votre composition, sélectionnez **[!UICONTROL Enregistrer]** pour confirmer ces mises à jour. La zone de travail de composition de l’audience réapparaît.

La zone de travail de composition de l’audience se compose de quatre types de blocs différents : **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclure]](#exclude-block)**, **[[!UICONTROL Classement]](#rank-block)** et **[[!UICONTROL Partage]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_audience"
>title="Bloc Audience"
>abstract="Le bloc Audience permet d’ajouter les sous-audiences que vous souhaitez utiliser pour composer votre nouvelle audience."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_merge_types"
>title="Types de fusion"
>abstract="Les types de fusion déterminent le mode de combinaison des sous-audiences sélectionnées. Les valeurs prises en charge sont Union, Intersection et Exclure le chevauchement."

Le type de bloc **[!UICONTROL Audience]** permet d’ajouter les sous-audiences que vous souhaitez utiliser pour composer votre nouvelle audience plus grande. Par défaut, un bloc **[!UICONTROL Audience]** est inclus dans la partie supérieure de la zone de travail de composition.

Lorsque vous sélectionnez le bloc **[!UICONTROL Audience]**, le rail de droite affiche des commandes d’étiquetage de l’audience, d’ajout d’audiences au bloc et de création de règles personnalisées pour le bloc d’audience.

>[!NOTE]
>
>Vous pouvez ajouter des audiences **ou** créer une règle personnalisée. Ces deux fonctionnalités **ne peuvent pas** être utilisées ensemble.

![Les détails du bloc Audience s’affichent.](../images/ui/audience-composition/audience-block.png)

### [!UICONTROL Ajouter une audience] {#add-audience}

Pour ajouter des audiences au bloc Audience : Sélectionnez **[!UICONTROL Ajouter une audience]**.

![Le bouton Ajouter une audience est mis en surbrillance.](../images/ui/audience-composition/select-add-audience.png)

>[!IMPORTANT]
>
>Notez que **seules** les audiences définies à l’aide de la politique de fusion par défaut s’affichent.
>
>En outre, seules les audiences **publiées** créées à l’aide du créateur de segments peuvent être utilisées. Les audiences créées à l’aide de la composition de l’audience et les audiences générées en externe ne sont **pas** disponibles.

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

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rule_builder"
>title="Créateur de segments"
>abstract="Vous pouvez utiliser le créateur de segments pour ajouter une règle personnalisée à votre composition."

Pour ajouter une règle personnalisée au bloc Audience, sélectionnez **[!UICONTROL Créer une règle]**.

![Le bouton Créer une règle est mis en surbrillance.](../images/ui/audience-composition/select-build-rule.png)

Le créateur de segments s’affiche. Vous pouvez utiliser le créateur de segments pour créer une règle personnalisée que l’audience doit suivre. Vous trouverez plus d’informations sur l’utilisation du créateur de segments dans le [Guide du créateur de segments](./segment-builder.md).

![L’interface utilisateur du créateur de segments s’affiche.](../images/ui/audience-composition/segment-builder.png)

Une fois que vous avez ajouté une règle personnalisée, sélectionnez **[!UICONTROL Enregistrer]** pour ajouter la règle à votre audience.

![](../images/ui/audience-composition/custom-rule.png)

## [!UICONTROL Exclure] {#exclude-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude"
>title="Exclure le bloc"
>abstract="Le bloc Exclure permet d’exclure des audiences ou attributs spécifiés de votre composition."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_type"
>title="Type d’exclusion"
>abstract="Vous pouvez exclure les profils appartenant à une audience spécifique (Exclure par audience) ou exclure les profils en fonction d’un attribut spécifique (Exclure par attribut)."

Le type de bloc **[!UICONTROL Exclure]** permet d’exclure une sous-audience ou des attributs spécifiés de votre nouvelle audience plus grande.

Pour ajouter un bloc **[!UICONTROL Exclure]**, sélectionnez l’icône **+**, puis **[!UICONTROL Exclure]**.

![L’option Exclure est sélectionnée.](../images/ui/audience-composition/add-exclude-block.png)

Le bloc **[!UICONTROL Exclure]** est ajouté. Lorsque ce bloc est sélectionné, les détails de l’exclusion apparaissent dans le rail de droite. Le libellé du bloc et le type d’exclusion sont inclus. Vous pouvez exclure [par audience](#exclude-audience) ou [par attribut](#exclude-attribute).

![Le bloc Exclure, mettant en surbrillance les deux types d’exclusion disponibles.](../images/ui/audience-composition/exclude.png)

### Exclure par audience {#exclude-audience}

Si vous excluez par audience, vous pouvez sélectionner l’audience à exclure en sélectionnant **[!UICONTROL Ajouter une audience]**.

![Le bouton [!UICONTROL Ajouter une audience] est sélectionné, ce qui vous permet de choisir l’audience que vous souhaitez exclure.](../images/ui/audience-composition/add-excluded-audience.png)

>[!IMPORTANT]
>
>Seules les audiences **publiées** créées à l’aide du créateur de segments peuvent être utilisées. Les audiences créées à l’aide de la composition de l’audience et les audiences générées en externe ne sont **pas** disponibles.

Une liste d’audiences s’affiche. Sélectionnez **[!UICONTROL Ajouter]** pour ajouter l’audience à exclure à votre bloc d’exclusion.

![Une liste d’audiences s’affiche. Dans cette boîte de dialogue, vous pouvez sélectionner l’audience à ajouter.](../images/ui/audience-composition/select-audience.png)

### Exclure par attribut {#exclude-attribute}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_exclude_attribute"
>title="Exclure par attribut"
>abstract="Lorsque vous excluez par attribut, vous pouvez exclure des profils spécifiques de l’affichage dans votre composition en fonction des attributs sélectionnés."

Si vous excluez par attribut, vous pouvez sélectionner les attributs à exclure en sélectionnant l’icône ![filtre](/help/images/icons/project-edit.png) dans la section **[!UICONTROL Règle d’exclusion]**. L’exclusion de l’attribut vous permet d’exclure tout profil contenant cet attribut de l’audience obtenue.

![La section d’attribut est mise en surbrillance, vous indiquant où sélectionner l’attribut à exclure.](../images/ui/audience-composition/exclude-attribute.png)

Une liste d’attributs de profil s’affiche. Sélectionnez le type d’attribut à exclure, puis **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc d’exclusion.

![Une liste d’attributs s’affiche.](../images/ui/audience-composition/select-attribute-exclude.png)

>[!IMPORTANT]
>
>Lors de l’exclusion par attribut, vous ne pouvez spécifier qu’**une seule valeur** exclure. L’utilisation d’un type de séparateur, tel qu’une virgule ou un point-virgule, entraîne uniquement l’exclusion de cette valeur exacte. Par exemple, la définition de la valeur sur `red, blue` entraîne l’exclusion du terme `red, blue` de l’attribut, mais **pas** l’exclusion du terme `red` ou `blue`.

## [!UICONTROL Enrichir] {#enrich-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich"
>title="Bloc Enrichir"
>abstract="Le bloc Enrichir vous permet d’enrichir votre audience avec des attributs supplémentaires provenant de jeux de données d’Adobe Experience Platform."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_dataset"
>title="Jeu de données d’enrichissement"
>abstract="Le jeu de données d’enrichissement contient les données que vous souhaitez associer à la composition."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_criteria"
>title="Critères d’enrichissement"
>abstract="Les critères d’enrichissement incluent la clé de jointure Source et la clé de jointure du jeu de données d’enrichissement. Ces deux clés réconcilient le jeu de données source et le jeu de données d’enrichissement."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_enrich_attributes"
>title="Attributs d’enrichissement"
>abstract="Les attributs d’enrichissement sont les attributs que vous souhaitez associer à la composition."

>[!IMPORTANT]
>
>Pour l’instant, les attributs d’enrichissement peuvent **uniquement** être utilisés dans des scénarios Adobe Journey Optimizer en aval.

Le type de bloc **[!UICONTROL Enrichir]** vous permet d’enrichir votre audience avec des attributs supplémentaires provenant d’un jeu de données. Vous pouvez utiliser ces attributs dans des cas d’utilisation de personnalisation.

Pour ajouter un bloc **[!UICONTROL Enrichir]**, sélectionnez l’icône **+**, puis **[!UICONTROL Enrichir]**.

![Sélection de l’option [!UICONTROL Enrichir].](../images/ui/audience-composition/add-enrich-block.png)

Le bloc **[!UICONTROL Enrichir]** est ajouté. Lors de la sélection du bloc, les détails de l’enrichissement apparaissent dans le rail de droite. Le libellé du bloc et le jeu de données d’enrichissement sont indiqués.

Pour sélectionner le jeu de données avec lequel enrichir l’audience, sélectionnez l’icône ![Filtrer](/help/images/icons/project-edit.png).

![Le bouton de filtre est mis en surbrillance. Sélectionnez l’icône pour afficher la fenêtre contextuelle [!UICONTROL Sélectionner un jeu de données].](../images/ui/audience-composition/enrich-select-dataset.png)

La fenêtre contextuelle **[!UICONTROL Sélectionner un jeu de données]** s’affiche. Choisissez le jeu de données à enrichir, puis cliquez sur **[!UICONTROL Sélectionner]** pour enrichir le jeu de données.

![Sélection du jeu de données souhaité.](../images/ui/audience-composition/select-dataset.png)

>[!IMPORTANT]
>
>Le jeu de données sélectionné **doit** remplir les critères suivants :
>
>- Le jeu de données **doit** être de type d’enregistrement.
>   - Le jeu de données **ne peut pas** être de type d’événement, être généré par le système ou être marqué pour le profil.
>- La taille du jeu de données **doit** être inférieure ou égale à 1 Go.

La section **[!UICONTROL Critères d’enrichissement]** s’affiche maintenant sur le rail de droite. Dans cette section, vous pouvez sélectionner la **[!UICONTROL clé de jointure source]** et la **[!UICONTROL clé de jointure du jeu de données d’enrichissement]**, qui vous permettent de lier le jeu de données d’enrichissement à l’audience que vous être en train de créer.

![La zone [!UICONTROL Critères d’enrichissement] est mise en surbrillance.](../images/ui/audience-composition/enrichment-criteria.png)

Pour sélectionner la **[!UICONTROL clé de jointure source]**, cliquez sur l’icône ![Filtrer](/help/images/icons/project-edit.png).

La fenêtre contextuelle de **[!UICONTROL Sélection d’un attribut de profil]** s’affiche. Choisissez l’attribut de profil à utiliser comme clé de jointure source, puis cliquez sur **[!UICONTROL Sélectionner]** pour choisir cet attribut comme clé de jointure source.

![L’attribut à utiliser comme clé de jointure source est mis en surbrillance.](../images/ui/audience-composition/select-source-join-key.png)

Pour sélectionner la **[!UICONTROL clé de jointure du jeu de données d’enrichissement]**, cliquez sur l’icône ![Filtrer](/help/images/icons/project-edit.png).

La fenêtre contextuelle **[!UICONTROL Attributs d’enrichissement]** s’affiche. Choisissez l’attribut à utiliser comme clé de jointure du jeu de données d’enrichissement, puis cliquez sur **[!UICONTROL Sélectionner]** pour choisir cet attribut comme clé de jointure de votre jeu de données d’enrichissement.

![L’attribut à utiliser comme clé de jointure du jeu de données d’enrichissement est mis en surbrillance.](../images/ui/audience-composition/select-enrichment-dataset-join-key.png)

Maintenant que vous avez ajouté vos deux clés de jointure, la section **[!UICONTROL Attributs d’enrichissement]** s’affiche. Vous pouvez maintenant ajouter l’attribut avec lequel vous souhaitez optimiser votre audience. Pour ajouter ces attributs, sélectionnez **[!UICONTROL Ajouter un attribut]**.

La fenêtre contextuelle **[!UICONTROL Attributs d’enrichissement]** s’affiche. Vous pouvez sélectionner les attributs du jeu de données pour enrichir votre audience, puis cliquez sur **[!UICONTROL Sélectionner]** pour ajouter les attributs à votre audience.

![Les attributs d’enrichissement à ajouter sont mis en surbrillance.](../images/ui/audience-composition/select-enrichment-attribute.png)

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

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_ranking"
>title="Bloc Classement"
>abstract="Le bloc Classement vous permet de classer les profils en fonction d’un attribut spécifique et de les inclure dans votre composition."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_rank_profilelimit_text"
>title="Ajouter une limite de profil"
>abstract="Le bouton (bascule) Ajouter une limite de profil permet de spécifier un nombre maximal de profils à inclure dans le cadre du processus de classement."

Le type de bloc **[!UICONTROL Classement]** permet de classer et de trier les profils en fonction d’un attribut spécifié et d’inclure ces profils classés dans votre composition.

Pour ajouter un bloc **[!UICONTROL Classement]**, sélectionnez l’icône **+**, puis **[!UICONTROL Classement]**.

![L’option « Classement » est sélectionnée.](../images/ui/audience-composition/add-rank-block.png)

Lorsque vous sélectionnez le bloc, les détails du classement s’affichent dans le rail de droite, notamment le libellé du bloc, l’attribut de classement, l’ordre de classement et un bouton permettant de limiter le nombre de profils à classer.

![Le bloc de classement est mis en surbrillance, ainsi que les détails le concernant.](../images/ui/audience-composition/rank.png)

Pour sélectionner l’attribut par lequel classer les audiences, sélectionnez l’icône de ![filtre](/help/images/icons/project-edit.png).

![L’icône de filtre est mise en surbrillance et indique les éléments à sélectionner pour accéder à l’écran de sélection des attributs de profil.](../images/ui/audience-composition/select-rank-attribute.png)

Une liste d’attributs de profil s’affiche. Dans cette fenêtre contextuelle, vous pouvez sélectionner le type d’attribut selon lequel vous souhaitez classer votre audience. Cliquez sur **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc de classement. Notez que l’attribut sélectionné peut **uniquement** être composé de chiffres.

![Une liste d’attributs s’affiche.](../images/ui/audience-composition/rank-attribute.png)

Après avoir sélectionné l’attribut, vous pouvez sélectionner l’ordre de classement. Il s’agit d’un ordre croissant (du plus bas au plus élevé) ou décroissant (du plus élevé au plus bas).

En outre, vous pouvez limiter le nombre de profils renvoyés en activant le bouton **[!UICONTROL Ajouter une limite de profil]**. Lorsque ce bouton est activé, vous pouvez définir le nombre maximal de profils renvoyés dans le champ **[!UICONTROL Profils inclus]**.

![Le bouton (bascule) Ajouter une limite de profil est mis en surbrillance, ce qui vous permet de limiter le nombre de profils renvoyés.](../images/ui/audience-composition/add-profile-limit-rank.png)

## [!UICONTROL Fractionner] {#split-block}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split"
>title="Bloc Partager"
>abstract="Le bloc Partager permet de diviser votre composition en plusieurs chemins d’accès."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_type"
>title="Type Partage"
>abstract="Vous pouvez partager votre composition en pourcentage ou en attributs. Le partage en pourcentage partage les profils de manière aléatoire en plusieurs chemins d’accès. Le partage en attributs vous permet de partager les profils en fonction d’un attribut spécifique."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_otherprofiles_text"
>title="Autres profils"
>abstract="Le bouton (bascule) Autres profils vous permet de créer un chemin d’accès supplémentaire avec les profils restants qui ne correspondent à aucune des conditions spécifiées des autres chemins d’accès."

>[!NOTE]
>
>Pour utiliser le bloc **[!UICONTROL Fractionner]**, vous **devez** avoir au moins 10 profils dans votre audience.

Le type de bloc **[!UICONTROL Fractionner]** vous permet de fractionner votre nouvelle audience en différentes sous-audiences. Vous pouvez fractionner cette audience en fonction d’un pourcentage ou d’un attribut.

Pour ajouter un bloc **[!UICONTROL Fractionner]**, sélectionnez l’icône **+**, puis **[!UICONTROL Fractionner]**.

![L’option « Fractionner » est sélectionnée.](../images/ui/audience-composition/add-split-block.png)

Vous pouvez fractionner une audience de deux façons : par pourcentage ou par attribut.

### Fractionner par pourcentage {#split-percentage}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_percentage"
>title="Fractionner par pourcentage"
>abstract="Vous pouvez partager l’audience de manière aléatoire en plusieurs audiences, en fonction du nombre de chemins et des pourcentages fournis."

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_split_persistent"
>title="Division persistante"
>abstract="Vous pouvez rendre le partage en pourcentage persistant en activant cette option et en sélectionnant un espace de noms d’identité."

Lors du fractionnement par pourcentage, les audiences sont réparties de manière aléatoire en fonction du nombre de chemins et des pourcentages fournis.

![Le partage en pourcentage est mis en surbrillance.](../images/ui/audience-composition/split-by-percentage.png)

Vous pouvez également fournir une identité, ce qui rendrait le partage en fonction du pourcentage persistant. Les types d’identité disponibles incluent tous les espaces de noms d’identité disponibles dans votre organisation.

![La case à cocher Fractionner par identité est mise en surbrillance. En outre, la liste déroulante qui vous permet de sélectionner avec une identité à fractionner est mise en surbrillance.](../images/ui/audience-composition/split-by-identity.png)

### Fractionner par attribut {#split-attribute}

Lors du fractionnement par attribut, les audiences sont fractionnées en fonction des attributs fournis. Pour sélectionner l’attribut du fractionnement, sélectionnez le bloc **[!UICONTROL Fractionner]**, puis l’icône de ![filtrage](/help/images/icons/project-edit.png).

![Le bouton de filtrage est sélectionné et indique comment filtrer par attribut.](../images/ui/audience-composition/split-by-attribute.png)

Une liste d’attributs de profil s’affiche. Sélectionnez le type d’attribut, puis **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc de fractionnement.

![Une liste d’attributs s’affiche.](../images/ui/audience-composition/select-attribute.png)

Après avoir sélectionné l’attribut, vous pouvez choisir les profils qui appartiendront à une sous-audience en ajoutant les valeurs dans le champ **[!UICONTROL Valeurs]**.

![Les valeurs par lesquelles vous souhaitez fractionner les attributs sont ajoutées.](../images/ui/audience-composition/attribute-split-values.png)

En outre, vous pouvez activer le bouton **[!UICONTROL Autres profils]** pour créer une sous-audience composée de tous les profils non sélectionnés.

![Le bouton « Autres profils » est mis en surbrillance.](../images/ui/audience-composition/split-other-profiles.png)

## Publier votre audience {#publish}

>[!CONTEXTUALHELP]
>id="platform_segmentation_ao_publish"
>title="Publier"
>abstract="Vous pouvez publier votre composition pour créer les audiences obtenues dans Adobe Experience Platform."

>[!IMPORTANT]
>
>Lors de la publication de la composition de votre audience, notez qu’il peut s’écouler jusqu’à 48 heures avant qu’elle soit évaluée et activée pour une utilisation dans des services en aval tels qu’une destination Real-Time CDP ou un canal Adobe Journey Optimizer.

Après avoir créé votre composition, vous pouvez l’enregistrer et la publier en sélectionnant **[!UICONTROL Publier]**.

![Le bouton Publier est mis en surbrillance et vous montre comment enregistrer et publier votre composition.](../images/ui/audience-composition/publish.png)

En cas d’erreur lors de la création de l’audience, une alerte s’affiche, vous indiquant comment résoudre le problème.

![Le bouton Publier est mis en surbrillance et vous montre comment enregistrer et publier votre composition.](../images/ui/audience-composition/audience-alert.png)

## Étapes suivantes

La composition de l’audience fournit un workflow complet qui vous permet de créer des compositions à partir des différents types de bloc. Pour en savoir plus sur d’autres parties de l’interface utilisateur de Segmentation Service, veuillez lire le [Guide d’utilisation de Segmentation Service](./overview.md).

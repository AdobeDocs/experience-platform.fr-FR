---
keywords: Experience Platform;accueil;rubriques les plus consultées;Segmentation Service;segmentation;service de segmentation;guide de l’utilisateur;guide de l’interface utilisateur;guide de l’interface utilisateur d’audiences;générateur d’audience;audience;audiences;guide de l’interface utilisateur d’audiences;
solution: Experience Platform
title: Guide de l’interface utilisateur d’Audiences
description: Le Créateur d’audience dans l’interface utilisateur d’Adobe Experience Platform fournit un espace de travail riche qui vous permet d’interagir avec les éléments de données de profil. L’espace de travail propose des commandes intuitives pour créer et modifier des audiences pour votre organisation.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: ht
source-wordcount: '1321'
ht-degree: 100%

---

# Guide de l’interface utilisateur du Créateur d’audience

>[!IMPORTANT]
>
>Le Créateur d’audience est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs et utilisatrices. La documentation et les fonctionnalités peuvent changer.

Le Créateur d’audience offre un espace de travail permettant de créer et de modifier des audiences à l’aide de blocs utilisés pour représenter différentes actions.

![Interface utilisateur du Créateur d’audience.](../images/ui/audience-builder/audience-builder.png)

Le canevas de composition d’audience se compose de cinq types de blocs différents : **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclure]](#exclude-block)**, **[[!UICONTROL Joindre]](#join-block)**, **[[!UICONTROL Classement]](#rank-block)** et **[[!UICONTROL Fractionner]](#split-block)**.

## [!UICONTROL Audience] {#audience-block}

Le type de bloc **[!UICONTROL Audience]** permet d’ajouter les sous-audiences de votre choix pour composer votre nouvelle audience plus grande. Par défaut, un bloc **[!UICONTROL Audience]** est inclus dans la partie supérieure du canevas de composition.

Lorsque vous sélectionnez le bloc **[!UICONTROL Audience]**, le rail de droite affiche des commandes pour libeller et ajouter des audiences au bloc.

![Les détails du bloc Audience s’affichent.](../images/ui/audience-builder/select-audience.png)

Après avoir sélectionné **[!UICONTROL Ajouter une audience]**, une liste d’audiences s’affiche. Sélectionnez les audiences que vous souhaitez inclure, puis **[!UICONTROL Ajouter]** pour les ajouter à votre bloc d’audience.

![Une liste d’audiences s’affiche. Dans cette boîte de dialogue, vous pouvez sélectionner l’audience à ajouter.](../images/ui/audience-builder/select-audience.png)

Les audiences sélectionnées s’affichent maintenant dans le rail de droite lorsque le bloc **[!UICONTROL Audience]** est sélectionné. À partir de là, vous pouvez modifier le type de fusion des audiences combinées.

![Les types de fusion possibles pour les audiences sont mis en surbrillance.](../images/ui/audience-builder/merge-types.png)

| Type de fusion | Description |
| ---------- | ----------- |
| [!UICONTROL Union] | Les audiences sont combinées en une seule audience. Il s’agit de l’équivalent d’une opération OR. |
| [!UICONTROL Intersection] | Les audiences sont combinées, avec seulement les audiences partagées dans **toutes** celles ajoutées. Il s’agit de l’équivalent d’une opération AND. |
| [!UICONTROL Exclure le chevauchement] | Les audiences sont combinées, avec seulement les audiences partagées dans **une, mais pas toutes** celles ajoutées. Il s’agit de l’équivalent d’une opération XOR. |

## [!UICONTROL Exclure] {#exclude-block}

Le type de bloc **[!UICONTROL Exclure]** permet d’exclure des sous-audiences ou attributs spécifiés de votre nouvelle audience plus grande.

Pour ajouter un bloc **[!UICONTROL Exclure]**, sélectionnez l’icône **+**, puis **[!UICONTROL Exclure]**.

![L’option Exclure est sélectionnée.](../images/ui/audience-builder/add-exclude-block.png)

Le bloc **[!UICONTROL Exclure]** est ajouté. Lorsque ce bloc est sélectionné, les détails de l’exclusion apparaissent dans le rail de droite. Le libellé du bloc et le type d’exclusion sont inclus. Vous pouvez exclure [par audience](#exclude-audience) ou [par attribut](#exclude-attribute).

![Le bloc Exclure, mettant en surbrillance les deux types d’exclusion disponibles.](../images/ui/audience-builder/exclude.png)

### Exclure par audience {#exclude-audience}

Si vous excluez par audience, vous pouvez sélectionner les audiences à exclure en sélectionnant **[!UICONTROL Ajouter une audience]**.

![Le bouton Ajouter une audience est sélectionné, ce qui vous permet de choisir l’audience que vous souhaitez exclure.](../images/ui/audience-builder/add-excluded-audience.png)

Une liste d’audiences s’affiche. Sélectionnez **[!UICONTROL Ajouter]** pour ajouter les audiences que vous souhaitez exclure à votre bloc d’exclusion.

![Une liste d’audiences s’affiche. Dans cette boîte de dialogue, vous pouvez sélectionner l’audience à ajouter.](../images/ui/audience-builder/select-audience.png)

### Exclure par attribut {#exclude-attribute}

Si vous excluez par attribut, vous pouvez sélectionner les attributs à exclure en sélectionnant l’icône de ![filtre](../images/ui/audience-builder/filter-attribute.png) dans la section **[!UICONTROL Règle d’exclusion]**.

![La section d’attribut est mise en surbrillance, vous indiquant où sélectionner l’attribut à exclure.](../images/ui/audience-builder/exclude-attribute.png)

Une liste d’attributs de profil s’affiche. Sélectionnez le type d’attribut à exclure, puis **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc d’exclusion.

![Une liste d’attributs s’affiche.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Jointure] {#join-block}

Le type de bloc **[!UICONTROL Joindre]** permet d’ajouter des audiences externes à partir de jeux de données qui n’ont pas encore été traités par Adobe Experience Platform.

Pour ajouter un bloc **[!UICONTROL Joindre]**, sélectionnez l’icône **+**, puis **[!UICONTROL Joindre]**.

![L’option « Joindre » est sélectionnée.](../images/ui/audience-builder/add-join-block.png)

Lorsque vous sélectionnez le bloc, les détails de la jonction sont affichés dans le rail de droite, y compris le libellé du bloc et l’option d’ajout d’audiences au jeu de données d’enrichissement.

![Le bloc de jonction est mis en surbrillance, ainsi que des détails le concernant.](../images/ui/audience-builder/join.png)

Après avoir sélectionné **[!UICONTROL Ajouter une audience]**, une liste d’audiences s’affiche. Sélectionnez les audiences que vous souhaitez inclure, puis choisissez **[!UICONTROL Ajouter]** pour les ajouter à votre bloc de jonction.

![Une liste d’audiences s’affiche. Vous pouvez sélectionner l’audience à ajouter à partir de cette boîte de dialogue.](../images/ui/audience-builder/select-audience.png)

Vos audiences sélectionnées s’affichent maintenant dans le rail de droite lorsque le bloc **[!UICONTROL Joindre]** est sélectionné.

![Les audiences qui ont été ajoutées dans le cadre de la jonction s’affichent.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Classement] {#rank-block}

Le type de bloc **[!UICONTROL Classement]** vous permet de classer et de trier les audiences avant la publication de votre nouvelle audience.

Pour ajouter un bloc **[!UICONTROL Classement]**, sélectionnez l’icône **+**, puis **[!UICONTROL Classement]**.

![L’option « Classement » est sélectionnée.](../images/ui/audience-builder/add-rank-block.png)

Lorsque vous sélectionnez le bloc, les détails du classement s’affichent dans le rail de droite, notamment le libellé du bloc, l’attribut de classement, l’ordre de classement et un bouton permettant de limiter le nombre de profils à classer.

![Le bloc de classement est mis en surbrillance, ainsi que les détails le concernant.](../images/ui/audience-builder/rank.png)

Pour sélectionner l’attribut par lequel classer les audiences, sélectionnez l’icône de ![filtre](../images/ui/audience-builder/filter-attribute.png).

![L’icône de filtre est mise en surbrillance et indique les éléments à sélectionner pour accéder à l’écran de sélection des attributs de profil.](../images/ui/audience-builder/select-rank-attribute.png)

Une liste d’attributs de profil s’affiche. Dans cette fenêtre contextuelle, vous pouvez sélectionner le type d’attribut selon lequel vous souhaitez classer votre audience. Cliquez sur **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc de classement. Notez que l’attribut sélectionné peut **seulement** être de type `int`.

![Une liste d’attributs s’affiche.](../images/ui/audience-builder/select-attribute.png)

Après avoir sélectionné l’attribut, vous pouvez sélectionner l’ordre de classement. Il s’agit d’un ordre croissant (du plus bas au plus élevé) ou décroissant (du plus élevé au plus bas).

En outre, vous pouvez limiter le nombre d’audiences renvoyées en activant le bouton **[!UICONTROL Ajouter une limite de profil]**. Lorsque ce bouton est activé, vous pouvez définir le nombre maximal d’audiences renvoyées dans le champ **[!UICONTROL Profils inclus]**.

![Le bouton« Ajouter une limite de profil » est mis en surbrillance, ce qui vous permet de limiter le nombre d’audiences renvoyées.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Fractionner] {#split-block}

Le type de bloc **[!UICONTROL Fractionner]** vous permet de fractionner votre nouvelle audience en différentes sous-audiences. Vous pouvez fractionner cette audience en fonction d’un pourcentage ou d’un attribut.

Pour ajouter un bloc **[!UICONTROL Fractionner]**, sélectionnez l’icône **+**, puis **[!UICONTROL Fractionner]**.

![L’option « Fractionner » est sélectionnée.](../images/ui/audience-builder/add-split-block.png)

### Fractionner par pourcentage {#split-percentage}

Lors du fractionnement par pourcentage, les audiences sont réparties de manière aléatoire en fonction du nombre de chemins et des pourcentages fournis.

Par exemple, vous pouvez avoir trois chemins, chacun avec un pourcentage de profils différent.

![La répartition en nombre d’audiences et de pourcentages enregistrés s’affiche.](../images/ui/audience-builder/percentages.png)

De plus, vous pouvez désigner l’une des audiences fractionnées comme groupe témoin.

![Le bouton « groupe témoin » est activé. Vous pouvez ainsi désigner l’une des audiences fractionnées comme groupe témoin.](../images/ui/audience-builder/control-group.png)

### Fractionner par attribut {#split-attribute}

Lors du fractionnement par attribut, les audiences sont fractionnées en fonction des attributs fournis. Pour sélectionner l’attribut du fractionnement, sélectionnez le bloc **[!UICONTROL Fractionner]**, puis l’icône de ![filtrage](../images/ui/audience-builder/filter-attribute.png).

![Le bouton de filtrage est sélectionné et indique comment filtrer par attribut.](../images/ui/audience-builder/select-attribute-split.png)

Une liste d’attributs de profil s’affiche. Sélectionnez le type d’attribut, puis **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc de fractionnement.

![Une liste d’attributs s’affiche.](../images/ui/audience-builder/select-attribute.png)

Après avoir sélectionné l’attribut, vous pouvez choisir les profils qui appartiendront à une sous-audience en ajoutant les valeurs dans le champ **[!UICONTROL Valeurs]**.

![Les valeurs par lesquelles vous souhaitez fractionner les attributs sont ajoutées.](../images/ui/audience-builder/attribute-split-values.png)

En outre, vous pouvez activer le bouton **[!UICONTROL Autres profils]** pour créer une sous-audience composée de tous les profils non sélectionnés.

![Le bouton « Autres profils » est mis en surbrillance.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Publier votre audience

Après avoir composé votre audience, vous pouvez l’enregistrer et la publier en sélectionnant **[!UICONTROL Publier]**.

![Le bouton « Publier » est mis en surbrillance et vous montre comment enregistrer et publier votre audience.](../images/ui/audience-builder/publish-audience.png)

En cas d’erreur lors de la création de l’audience, une alerte s’affiche, vous indiquant comment résoudre le problème.

![Le bouton « Publier » est mis en surbrillance et vous montre comment enregistrer et publier votre audience.](../images/ui/audience-builder/audience-alert.png)

## Étapes suivantes

Le créateur d’audiences offre un workflow riche qui vous permet de créer des audiences à partir des différents types de bloc. Pour en savoir plus sur d’autres parties de l’interface utilisateur de Segmentation Service, veuillez lire le [Guide d’utilisation de Segmentation Service](./overview.md).

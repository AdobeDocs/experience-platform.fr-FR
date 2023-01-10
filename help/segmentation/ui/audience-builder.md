---
keywords: Experience Platform;accueil;rubriques les plus consultées;Segmentation Service;segmentation;service de segmentation;guide de l’utilisateur;guide de l’interface utilisateur d’audience;générateur d’audience;audience;guide de l’interface utilisateur d’audience
solution: Experience Platform
title: Guide de l’interface utilisateur d’Audiences
description: Audience Builder de l’interface utilisateur de Adobe Experience Platform fournit un espace de travail riche qui vous permet d’interagir avec les éléments de données Profile. L’espace de travail fournit des contrôles intuitifs pour la création et la modification d’audiences pour votre organisation.
hide: true
hidefromtoc: true
exl-id: 0dda0cb1-49e0-478b-8004-84572b6cf625
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 1%

---

# Guide de l’interface utilisateur d’Audience Builder

>[!IMPORTANT]
>
>Audience Builder est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. La documentation et les fonctionnalités peuvent changer.

Audience Builder fournit un espace de travail permettant de créer et de modifier des audiences à l’aide de blocs utilisés pour représenter différentes actions.

![Interface utilisateur d’Audience Builder.](../images/ui/audience-builder/audience-builder.png)

Le canevas de composition de l’audience se compose de cinq types de blocs différents : **[[!UICONTROL Audience]](#audience-block)**, **[[!UICONTROL Exclure]](#exclude-block)**, **[[!UICONTROL Joindre]](#join-block)**, **[[!UICONTROL Classement]](#rank-block)**, et **[[!UICONTROL Partage]](#split-block)**.

## [!UICONTROL Audience   ] {#audience-block}

Le **[!UICONTROL Audience]** type block permet d’ajouter les sous-audiences que vous souhaitez composer avec votre nouvelle audience plus large. Par défaut, un **[!UICONTROL Audience]** est inclus en haut du canevas de composition.

Lorsque vous sélectionnez la variable **[!UICONTROL Audience]** block, le rail de droite affiche les commandes d’étiquetage et d’ajout d’audiences au bloc.

![Les détails du bloc Audience s’affichent.](../images/ui/audience-builder/select-audience.png)

Après avoir sélectionné **[!UICONTROL Ajouter une audience]**, une liste d’audiences s’affiche. Sélectionnez les audiences que vous souhaitez inclure, suivies de **[!UICONTROL Ajouter]** pour les ajouter à votre bloc d’audience.

![Une liste d’audiences s’affiche. Vous pouvez sélectionner l’audience à ajouter dans cette boîte de dialogue.](../images/ui/audience-builder/select-audience.png)

Les audiences sélectionnées s’affichent maintenant dans le rail de droite lorsque la variable **[!UICONTROL Audience]** block est sélectionné. À partir de là, vous pouvez modifier le type de fusion des audiences combinées.

![Les types de fusion possibles pour les audiences sont mis en surbrillance.](../images/ui/audience-builder/merge-types.png)

| Type de fusion | Description |
| ---------- | ----------- |
| [!UICONTROL Union] | Les audiences sont combinées en une seule audience. Il s’agit de l’équivalent d’une opération OU. |
| [!UICONTROL Intersection] | Les audiences sont combinées, avec uniquement les audiences partagées dans **all** d&#39;entre eux en cours d&#39;ajout. Il s’agirait de l’équivalent d’une opération ET. |
| [!UICONTROL Exclure le chevauchement] | Les audiences sont combinées, avec uniquement les audiences partagées dans **un, mais pas tous** d&#39;entre eux en cours d&#39;ajout. Cela serait l’équivalent d’une opération XOR. |

## [!UICONTROL Exclure] {#exclude-block}

Le **[!UICONTROL Exclure]** le type block permet d’exclure des sous-audiences ou attributs spécifiés de votre nouvelle audience plus large.

Pour ajouter une **[!UICONTROL Exclure]** block, sélectionnez la **+** , suivie de **[!UICONTROL Exclure]**.

![L’option Exclure est sélectionnée.](../images/ui/audience-builder/add-exclude-block.png)

Le **[!UICONTROL Exclure]** block est ajouté. Lorsque ce bloc est sélectionné, les détails de l’exclusion apparaissent dans le rail de droite. Cela inclut le libellé du bloc et le type d&#39;exclusion. Vous pouvez exclure [par audience](#exclude-audience) ou [par attribut](#exclude-attribute).

![Le bloc Exclure , mettant en surbrillance les deux types d’exclusion disponibles.](../images/ui/audience-builder/exclude.png)

### Exclure par audience {#exclude-audience}

Si vous excluez par audience, vous pouvez sélectionner les audiences à exclure en sélectionnant **[!UICONTROL Ajouter une audience]**.

![Le bouton Ajouter une audience est sélectionné, ce qui vous permet de choisir l&#39;audience que vous souhaitez exclure.](../images/ui/audience-builder/add-excluded-audience.png)

Une liste d’audiences s’affiche. Sélectionner **[!UICONTROL Ajouter]** pour ajouter les audiences que vous souhaitez exclure à votre bloc d’exclusion.

![Une liste d’audiences s’affiche. Vous pouvez sélectionner l’audience à ajouter dans cette boîte de dialogue.](../images/ui/audience-builder/select-audience.png)

### Exclure par attribut {#exclude-attribute}

Si vous excluez par attribut, vous pouvez sélectionner les attributs à exclure en sélectionnant le ![filter](../images/ui/audience-builder/filter-attribute.png) dans le **[!UICONTROL Règle d’exclusion]** .

![La section Attribut est mise en surbrillance, vous indiquant où sélectionner l’attribut à exclure.](../images/ui/audience-builder/exclude-attribute.png)

Une liste des attributs de profil s’affiche. Sélectionnez le type d’attribut à exclure, suivi de **[!UICONTROL Sélectionner]** pour les ajouter à votre bloc d’exclusion.

![Une liste d’attributs s’affiche.](../images/ui/audience-builder/select-attribute.png)

## [!UICONTROL Jointure] {#join-block}

Le **[!UICONTROL Joindre]** type block permet d’ajouter des audiences externes à partir de jeux de données qui n’ont pas encore été traités par Adobe Experience Platform.

Pour ajouter une **[!UICONTROL Joindre]** block, sélectionnez la **+** , suivie de **[!UICONTROL Joindre]**.

![L’option Joindre est sélectionnée.](../images/ui/audience-builder/add-join-block.png)

Lorsque vous sélectionnez le bloc, les détails de la jointure sont affichés dans le rail de droite, y compris le libellé du bloc et l’option d’ajout d’audiences au jeu de données d’enrichissement.

![Le bloc de jointure est mis en surbrillance, y compris des détails sur le bloc de jointure.](../images/ui/audience-builder/join.png)

Après avoir sélectionné **[!UICONTROL Ajouter une audience]**, une liste d’audiences s’affiche. Sélectionnez les audiences que vous souhaitez inclure, suivies de **[!UICONTROL Ajouter]** pour les ajouter à votre bloc join.

![Une liste d’audiences s’affiche. Vous pouvez sélectionner l’audience à ajouter dans cette boîte de dialogue.](../images/ui/audience-builder/select-audience.png)

Les audiences sélectionnées s’affichent maintenant dans le rail de droite lorsque la variable **[!UICONTROL Joindre]** block est sélectionné.

![Les audiences qui ont été ajoutées dans le cadre de la jointure s’affichent.](../images/ui/audience-builder/selected-audiences.png)

## [!UICONTROL Classement] {#rank-block}

Le **[!UICONTROL Classement]** le type block vous permet de classer et de trier les audiences avant la publication de votre nouvelle audience.

Pour ajouter une **[!UICONTROL Classement]** block, sélectionnez la **+** , suivie de **[!UICONTROL Classement]**.

![L’option Classement est sélectionnée.](../images/ui/audience-builder/add-rank-block.png)

Lorsque vous sélectionnez le bloc, les détails du classement s’affichent dans le rail de droite, notamment le libellé du bloc, l’attribut de classement, l’ordre de classement et un bouton d’activation/désactivation permettant de limiter le nombre de profils à classer.

![Le bloc de classement est mis en surbrillance, ainsi que les détails du bloc de classement.](../images/ui/audience-builder/rank.png)

Pour sélectionner l’attribut par lequel classer les audiences, sélectionnez la variable ![filter](../images/ui/audience-builder/filter-attribute.png) icône .

![L’icône de filtre est mise en surbrillance et indique les éléments à sélectionner pour accéder à l’écran de sélection des attributs de profil.](../images/ui/audience-builder/select-rank-attribute.png)

Une liste des attributs de profil s’affiche. Dans cette fenêtre contextuelle, vous pouvez sélectionner le type d’attribut selon lequel vous souhaitez classer votre audience. Sélectionner **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc de classement. Notez que l’attribut sélectionné peut **only** être de type `int`.

![Une liste d’attributs s’affiche.](../images/ui/audience-builder/select-attribute.png)

Après avoir sélectionné l’attribut, vous pouvez sélectionner l’ordre de classement. Il s’agit d’un ordre croissant (du plus petit au plus élevé) ou décroissant (du plus haut au plus bas).

En outre, vous pouvez limiter le nombre d’audiences renvoyées en activant la variable **[!UICONTROL Ajouter une limite de profil]** bascule. Lorsque cette bascule est activée, vous pouvez définir le nombre maximal d’audiences renvoyées dans la variable **[!UICONTROL Profils inclus]** champ .

![Le bouton d’activation/désactivation Ajouter une limite de profil est mis en surbrillance, ce qui vous permet de limiter le nombre d’audiences renvoyées.](../images/ui/audience-builder/add-profile-limit.png)

## [!UICONTROL Fractionner] {#split-block}

Le **[!UICONTROL Partage]** type block permet de diviser votre nouvelle audience en différentes sous-audiences. Vous pouvez fractionner cette audience en fonction d’un pourcentage ou d’un attribut.

Pour ajouter une **[!UICONTROL Partage]** block, sélectionnez la **+** , suivie de **[!UICONTROL Partage]**.

![L’option Partage est sélectionnée.](../images/ui/audience-builder/add-split-block.png)

### Partage par pourcentage {#split-percentage}

Lors de la division par pourcentage, les audiences sont réparties de manière aléatoire en fonction du nombre de chemins et de pourcentages fournis.

Par exemple, vous pouvez avoir trois chemins, chacun avec un pourcentage différent de profils.

![La répartition en nombre d’audiences et de pourcentages enregistrées s’affiche.](../images/ui/audience-builder/percentages.png)

De plus, vous pouvez marquer l’une des audiences partagées comme groupe témoin.

![Le bouton bascule de la population témoin est activé. Vous pouvez ainsi marquer l’une des audiences partagées comme groupe témoin.](../images/ui/audience-builder/control-group.png)

### Partage par attribut {#split-attribute}

Lors de la division par attribut, les audiences sont fractionnées en fonction des attributs fournis. Pour sélectionner l’attribut de division, sélectionnez la variable **[!UICONTROL Partage]** , suivie de la fonction ![filter](../images/ui/audience-builder/filter-attribute.png) icône .

![Le bouton de filtrage est sélectionné et indique comment filtrer par attribut.](../images/ui/audience-builder/select-attribute-split.png)

Une liste des attributs de profil s’affiche. Sélectionnez le type d’attribut, suivi de **[!UICONTROL Sélectionner]** pour l’ajouter à votre bloc partagé.

![Une liste d’attributs s’affiche.](../images/ui/audience-builder/select-attribute.png)

Après avoir sélectionné l’attribut, vous pouvez choisir les profils qui appartiendront à une sous-audience en ajoutant les valeurs dans la variable **[!UICONTROL Valeurs]** champ .

![Les valeurs par lesquelles vous souhaitez fractionner les attributs sont ajoutées.](../images/ui/audience-builder/attribute-split-values.png)

En outre, vous pouvez activer la variable **[!UICONTROL Autres profils]** pour créer une sous-audience composée de tous les profils non sélectionnés.

![Le bouton bascule Autres profils est mis en surbrillance.](../images/ui/audience-builder/attribute-split-other-profiles.png)

## Publier votre audience

Après avoir composé votre audience, vous pouvez l’enregistrer et la publier en sélectionnant **[!UICONTROL Publier]**.

![Le bouton Publier est mis en surbrillance et vous montre comment enregistrer et publier votre audience.](../images/ui/audience-builder/publish-audience.png)

En cas d’erreur lors de la création de l’audience, une alerte s’affiche, vous indiquant comment résoudre le problème.

![Le bouton Publier est mis en surbrillance et vous montre comment enregistrer et publier votre audience.](../images/ui/audience-builder/audience-alert.png)

## Étapes suivantes

Le créateur d’audiences offre un processus riche qui vous permet de créer des audiences à partir des différents types de blocs. Pour en savoir plus sur d’autres parties de l’interface utilisateur de Segmentation Service, veuillez lire le [Guide d’utilisation de Segmentation Service](./overview.md).

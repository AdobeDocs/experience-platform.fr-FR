---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;schéma;schémas;schémas
solution: Experience Platform
title: Création et modification de schémas dans l’interface utilisateur
description: Découvrez les principes de base de la création et de l’édition de schémas dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 49a54b78d1e3745694352e779fb2226acd99d663
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 0%

---

# Création et modification de schémas dans l’interface utilisateur

Ce guide explique comment créer, modifier et gérer des schémas de modèle de données d’expérience (XDM) pour votre organisation dans l’interface utilisateur de Adobe Experience Platform.

>[!IMPORTANT]
>
>Les schémas XDM sont extrêmement personnalisables. Par conséquent, les étapes de création d’un schéma peuvent varier en fonction du type de données que vous souhaitez que le schéma capture. Par conséquent, ce document couvre uniquement les interactions de base que vous pouvez effectuer avec les schémas dans l’interface utilisateur et exclut les étapes associées telles que la personnalisation des classes, des groupes de champs de schéma, des types de données et des champs.
>
>Pour une visite complète du processus de création de schéma, suivez le [tutoriel sur la création de schéma](../../tutorials/create-schema-ui.md) pour créer un schéma d’exemple complet et vous familiariser avec les nombreuses fonctionnalités de la variable [!DNL Schema Editor].

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la section [Présentation de XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform, et de [principes de base de la composition des schémas](../../schema/composition.md) pour un aperçu de la création des schémas.

## Création d&#39;un schéma {#create}

Dans le [!UICONTROL Schémas] espace de travail, sélectionnez **[!UICONTROL Créer un schéma]** dans le coin supérieur droit. Dans la liste déroulante qui s’affiche, vous pouvez choisir entre **[!UICONTROL XDM Individual Profile]** et **[!UICONTROL XDM ExperienceEvent]** comme classe de base du schéma. Vous pouvez également sélectionner **[!UICONTROL Parcourir]** pour effectuer une sélection dans la liste complète des classes disponibles, ou [créer une classe personnalisée](./classes.md#create) au lieu de .

![](../../images/ui/resources/schemas/create-schema.png)

Une fois que vous avez sélectionné une classe, la variable [!DNL Schema Editor] apparaît et la structure de base du schéma (fournie par la classe) s’affiche dans la zone de travail. À partir de là, vous pouvez utiliser le rail de droite pour ajouter une **[!UICONTROL Nom d’affichage]** et **[!UICONTROL Description]** pour le schéma.

![](../../images/ui/resources/schemas/schema-details.png)

Vous pouvez maintenant commencer à créer la structure du schéma en [ajout de groupes de champs de schéma](#add-field-groups).

## Modification d’un schéma existant {#edit}

>[!NOTE]
>
>Une fois qu’un schéma a été enregistré et utilisé dans l’ingestion de données, seules des modifications additifs peuvent lui être apportées. Voir [règles d’évolution des schémas](../../schema/composition.md#evolution) pour plus d’informations.

Pour modifier un schéma existant, sélectionnez l’option **[!UICONTROL Parcourir]** puis sélectionnez le nom du schéma à modifier.

![](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Vous pouvez utiliser les fonctionnalités de recherche et de filtrage de l’espace de travail pour faciliter la recherche du schéma. Consultez le guide sur la [exploration des ressources XDM](../explore.md) pour plus d’informations.

Une fois que vous avez sélectionné un schéma, la variable [!DNL Schema Editor] apparaît avec la structure du schéma affichée dans la zone de travail. Vous pouvez désormais [ajouter des groupes de champs](#add-field-groups) au schéma, [modifier les noms d’affichage des champs ;](#display-names)ou [modifier des groupes de champs personnalisés ;](./field-groups.md#edit) si le schéma en utilise un.

## Ajout de groupes de champs à un schéma {#add-field-groups}

>[!NOTE]
>
>Cette section explique comment ajouter des groupes de champs existants à un schéma. Si vous souhaitez créer un groupe de champs personnalisé, consultez le guide sur [création et modification de groupes de champs](./field-groups.md#create) au lieu de .

Une fois que vous avez ouvert un schéma dans la fonction [!DNL Schema Editor], vous pouvez ajouter des champs au schéma à l’aide de groupes de champs. Pour commencer, sélectionnez **[!UICONTROL Ajouter]** en regard de **[!UICONTROL Groupes de champs]** dans le rail de gauche.

![](../../images/ui/resources/schemas/add-field-group-button.png)

Une boîte de dialogue s’affiche, affichant la liste des groupes de champs que vous pouvez sélectionner pour le schéma. Puisque les groupes de champs ne sont compatibles qu’avec une seule classe, seuls les groupes de champs associés à la classe sélectionnée du schéma sont répertoriés. Par défaut, les groupes de champs répertoriés sont triés en fonction de leur popularité d’utilisation au sein de votre entreprise.

![](../../images/ui/resources/schemas/field-group-popularity.png)

Si vous connaissez l’activité générale ou le domaine d’activité des champs que vous souhaitez ajouter, sélectionnez une ou plusieurs des catégories verticales du secteur dans le rail de gauche pour filtrer la liste affichée des groupes de champs.

![](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Pour plus d’informations sur les bonnes pratiques relatives à la modélisation de données spécifique au secteur dans XDM, consultez la documentation sur [modèles de données du secteur](../../schema/industries/overview.md).

Vous pouvez également utiliser la barre de recherche pour localiser le groupe de champs souhaité. Les groupes de champs dont le nom correspond à la requête apparaissent en haut de la liste. Sous **[!UICONTROL Champs standard]**, les groupes de champs contenant les champs qui décrivent les attributs de données souhaités s’affichent.

![](../../images/ui/resources/schemas/field-group-search.png)

Cochez la case en regard du nom du groupe de champs que vous souhaitez ajouter au schéma. Vous pouvez sélectionner plusieurs groupes de champs dans la liste, chaque groupe de champs sélectionné apparaissant dans le rail de droite.

![](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Pour tout groupe de champs répertorié, vous pouvez pointer ou vous concentrer sur l’icône d’informations (![](../../images/ui/resources/schemas/info-icon.png)) pour afficher une brève description du type de données que le groupe de champs capture. Vous pouvez également sélectionner l’icône d’aperçu (![](../../images/ui/resources/schemas/preview-icon.png)) pour afficher la structure des champs que le groupe de champs fournit avant de décider de l’ajouter au schéma.

Une fois que vous avez choisi vos groupes de champs, sélectionnez **[!UICONTROL Ajouter des groupes de champs]** pour les ajouter au schéma.

![](../../images/ui/resources/schemas/add-field-group-finish.png)

Le [!DNL Schema Editor] réapparaît avec les champs fournis par le groupe de champs représentés dans la zone de travail.

![](../../images/ui/resources/schemas/field-groups-added.png)

## Activation d’un schéma pour Real-time Customer Profile {#profile}

[Real-time Customer Profile](../../../profile/home.md) fusionne les données provenant de sources disparates afin de créer une vue complète de chaque client. Si vous souhaitez que les données capturées par un schéma participent à ce processus, vous devez activer le schéma à utiliser dans [!DNL Profile].

>[!IMPORTANT]
>
>Pour activer un schéma pour [!DNL Profile], un champ d’identité Principal doit être défini pour celui-ci. Consultez le guide sur la [définition des champs d’identité](../fields/identity.md) pour plus d’informations.

Pour activer le schéma, sélectionnez d’abord le nom du schéma dans le rail de gauche, puis sélectionnez l’option **[!UICONTROL Profil]** bascule dans le rail de droite.

![](../../images/ui/resources/schemas/profile-toggle.png)

Une fenêtre contextuelle s’affiche, vous avertissant qu’une fois qu’un schéma a été activé et enregistré, il ne peut pas être désactivé. Sélectionner **[!UICONTROL Activer]** pour continuer.

![](../../images/ui/resources/schemas/profile-confirm.png)

La zone de travail réapparaît avec la fonction [!UICONTROL Profil] bascule activé.

>[!IMPORTANT]
>
>Comme le schéma n’est pas encore enregistré, il s’agit d’un point de non-retour si vous changez d’avis concernant la possibilité de laisser le schéma participer à Real-time Customer Profile : une fois que vous avez enregistré un schéma activé, il ne peut plus être désactivé. Sélectionnez la **[!UICONTROL Profil]** basculez à nouveau pour désactiver le schéma.

Pour terminer le processus, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma.

![](../../images/ui/resources/schemas/profile-enabled.png)

Le schéma est désormais activé pour une utilisation dans Real-time Customer Profile. Lorsque Platform ingère des données dans des jeux de données en fonction de ce schéma, ces données sont intégrées à vos données de profil fusionnées.

## Modification des noms d’affichage des champs de schéma {#display-names}

Une fois que vous avez affecté une classe et ajouté des groupes de champs à un schéma, vous pouvez modifier les noms d’affichage de l’un des champs du schéma, que ces champs aient été fournis par des ressources XDM standard ou personnalisées.

>[!NOTE]
>
>Gardez à l’esprit que les noms d’affichage des champs appartenant à des classes standard ou à des groupes de champs ne peuvent être modifiés que dans le contexte d’un schéma spécifique. En d’autres termes, la modification du nom d’affichage d’un champ standard dans un schéma n’a aucun effet sur les autres schémas qui utilisent la même classe ou le même groupe de champs associé.
>
>Une fois que vous avez apporté des modifications aux noms d’affichage des champs d’un schéma, ces modifications sont immédiatement répercutées dans les jeux de données existants basés sur ce schéma.

Pour modifier le nom d’affichage d’un champ de schéma, sélectionnez le champ dans la zone de travail. Dans le rail de droite, indiquez le nouveau nom sous **[!UICONTROL Nom d’affichage]**.

![](../../images/ui/resources/schemas/display-name.png)

Sélectionner **[!UICONTROL Appliquer]** dans le rail de droite, et la zone de travail se met à jour pour afficher le nouveau nom d’affichage du champ. Sélectionner **[!UICONTROL Enregistrer]** pour appliquer les modifications au schéma.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Modification de la classe d’un schéma {#change-class}

Vous pouvez modifier la classe d’un schéma à tout moment pendant le processus de composition initial avant l’enregistrement du schéma.

>[!WARNING]
>
>La réattribution de la classe pour un schéma doit être effectuée avec une extrême prudence. Les groupes de champs ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialise le canevas et les champs que vous avez ajoutés.

Pour réaffecter une classe, sélectionnez **[!UICONTROL Attribuer]** dans la partie gauche du canevas.

![](../../images/ui/resources/schemas/assign-class-button.png)

Une boîte de dialogue s’affiche, qui affiche une liste de toutes les classes disponibles, y compris toutes les classes définies par votre organisation (le propriétaire étant &quot;[!UICONTROL Client]&quot;) ainsi que les classes standard définies par Adobe.

Sélectionnez une classe dans la liste pour afficher sa description sur le côté droit de la boîte de dialogue. Vous pouvez également sélectionner **[!UICONTROL Aperçu de la structure de classe]** pour afficher les champs et les métadonnées associés à la classe. Sélectionner **[!UICONTROL Attribuer une classe]** pour continuer.

![](../../images/ui/resources/schemas/assign-class.png)

Une nouvelle boîte de dialogue s’ouvre, vous demandant de confirmer que vous souhaitez attribuer une nouvelle classe. Sélectionner **[!UICONTROL Attribuer]** pour confirmer.

![](../../images/ui/resources/schemas/assign-confirm.png)

Après avoir confirmé la modification de classe, le canevas est réinitialisé et toute progression de la composition est perdue.

## Étapes suivantes

Ce document couvrait les principes de base de la création et de la modification de schémas dans l’interface utilisateur de Platform. Il est vivement recommandé de consulter la section [tutoriel sur la création de schéma](../../tutorials/create-schema-ui.md) pour un processus complet de création d’un schéma complet dans l’interface utilisateur, notamment la création de groupes de champs personnalisés et de types de données pour des cas d’utilisation uniques.

Pour plus d’informations sur les fonctionnalités de la variable [!UICONTROL Schémas] workspace, voir [[!UICONTROL Schémas] présentation de workspace](../overview.md).

Pour savoir comment gérer les schémas dans le [!DNL Schema Registry] API, voir [guide de point d’entrée des schémas](../../api/schemas.md).

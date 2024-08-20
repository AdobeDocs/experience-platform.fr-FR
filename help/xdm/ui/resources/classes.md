---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;classe;classes;
solution: Experience Platform
title: Création et modification de classes dans l’interface utilisateur
description: Découvrez comment créer et modifier des classes dans l’interface utilisateur de l’Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '1560'
ht-degree: 8%

---

# Créer et modifier des classes dans l’interface utilisateur {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtre de classe standard ou personnalisé"
>abstract="La liste des classes disponibles est préfiltrée en fonction de la manière dont elles ont été créées. Sélectionnez le bouton radio pour choisir entre les options Standard et Personnalisé. L’option Standard affiche les entités créées par Adobe et inclut les classes XDM profil individuel et XDM événement d’expérience. L’option Personnalisé affiche les entités créées au sein de votre organisation. Consultez la documentation pour en savoir plus sur la création et la modification de classes."

Dans Adobe Experience Platform, une classe de schéma définit les aspects comportementaux des données que le schéma contiendra (enregistrement ou série temporelle). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

Adobe fournit plusieurs classes standard (&quot;core&quot;) Experience Data Model (XDM), y compris XDM Individual Profile et XDM ExperienceEvent. Outre ces classes de base, vous pouvez également créer vos propres classes personnalisées afin de décrire des cas d’utilisation plus spécifiques à votre organisation.

Ce document présente la création, la modification et la gestion des classes personnalisées dans l’interface utilisateur de l’Experience Platform.

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et aux [ principes de base de la composition des schémas](../../schema/composition.md) pour apprendre comment les classes contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités de l’éditeur de schémas.

## Commencer {#getting-started}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Schémas], puis sélectionnez l’onglet **[!UICONTROL Classes]**. Une liste des classes disponibles s’affiche.

## Classes de filtre {#filter}

La liste des classes est automatiquement filtrée en fonction de leur mode de création. Le paramètre par défaut affiche les classes définies par Adobe. Vous pouvez également filtrer la liste pour afficher celles créées par votre organisation. Sélectionnez le bouton radio pour choisir entre les options [!UICONTROL Standard] et [!UICONTROL Personnalisé] . L’option [!UICONTROL Standard] affiche les entités créées par Adobe et l’option [!UICONTROL Personnalisée] affiche les entités créées dans votre organisation.

![Onglet [!UICONTROL Classes] de l&#39;espace de travail [!UICONTROL Schémas] avec [!UICONTROL Standard] et [!UICONTROL Personnalisé] surligné.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Utilisez les fonctionnalités de recherche pour filtrer ou trouver une classe en fonction de son nom. Pour plus d’informations, consultez le guide sur l’ [exploration des ressources XDM](../explore.md) .

## Création d’une nouvelle classe {#create}

Il existe deux méthodes pour créer une classe dans l’interface utilisateur de Platform. Dans n’importe quel onglet de l’espace de travail [!UICONTROL Schémas], sélectionnez **[!UICONTROL Créer un schéma]** ou sélectionnez [!UICONTROL Classes] dans l’onglet **[!UICONTROL Créer une classe]**.

![L’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schémas] avec [!UICONTROL Créer un schéma] et [!UICONTROL Créer une classe] surlignée](../../images/ui/resources/classes/create-class-methods.png)

Si vous sélectionnez **[!UICONTROL Créer une classe]**, la boîte de dialogue [!UICONTROL Créer une classe] s’affiche. Saisissez un [!UICONTROL nom d’affichage] et une [!UICONTROL description] pour votre classe et choisissez le comportement prévu de votre classe avec les boutons radio. Les classes peuvent être du type, d’une série d’enregistrements ou d’une série temporelle. Sélectionnez **[!UICONTROL Créer]** pour confirmer vos choix et revenir à l’onglet [!UICONTROL Classes].

![La boîte de dialogue [!UICONTROL Créer une classe] avec [!UICONTROL Créer] surlignée.](../../images/ui/resources/classes/create-class-dialog.png)

La classe que vous avez créée est disponible et répertoriée dans la vue [!UICONTROL Classes].

![Onglet [!UICONTROL Classes] de l&#39;espace de travail [!UICONTROL Schémas] avec la classe récemment créée mise en surbrillance.](../../images/ui/resources/classes/new-class-listing.png)

### Création ou modification d’une classe {#create-or-edit}

Si vous choisissez de créer manuellement un schéma, vous pouvez également créer ou modifier une classe existante dans le cadre de ce workflow. Sélectionnez **[!UICONTROL Créer un schéma]** suivi de **[!UICONTROL Manuel]** dans la boîte de dialogue [!UICONTROL Créer un schéma] qui s’affiche.

>[!NOTE]
>
>Si vous utilisez le workflow de création de schéma assisté ML, vous pouvez charger un fichier et utiliser des algorithmes ML pour générer un schéma recommandé. Dans ce workflow de création de schéma, vous n’avez pas besoin de spécifier la classe de base de votre schéma. Pour savoir comment ML peut recommander une structure de schéma basée sur un fichier csv, consultez le [guide de création de schémas assisté par l’apprentissage automatique](../ml-assisted-schema-creation.md).

![La boîte de dialogue Créer un schéma avec les options du workflow et sélectionnez mise en surbrillance.](../../images/ui/resources/classes/manually-create-a-schema.png)

Le workflow de création de schéma s’affiche. Dans la section [!UICONTROL Schéma details], sélectionnez **[!UICONTROL Autre]**. Une liste des classes disponibles s’affiche. À partir de là, vous pouvez parcourir et filtrer les classes préexistantes sur lesquelles baser votre nouvelle classe.

>[!NOTE]
>
>Seules les classes personnalisées définies par votre organisation peuvent être entièrement modifiées et personnalisées. Pour les classes de base définies par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Pour plus d’informations, reportez-vous à la section sur la [modification des noms d’affichage des champs de schéma](./schemas.md#display-names) .
>
>Une fois qu’une classe personnalisée a été enregistrée et utilisée dans l’ingestion de données, seules des modifications supplémentaires peuvent lui être apportées par la suite. Pour plus d’informations, voir les [règles de l’évolution du schéma](../../schema/composition.md#evolution) .

![Le workflow [!UICONTROL Créer un schéma] avec [!UICONTROL Autre] surligné dans la section [!UICONTROL Détails du schéma].](../../images/ui/resources/classes/other-schema-details.png)

Sélectionnez un bouton radio pour filtrer les classes selon qu’elles sont personnalisées ou standard. Vous pouvez également filtrer les résultats disponibles en fonction de leur secteur d’activité ou rechercher une classe spécifique à l’aide du champ de recherche.

![Le workflow [!UICONTROL Créer un schéma] avec la barre de recherche, [!UICONTROL Personnalisé] et [!UICONTROL Industries] surlignée.](../../images/ui/resources/classes/filter-and-search.png)

Pour vous aider à décider de la classe appropriée, il y a des informations (![Une icône d’information.](/help/images/icons/info.png)) et aperçu (![Icône Aperçu.](/help/images/icons/preview.png)) pour chaque classe. L’icône d’information ouvre une boîte de dialogue qui fournit une description de la classe et du secteur auquel elle est associée. L’icône d’aperçu ouvre une boîte de dialogue d’aperçu pour la classe contenant un schéma et ses propriétés.

![Aperçu de la classe sélectionnée avec le schéma de schéma et les propriétés de classe mises en surbrillance.](../../images/ui/resources/classes/class-preview.png)

Sélectionnez une ligne pour choisir une classe, puis cliquez sur **[!UICONTROL Suivant]** pour confirmer votre choix.

![Le workflow [!UICONTROL Créer un schéma] avec une classe sélectionnée dans la table des classes disponibles et [!UICONTROL Suivant] surligné.](../../images/ui/resources/classes/select-class.png)

La section [!UICONTROL Nom et révision] du workflow s’affiche. Dans cette section, indiquez un nom et une description pour identifier votre schéma. &#x200B;La structure de base du schéma (fournie par la classe) s’affiche dans la zone de travail afin que vous puissiez examiner et vérifier la classe et la structure de schéma sélectionnés.

Saisissez un nom court, descriptif, unique et convivial pour la classe dans le champ de texte [!UICONTROL Nom d’affichage du schéma] . Saisissez ensuite une description appropriée pour identifier le comportement des données que le schéma définit. Une fois la structure de votre schéma revue et vos paramètres satisfaits, sélectionnez **[!UICONTROL Terminer]** pour créer votre schéma.

![La section [!UICONTROL Nom et révision] du workflow [!UICONTROL Créer un schéma] avec le [!UICONTROL nom d’affichage du schéma], la [!UICONTROL Description] et la [!UICONTROL Terminer] mise en surbrillance.](../../images/ui/resources/classes/name-and-review-class.png)

L’éditeur de schémas s’affiche, avec la structure du schéma affichée dans la zone de travail. Vous pouvez maintenant commencer [à ajouter des champs à la classe](#add-fields).

![Éditeur de schéma avec la structure du schéma affichée dans la zone de travail.](../../images/ui/resources/classes/edit.png)

## Ajout de champs à une classe {#add-fields}

Une fois que vous disposez d’un schéma qui utilise une classe personnalisée ouverte dans l’ [!UICONTROL éditeur de schémas], vous pouvez commencer à ajouter des champs à la classe . Pour ajouter un nouveau champ, sélectionnez l’icône **plus (+)** en regard du nom du schéma.

>[!IMPORTANT]
>
>Lors de la création d’un schéma qui met en oeuvre une classe définie par votre organisation, n’oubliez pas que les groupes de champs de schéma ne peuvent être utilisés qu’avec des classes compatibles. La classe que vous avez définie étant nouvelle, aucun groupe de champs compatible n’est répertorié dans la boîte de dialogue **[!UICONTROL Ajouter un groupe de champs]** . À la place, vous devrez [créer de nouveaux groupes de champs](./field-groups.md#create) à utiliser avec cette classe. La prochaine fois que vous composerez un schéma qui implémente la nouvelle classe, les groupes de champs que vous avez définis seront répertoriés et utilisables.

![ L’éditeur de schémas avec le bouton d’ajout en surbrillance.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Gardez à l’esprit que tous les champs que vous ajoutez à une classe seront utilisés dans tous les schémas qui utilisent cette classe. Vous devez donc soigneusement examiner les champs qui seront utiles dans tous les cas d’utilisation de schéma. Si vous envisagez d’ajouter un champ qui ne peut être utilisé que dans certains schémas sous cette classe, vous pouvez envisager de l’ajouter à ces schémas en [créant un groupe de champs](./field-groups.md#create) à la place.

Un espace réservé **[!UICONTROL Champ sans titre]** s’affiche dans la zone de travail et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Sous **[!UICONTROL Attribuer à]**, sélectionnez **[!UICONTROL Classe]**.

![Champ sans titre dans la zone de travail de l’éditeur de schéma avec la propriété de champ Attribuer à la classe sélectionnée et mise en surbrillance.](../../images/ui/resources/classes/assign-to-class.png)

Pour obtenir des instructions spécifiques sur la configuration et l’ajout du champ à la classe, consultez le guide sur la [définition des champs dans l’interface utilisateur](../fields/overview.md#define) . Continuez à ajouter autant de champs que nécessaire à la classe . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et la classe.

![Le nouveau schéma créé sur la zone de travail de l’éditeur de schémas, avec [!UICONTROL Enregistrer] en surbrillance.](../../images/ui/resources/classes/save.png)

Si vous avez déjà créé des schémas qui utilisent cette classe, les champs nouvellement ajoutés s’affichent automatiquement dans ces schémas.

## Modification de la classe d’un schéma {#schema}

Vous pouvez modifier la classe du schéma à tout moment pendant le processus de création initial avant qu’il ne soit enregistré. Cela doit être fait avec précaution, car les groupes de champs ne sont compatibles qu’avec certaines classes. La modification de la classe réinitialise le canevas et tous les champs que vous avez ajoutés.
Pour plus d’informations, consultez le guide sur la [création et l’édition de schémas](./schemas.md#change-class) .

## Étapes suivantes {#next-steps}

Ce document explique comment créer et modifier des classes à l’aide de l’interface utilisateur de Platform. Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

Pour savoir comment gérer les classes à l’aide de l’API Schema Registry, consultez le [guide de point de terminaison de classes](../../api/classes.md).

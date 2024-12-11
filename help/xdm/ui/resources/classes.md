---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;classe;classes;
solution: Experience Platform
title: Création et modification de classes dans l’interface utilisateur
description: Découvrez comment créer et modifier des classes dans l’interface utilisateur de l’Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: 02b709c01347c1d03f870132dff437b97f239a9c
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 7%

---

# Créer et modifier des classes dans l’interface utilisateur {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtre de classe standard ou personnalisé"
>abstract="La liste des classes disponibles est préfiltrée en fonction de la manière dont elles ont été créées. Sélectionnez le bouton radio pour choisir entre les options Standard et Personnalisé. L’option Standard affiche les entités créées par Adobe et inclut les classes XDM profil individuel et XDM événement d’expérience. L’option Personnalisé affiche les entités créées au sein de votre organisation. Consultez la documentation pour en savoir plus sur la création et la modification de classes."

Dans Adobe Experience Platform, une classe de schéma définit les aspects comportementaux des données que le schéma contiendra (enregistrement ou série temporelle). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

Adobe fournit plusieurs classes standard (&quot;core&quot;) Experience Data Model (XDM), dont [XDM Individual Profile](../../classes/individual-profile.md) et [XDM ExperienceEvent](../../classes/experienceevent.md). Outre ces classes de base, vous pouvez également créer vos propres classes personnalisées afin de décrire des cas d’utilisation plus spécifiques à votre organisation.

Ce document présente la création, la modification et la gestion des classes personnalisées dans l’interface utilisateur de l’Experience Platform.

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et aux [ principes de base de la composition des schémas](../../schema/composition.md) pour apprendre comment les classes contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités de l’éditeur de schémas.

## Commencer {#getting-started}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Schémas], puis sélectionnez l’onglet **[!UICONTROL Classes]**. Une liste des classes disponibles s’affiche.

![Nombre de classes dans l’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schémas] [!UICONTROL Classes] et [!UICONTROL Schémas] mis en surbrillance.](../../images/ui/resources/classes/available-classes.png)

## Classes de filtre {#filter}

La liste des classes est automatiquement filtrée en fonction de leur mode de création. Le paramètre par défaut affiche les classes définies par Adobe. Vous pouvez également filtrer la liste pour afficher celles créées par votre organisation. Sélectionnez le bouton radio pour choisir entre les options [!UICONTROL Standard] et [!UICONTROL Personnalisé] . L’option [!UICONTROL Standard] affiche les entités créées par Adobe et l’option [!UICONTROL Personnalisée] affiche les entités créées dans votre organisation.

![Onglet [!UICONTROL Classes] de l&#39;espace de travail [!UICONTROL Schémas] avec [!UICONTROL Standard] et [!UICONTROL Personnalisé] surligné.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Utilisez les fonctionnalités de recherche pour filtrer ou trouver une classe en fonction de son nom. Pour plus d’informations, consultez le guide sur l’ [exploration des ressources XDM](../explore.md) .

## Création d’une nouvelle classe {#create}

Il existe deux méthodes pour créer une classe dans l’interface utilisateur de Platform : **[!UICONTROL Créer une classe]** ou **[!UICONTROL Créer un schéma]**.

### Créer une classe

Sélectionnez **[!UICONTROL Créer une classe]** dans l’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schémas].

![L’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schémas] avec [!UICONTROL Créer une classe] mise en surbrillance](../../images/ui/resources/classes/create-class.png)

La boîte de dialogue [!UICONTROL Créer une classe] s’affiche. Saisissez un [!UICONTROL nom d’affichage] et une [!UICONTROL description] pour votre classe et choisissez le comportement prévu de votre classe avec les boutons radio. Les classes peuvent être du type [!UICONTROL Record] ou [!UICONTROL Time-series]. Sélectionnez **[!UICONTROL Créer]** pour confirmer vos choix et revenir à l’onglet [!UICONTROL Classes].

![La boîte de dialogue [!UICONTROL Créer une classe] avec [!UICONTROL Créer] surlignée.](../../images/ui/resources/classes/create-class-dialog.png)

La classe que vous avez créée est disponible et répertoriée dans la vue [!UICONTROL Classes].

![Onglet [!UICONTROL Classes] de l&#39;espace de travail [!UICONTROL Schémas] avec la classe récemment créée mise en surbrillance.](../../images/ui/resources/classes/new-class-listing.png)

### Créer un schéma

Vous pouvez également créer une classe en créant manuellement un schéma. Sélectionnez **[!UICONTROL Créer un schéma]** dans l’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schémas].

![L’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schémas] avec [!UICONTROL Créer un schéma] surligné](../../images/ui/resources/classes/create-schema.png)

Sélectionnez **[!UICONTROL Manuel]** dans la boîte de dialogue [!UICONTROL Créer un schéma] qui s’affiche.

>[!NOTE]
>
>Si vous utilisez le workflow de création de schéma assisté ML, vous pouvez charger un fichier et utiliser des algorithmes ML pour générer un schéma recommandé. Dans ce workflow de création de schéma, vous n’avez pas besoin de spécifier la classe de base de votre schéma. Pour savoir comment ML peut recommander une structure de schéma basée sur un fichier csv, consultez le [guide de création de schémas assisté par l’apprentissage automatique](../ml-assisted-schema-creation.md).

![La boîte de dialogue Créer un schéma avec les options du workflow et sélectionnez mise en surbrillance.](../../images/ui/resources/classes/manually-create-a-schema.png)

Le workflow de création de schéma s’affiche. Dans la section [!UICONTROL Schéma details], sélectionnez **[!UICONTROL Autre]**. Une liste des classes disponibles s’affiche. Sélectionnez **[!UICONTROL Créer une classe]**.

![Le workflow [!UICONTROL Créer un schéma] avec [!UICONTROL Autre] surligné dans la section [!UICONTROL Détails du schéma].](../../images/ui/resources/classes/other-schema-details.png)

La boîte de dialogue [!UICONTROL Créer une classe] s’affiche. Saisissez un [!UICONTROL nom d’affichage] et une [!UICONTROL description] pour votre classe et choisissez le comportement prévu de votre classe avec les boutons radio. Les classes peuvent être du type [!UICONTROL Record] ou [!UICONTROL Time-series]. Sélectionnez **[!UICONTROL Créer]** pour confirmer vos choix et revenir à l’onglet [!UICONTROL Classes].

![La boîte de dialogue [!UICONTROL Créer une classe] avec [!UICONTROL Créer] surlignée.](../../images/ui/resources/classes/create-class-from-schema.png)

La liste des classes s’actualise dans la section [!UICONTROL Détails du schéma] et la classe que vous venez de créer est automatiquement sélectionnée. Sélectionnez **[!UICONTROL Suivant]** pour continuer la création de votre schéma.

![La section [!UICONTROL Détails du schéma] avec la nouvelle classe sélectionnée et [!UICONTROL Suivant] mise en surbrillance.](../../images/ui/resources/classes/select-new-class.png)

Une fois que vous avez sélectionné une classe, la section [!UICONTROL Nom et révision] s’affiche. Dans cette section, vous fournissez un nom et une description pour identifier votre schéma. &#x200B;La structure de base du schéma (fournie par la classe) s’affiche dans la zone de travail afin que vous puissiez examiner et vérifier la classe et la structure de schéma sélectionnés.

Saisissez un [!UICONTROL nom d’affichage de schéma] convivial dans le champ de texte. Saisissez ensuite une description appropriée pour vous aider à identifier votre schéma. Une fois la structure de votre schéma revue et vos paramètres satisfaits, sélectionnez **[!UICONTROL Terminer]** pour créer votre schéma.

![La section [!UICONTROL Nom et révision] du workflow [!UICONTROL Créer un schéma] avec le [!UICONTROL nom d’affichage du schéma], la [!UICONTROL Description] et la [!UICONTROL Terminer] mise en surbrillance.](../../images/ui/resources/classes/schema-details.png)

## Ajout de champs à une classe {#add-fields}

Une fois que vous disposez d’un schéma qui utilise une classe personnalisée ouverte dans l’éditeur de schémas, vous pouvez commencer à ajouter des champs à la classe . Pour ajouter un nouveau champ, sélectionnez l’icône **plus (+)** en regard du nom du schéma.

>[!IMPORTANT]
>
>Lors de la création d’un schéma qui met en oeuvre une classe définie par votre organisation, n’oubliez pas que les groupes de champs de schéma ne peuvent être utilisés qu’avec des classes compatibles. La classe que vous avez définie étant nouvelle, aucun groupe de champs compatible n’est répertorié dans la boîte de dialogue **[!UICONTROL Ajouter un groupe de champs]** . À la place, vous devrez [créer de nouveaux groupes de champs](./field-groups.md#create) à utiliser avec cette classe. La prochaine fois que vous composerez un schéma qui implémente la nouvelle classe, les groupes de champs que vous avez définis seront répertoriés et utilisables.

![ L’éditeur de schémas avec le bouton d’ajout en surbrillance.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Gardez à l’esprit que tous les champs que vous ajoutez à une classe seront utilisés dans tous les schémas qui utilisent cette classe. Vous devez donc soigneusement examiner les champs qui seront utiles dans tous les cas d’utilisation de schéma. Si vous envisagez d’ajouter un champ qui ne peut être utilisé que dans certains schémas sous cette classe, vous pouvez envisager de l’ajouter à ces schémas en [créant un groupe de champs](./field-groups.md#create) à la place.

Un espace réservé **[!UICONTROL Champ sans titre]** s’affiche dans la zone de travail et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Sous **[!UICONTROL Attribuer à]**, sélectionnez **[!UICONTROL Classe]**.

![Champ sans titre dans la zone de travail de l’éditeur de schémas avec la propriété de champ Attribuer à la [!UICONTROL classe] sélectionnée et mise en surbrillance.](../../images/ui/resources/classes/assign-to-class.png)

Pour obtenir des instructions spécifiques sur la configuration et l’ajout du champ à la classe, consultez le guide sur la [définition des champs dans l’interface utilisateur](../fields/overview.md#define) . Continuez à ajouter autant de champs que nécessaire à la classe . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et la classe.

![Le nouveau schéma créé sur la zone de travail de l’éditeur de schémas, avec [!UICONTROL Enregistrer] en surbrillance.](../../images/ui/resources/classes/save.png)

Si vous avez déjà créé des schémas qui utilisent cette classe, les champs nouvellement ajoutés s’affichent automatiquement dans ces schémas.

## Modifier une classe (#edit-a-class)

>[!NOTE]
>
>Seules les classes personnalisées définies par votre organisation peuvent être entièrement modifiées et personnalisées. Pour les classes de base définies par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Pour plus d’informations, reportez-vous à la section sur la [modification des noms d’affichage des champs de schéma](./schemas.md#display-names) .
>
>Une fois qu’une classe personnalisée a été enregistrée et utilisée dans l’ingestion de données, seules des modifications supplémentaires peuvent lui être apportées par la suite. Pour plus d’informations, voir les [règles de l’évolution du schéma](../../schema/composition.md#evolution) .

Vous pouvez modifier une classe par le biais du workflow de schéma en éditant un schéma existant qui étend la classe ou en créant manuellement un schéma. Il n’est pas possible de modifier directement une classe. Dans l’onglet [!UICONTROL Parcourir] de l’espace de travail [!UICONTROL Schémas], sélectionnez une classe existante ou **[!UICONTROL Créer un schéma]**.

![ L’éditeur de schémas avec une classe existante et l’élément [!UICONTROL Créer un schéma] mis en surbrillance.](../../images/ui/resources/classes/edit-class-options.png)

Si vous choisissez de créer un nouveau schéma, reportez-vous à la section sur la [création d’un schéma](#create-schema) pour plus de détails. Une fois que vous avez créé le schéma (ou après avoir sélectionné un schéma existant), l’éditeur de schémas s’affiche. Pour mettre à jour un champ de classe existant, sélectionnez le champ dans la structure du schéma. Les informations du champ s’affichent dans le rail de droite. Assurez-vous que la fonction [!UICONTROL Attribuer à]
L’option **[!UICONTROL Classe]** est sélectionnée ou vos mises à jour n’affectent pas la classe.

![ L’éditeur de schémas avec un champ sélectionné et mis en surbrillance, ainsi que le rail de droite affiché, surlignant [!UICONTROL Attribuer à].](../../images/ui/resources/classes/edit-existing-field.png)

Apportez les modifications souhaitées au champ, en faisant défiler la page vers le bas dans le rail de droite pour sélectionner **[!UICONTROL Appliquer]** pour enregistrer vos modifications.

>[!IMPORTANT]
>
> Toutes les mises à jour apportées aux champs seront appliquées à tous les schémas qui utilisent cette classe, en suivant les [règles de l’évolution des schémas](../../schema/composition.md#evolution).

![Éditeur de schéma avec un champ sélectionné et le rail droit exposé, surlignant [!UICONTROL Appliquer].](../../images/ui/resources/classes/save-changes.png)

Pour ajouter de nouveaux champs, suivez le guide [add fields to a class](#add-fields-to-a-class) (Ajouter des champs à une classe). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et la classe.

![ L’éditeur de schémas avec [!UICONTROL Enregistrer] surligné.](../../images/ui/resources/classes/save-schema.png)

## Modification de la classe d’un schéma {#schema}

Vous pouvez modifier la classe du schéma à tout moment pendant le processus de création initial avant qu’il ne soit enregistré. Cela doit être fait avec précaution, car les groupes de champs ne sont compatibles qu’avec certaines classes. La modification de la classe réinitialise le canevas et tous les champs que vous avez ajoutés.
Pour plus d’informations, consultez le guide sur la [création et l’édition de schémas](./schemas.md#change-class) .

## Étapes suivantes {#next-steps}

Ce document explique comment créer et modifier des classes à l’aide de l’interface utilisateur de Platform. Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

Pour savoir comment gérer les classes à l’aide de l’API Schema Registry, consultez le [guide de point de terminaison de classes](../../api/classes.md).

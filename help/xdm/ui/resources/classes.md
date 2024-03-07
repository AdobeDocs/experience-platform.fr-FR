---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;classe;classes;
solution: Experience Platform
title: Création et modification de classes dans l’interface utilisateur
description: Découvrez comment créer et modifier des classes dans l’interface utilisateur de l’Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1458'
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

Ce guide nécessite une compréhension pratique du système XDM. Voir [Présentation de XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform, et la variable [principes de base de la composition des schémas](../../schema/composition.md) pour découvrir comment les classes contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités de l’éditeur de schémas.

## Prise en main {#getting-started}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir la [!UICONTROL Schémas] espace de travail, puis sélectionnez **[!UICONTROL Classes]** . Une liste des classes disponibles s’affiche.

## Classes de filtre {#filter}

La liste des classes est automatiquement filtrée en fonction de leur mode de création. Le paramètre par défaut affiche les classes définies par Adobe. Vous pouvez également filtrer la liste pour afficher celles créées par votre organisation. Sélectionnez le bouton radio à choisir parmi les [!UICONTROL Standard] et [!UICONTROL Personnalisé] options. La variable [!UICONTROL Standard] affiche les entités créées par l’Adobe et la variable [!UICONTROL Personnalisé] affiche les entités créées dans votre organisation.

![La variable [!UICONTROL Classes] de la [!UICONTROL Schémas] Workspace avec [!UICONTROL Standard] et [!UICONTROL Personnalisé] surlignée.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Utilisez les fonctionnalités de recherche pour filtrer ou trouver une classe en fonction de son nom. Consultez le guide sur la [exploration des ressources XDM](../explore.md) pour plus d’informations.

## Création d’une nouvelle classe {#create}

Il existe deux méthodes pour créer une classe dans l’interface utilisateur de Platform. Depuis n’importe quel onglet de la [!UICONTROL Schémas] espace de travail, sélectionnez **[!UICONTROL Créer un schéma]**, ou depuis le [!UICONTROL Classes] tab select **[!UICONTROL Créer une classe]**.

![La variable [!UICONTROL Classes] de la [!UICONTROL Schémas] Workspace avec [!UICONTROL Créer un schéma] et [!UICONTROL Créer une classe] mis en évidence](../../images/ui/resources/classes/create-class-methods.png)

Si vous sélectionnez **[!UICONTROL Créer une classe]**, la variable [!UICONTROL Créer une classe] s’affiche. Saisissez un [!UICONTROL Nom d’affichage] et [!UICONTROL Description] pour votre classe et choisissez le comportement prévu de votre classe avec les boutons radio. Les classes peuvent être du type, d’une série d’enregistrements ou d’une série temporelle. Sélectionner **[!UICONTROL Créer]** pour confirmer vos choix et revenir au [!UICONTROL Classes] .

![La variable [!UICONTROL Créer une classe] Boîte de dialogue avec [!UICONTROL Créer] surlignée.](../../images/ui/resources/classes/create-class-dialog.png)

La classe que vous avez créée est disponible et répertoriée dans le [!UICONTROL Classes] vue.

![La variable [!UICONTROL Classes] de la [!UICONTROL Schémas] espace de travail avec la classe récemment créée mise en surbrillance.](../../images/ui/resources/classes/new-class-listing.png)

### Création ou modification d’une classe {#create-or-edit}

Si vous sélectionnez **[!UICONTROL Créer un schéma]**, la variable [!UICONTROL Créer un schéma] le workflow s’affiche. Dans le [!UICONTROL Détails du schéma] , sélectionnez **[!UICONTROL Autre]**. Une liste des classes disponibles s’affiche. À partir de là, vous pouvez parcourir et filtrer les classes préexistantes sur lesquelles baser votre nouvelle classe.

>[!NOTE]
>
>Seules les classes personnalisées définies par votre organisation peuvent être entièrement modifiées et personnalisées. Pour les classes de base définies par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Voir la section sur [modification des noms d’affichage des champs de schéma](./schemas.md#display-names) pour plus d’informations.
>
>Une fois qu’une classe personnalisée a été enregistrée et utilisée dans l’ingestion de données, seules des modifications supplémentaires peuvent lui être apportées par la suite. Voir [règles d’évolution des schémas](../../schema/composition.md#evolution) pour plus d’informations.

![La variable [!UICONTROL Créer un schéma] workflow avec [!UICONTROL Autre] mis en surbrillance dans la variable [!UICONTROL Détails du schéma] .](../../images/ui/resources/classes/other-schema-details.png)

Sélectionnez un bouton radio pour filtrer les classes selon qu’elles sont personnalisées ou standard. Vous pouvez également filtrer les résultats disponibles en fonction de leur secteur d’activité ou rechercher une classe spécifique à l’aide du champ de recherche.

![La variable [!UICONTROL Créer un schéma] workflow avec la barre de recherche, [!UICONTROL Personnalisé], et [!UICONTROL Industries] surlignée.](../../images/ui/resources/classes/filter-and-search.png)

Pour vous aider à décider de la classe appropriée, il y a des informations (![Une icône d’information.](../../images/ui/resources/classes/info.png)) et aperçu (![Icône Aperçu.](../../images/ui/resources/classes/preview.png)) pour chaque classe. L’icône d’information ouvre une boîte de dialogue qui fournit une description de la classe et du secteur auquel elle est associée. L’icône d’aperçu ouvre une boîte de dialogue d’aperçu pour la classe contenant un schéma et ses propriétés.

![Un aperçu de la classe sélectionnée avec le schéma de schéma et les propriétés de classe mises en surbrillance.](../../images/ui/resources/classes/class-preview.png)

Sélectionnez une rangée pour choisir une classe, puis cliquez sur **[!UICONTROL Suivant]** pour confirmer votre choix.

![La variable [!UICONTROL Créer un schéma] workflow avec une classe sélectionnée dans la table des classes disponibles et [!UICONTROL Suivant] surlignée.](../../images/ui/resources/classes/select-class.png)

La variable [!UICONTROL Nom et révision] s’affiche. Dans cette section, indiquez un nom et une description pour identifier votre schéma. &#x200B;La structure de base du schéma (fournie par la classe) s’affiche dans la zone de travail afin que vous puissiez examiner et vérifier la classe et la structure de schéma sélectionnés.

Saisissez un nom court, descriptif, unique et convivial pour la classe dans la variable [!UICONTROL Nom d’affichage du schéma] Champ de texte. Saisissez ensuite une description appropriée pour identifier le comportement des données que le schéma définit. Une fois la structure de votre schéma revue et vos paramètres passés, sélectionnez **[!UICONTROL Terminer]** pour créer votre schéma.

![La variable [!UICONTROL Nom et révision] de la [!UICONTROL Créer un schéma] avec la méthode [!UICONTROL Nom d’affichage du schéma], [!UICONTROL Description], et [!UICONTROL Terminer] surlignée.](../../images/ui/resources/classes/name-and-review-class.png)

L’éditeur de schémas s’affiche, avec la structure du schéma affichée dans la zone de travail. Vous pouvez maintenant commencer. [ajout de champs à la classe](#add-fields).

![L’éditeur de schémas avec la structure du schéma affichée dans la zone de travail.](../../images/ui/resources/classes/edit.png)

## Ajout de champs à une classe {#add-fields}

Une fois que vous disposez d’un schéma qui utilise une classe personnalisée ouverte dans le [!UICONTROL Éditeur de schéma], vous pouvez commencer à ajouter des champs à la classe . Pour ajouter un nouveau champ, sélectionnez l’option **plus (+)** en regard du nom du schéma.

>[!IMPORTANT]
>
>Lors de la création d’un schéma qui met en oeuvre une classe définie par votre organisation, n’oubliez pas que les groupes de champs de schéma ne peuvent être utilisés qu’avec des classes compatibles. La classe que vous avez définie étant nouvelle, aucun groupe de champs compatible n’est répertorié dans la variable **[!UICONTROL Ajouter un groupe de champs]** boîte de dialogue. Vous devrez au contraire : [créer des groupes de champs ;](./field-groups.md#create) à utiliser avec cette classe. La prochaine fois que vous composerez un schéma qui implémente la nouvelle classe, les groupes de champs que vous avez définis seront répertoriés et utilisables.

![Éditeur de schéma avec le bouton d’ajout en surbrillance.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Gardez à l’esprit que tous les champs que vous ajoutez à une classe seront utilisés dans tous les schémas qui utilisent cette classe. Vous devez donc soigneusement examiner les champs qui seront utiles dans tous les cas d’utilisation de schéma. Si vous envisagez d’ajouter un champ qui ne peut être utilisé que dans certains schémas sous cette classe, vous pouvez envisager de l’ajouter à ces schémas en [créer un groupe de champs](./field-groups.md#create) au lieu de .

Un **[!UICONTROL Champ sans titre]** un espace réservé apparaît dans la zone de travail et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Sous **[!UICONTROL Attribuer à]**, sélectionnez **[!UICONTROL Classe]**.

![Champ sans titre dans la zone de travail de l’éditeur de schéma avec la propriété de champ Attribuer à la classe sélectionnée et mise en surbrillance.](../../images/ui/resources/classes/assign-to-class.png)

Consultez le guide sur la [définition des champs dans l’interface utilisateur](../fields/overview.md#define) pour obtenir des instructions spécifiques sur la configuration et l’ajout du champ à la classe . Continuez à ajouter autant de champs que nécessaire à la classe . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et la classe.

![Le nouveau schéma créé sur la zone de travail de l’éditeur de schémas, avec [!UICONTROL Enregistrer] surlignée.](../../images/ui/resources/classes/save.png)

Si vous avez déjà créé des schémas qui utilisent cette classe, les champs nouvellement ajoutés s’affichent automatiquement dans ces schémas.

## Modification de la classe d’un schéma {#schema}

Vous pouvez modifier la classe du schéma à tout moment pendant le processus de création initial avant qu’il ne soit enregistré. Cela doit être fait avec précaution, car les groupes de champs ne sont compatibles qu’avec certaines classes. La modification de la classe réinitialise le canevas et tous les champs que vous avez ajoutés.
Consultez le guide sur la [création et édition de schémas](./schemas.md#change-class) pour plus d’informations.

## Étapes suivantes {#next-steps}

Ce document explique comment créer et modifier des classes à l’aide de l’interface utilisateur de Platform. Pour plus d’informations sur les fonctionnalités de la variable [!UICONTROL Schémas] workspace, voir [[!UICONTROL Schémas] présentation de workspace](../overview.md).

Pour savoir comment gérer les classes à l’aide de l’API Schema Registry, reportez-vous à la section [guide de point de terminaison des classes](../../api/classes.md).

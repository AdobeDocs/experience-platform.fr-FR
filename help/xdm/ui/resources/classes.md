---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;interface utilisateur;espace de travail;classe;classes;
solution: Experience Platform
title: Créer et modifier des classes dans l’interface utilisateur
description: Découvrez comment créer et modifier des classes dans l’interface utilisateur Experience Platform.
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: a05ee385694b028b513e2fa632079e665ba815bb
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 8%

---

# Créer et modifier des classes dans l’interface utilisateur {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_class_filter"
>title="Filtre de classe standard ou personnalisé"
>abstract="La liste des classes disponibles est préfiltrée en fonction de la manière dont elles ont été créées. Sélectionnez le bouton radio pour choisir entre les options Standard et Personnalisé. L’option Standard affiche les entités créées par Adobe et inclut les classes XDM profil individuel et XDM événement d’expérience. L’option Personnalisé affiche les entités créées au sein de votre organisation. Consultez la documentation pour en savoir plus sur la création et la modification de classes."

Dans Adobe Experience Platform, la classe d’un schéma définit les aspects comportementaux des données que le schéma contiendra (enregistrement ou série temporelle). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

Adobe fournit plusieurs classes de modèle de données d’expérience (XDM) standard (« core »), notamment [XDM Individual Profile](../../classes/individual-profile.md) et [XDM ExperienceEvent](../../classes/experienceevent.md). Outre ces classes principales, vous pouvez également créer vos propres classes personnalisées pour décrire des cas d’utilisation plus spécifiques pour votre organisation.

Ce document présente la création, la modification et la gestion de classes personnalisées dans l’interface utilisateur d’Experience Platform.

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une introduction au rôle de XDM dans l’écosystème Experience Platform et aux [principes de base de la composition de schémas](../../schema/composition.md) afin de découvrir comment les classes contribuent aux schémas XDM.

Bien que cela ne soit pas obligatoire pour ce guide, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités de l’éditeur de schémas.

## Commencer {#getting-started}

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Schemas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Schemas], puis sélectionnez l’onglet **[!UICONTROL Classes]** . Une liste des classes disponibles s’affiche.

![Le des classes dans l’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schemas] [!UICONTROL Classes] et [!UICONTROL Schemas] mis en surbrillance.](../../images/ui/resources/classes/available-classes.png)

## Classes de filtre {#filter}

La liste des classes est automatiquement filtrée en fonction de leur mode de création. Le paramètre par défaut affiche les classes définies par Adobe. Vous pouvez également filtrer la liste pour afficher celles créées par votre organisation. Sélectionnez le bouton radio pour choisir entre les options [!UICONTROL Standard] et [!UICONTROL Custom]. L’option [!UICONTROL Standard] affiche les entités créées par Adobe et l’option [!UICONTROL Custom] affiche les entités créées au sein de votre organisation.

![Onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schemas] avec [!UICONTROL Standard] et [!UICONTROL Custom] en surbrillance.](../../images/ui/resources/classes/standard-and-custom-classes.png)

>[!TIP]
>
>Utilisez les fonctionnalités de recherche pour filtrer ou rechercher une classe en fonction de son nom. Pour plus d’informations, consultez le guide sur l’[exploration des ressources XDM](../explore.md).

## Création d’une nouvelle classe {#create}

Il existe deux méthodes de création d’une classe dans l’interface utilisateur d’Experience Platform, par **[!UICONTROL Create class]** ou **[!UICONTROL Create schema]**.

### Créer une classe

Sélectionnez **[!UICONTROL Create class]** dans l’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schemas].

![Onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schemas] avec [!UICONTROL Create class] mis en surbrillance](../../images/ui/resources/classes/create-class.png)

La boîte de dialogue [!UICONTROL Create class] s’affiche. Saisissez un [!UICONTROL Display name] et un [!UICONTROL Description] pour votre classe, puis choisissez le comportement prévu de votre classe à l’aide des boutons radio. Les classes peuvent être du type [!UICONTROL Record] ou [!UICONTROL Time-series]. Sélectionnez **[!UICONTROL Create]** pour confirmer vos choix et revenir à l’onglet [!UICONTROL Classes] .

![Boîte de dialogue [!UICONTROL Create class] avec [!UICONTROL Create] mise en surbrillance.](../../images/ui/resources/classes/create-class-dialog.png)

La classe que vous avez créée est disponible et répertoriée dans la vue [!UICONTROL Classes].

![Onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schemas] avec la classe récemment créée en surbrillance.](../../images/ui/resources/classes/new-class-listing.png)

### Créer un schéma

Vous pouvez également créer une classe en créant manuellement un schéma. Sélectionnez **[!UICONTROL Create schema]** dans l’onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schemas].

![Onglet [!UICONTROL Classes] de l’espace de travail [!UICONTROL Schemas] avec [!UICONTROL Create schema] mis en surbrillance](../../images/ui/resources/classes/create-schema.png)

Sélectionnez **[!UICONTROL Manual]** dans la boîte de dialogue [!UICONTROL Create a schema] qui s’affiche.

>[!NOTE]
>
>Si vous utilisez le workflow de création de schéma assistée par ML, vous pouvez charger un fichier et utiliser des algorithmes ML pour générer un schéma recommandé. Dans ce workflow de création de schéma, vous n’avez pas besoin de spécifier la classe de base pour votre schéma. Pour découvrir comment ML peut recommander une structure de schéma basée sur un fichier csv, consultez le guide [création de schéma assistée par machine learning](../ml-assisted-schema-creation.md).

![La boîte de dialogue Créer un schéma avec les options de workflow et sélectionnez en surbrillance.](../../images/ui/resources/classes/manually-create-a-schema.png)

Le workflow de création de schéma s’affiche. Dans la section [!UICONTROL Schema details], sélectionnez **[!UICONTROL Other]**. Une liste des classes disponibles s’affiche. Sélectionnez **[!UICONTROL Create class]**.

![Workflow [!UICONTROL Create schema] avec [!UICONTROL Other] mis en surbrillance dans la section [!UICONTROL Schema details].](../../images/ui/resources/classes/other-schema-details.png)

La boîte de dialogue [!UICONTROL Create class] s’affiche. Saisissez un [!UICONTROL Display name] et un [!UICONTROL Description] pour votre classe, puis choisissez le comportement prévu de votre classe à l’aide des boutons radio. Les classes peuvent être du type [!UICONTROL Record] ou [!UICONTROL Time-series]. Sélectionnez **[!UICONTROL Create]** pour confirmer vos choix et revenir à l’onglet [!UICONTROL Classes] .

![Boîte de dialogue [!UICONTROL Create class] avec [!UICONTROL Create] mise en surbrillance.](../../images/ui/resources/classes/create-class-from-schema.png)

La liste des classes est actualisée dans la section [!UICONTROL Schema details] et la classe que vous venez de créer est automatiquement sélectionnée. Sélectionnez **[!UICONTROL Next]** pour continuer à créer votre schéma.

![La section [!UICONTROL Schema details] avec la nouvelle classe sélectionnée et [!UICONTROL Next] mise en surbrillance.](../../images/ui/resources/classes/select-new-class.png)

Après avoir sélectionné une classe, la section [!UICONTROL Name and review] s’affiche. Dans cette section, vous indiquez un nom et une description pour identifier votre schéma. &#x200B;La structure de base du schéma (fournie par la classe ) s’affiche dans la zone de travail. Vous pouvez ainsi consulter et vérifier la structure de classe et de schéma sélectionnée.

Saisissez un [!UICONTROL Schema display name] convivial dans le champ de texte. Saisissez ensuite une description appropriée pour vous aider à identifier votre schéma. Une fois que vous avez révisé votre structure de schéma et que vos paramètres vous conviennent, sélectionnez **[!UICONTROL Finish]** pour créer votre schéma.

![Section [!UICONTROL Name and review] du workflow de [!UICONTROL Create schema] avec les [!UICONTROL Schema display name], [!UICONTROL Description] et [!UICONTROL Finish] en surbrillance.](../../images/ui/resources/classes/schema-details.png)

## Ajouter des champs à une classe {#add-fields}

Une fois que vous disposez d’un schéma qui utilise une classe personnalisée ouverte dans l’éditeur de schémas, vous pouvez commencer à ajouter des champs à la classe . Pour ajouter un nouveau champ, sélectionnez l’icône **plus (+)** à côté du nom du schéma.

>[!IMPORTANT]
>
>Lors de la création d’un schéma qui implémente une classe définie par votre organisation, n’oubliez pas que les groupes de champs de schéma ne peuvent être utilisés qu’avec des classes compatibles. Comme la classe que vous avez définie est nouvelle, aucun groupe de champs compatible n’est répertorié dans la boîte de dialogue **[!UICONTROL Add field group]**. À la place, vous devez [créer de nouveaux groupes de champs](./field-groups.md#create) à utiliser avec cette classe. La prochaine fois que vous composerez un schéma qui implémente la nouvelle classe, les groupes de champs que vous avez définis seront répertoriés et disponibles.

![Éditeur de schémas avec le bouton d’ajout en surbrillance.](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Gardez à l’esprit que tous les champs que vous ajoutez à une classe seront utilisés dans tous les schémas qui utilisent cette classe. Vous devez donc soigneusement réfléchir aux champs qui seront utiles dans tous les cas d’utilisation de schéma. Si vous envisagez d’ajouter un champ qui ne peut être utilisé que dans certains schémas sous cette classe, vous pouvez l’ajouter à ces schémas en [créant un groupe de champs](./field-groups.md#create) à la place.

Un espace réservé **[!UICONTROL Untitled Field]** apparaît dans la zone de travail, et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Sous **[!UICONTROL Assign to]**, sélectionnez **[!UICONTROL Class]**.

![Champ sans titre dans la zone de travail de l’éditeur de schémas avec la propriété Affecter à [!UICONTROL Class] champ sélectionnée et mise en surbrillance.](../../images/ui/resources/classes/assign-to-class.png)

Consultez le guide sur la [définition de champs dans l’interface utilisateur](../fields/overview.md#define) pour obtenir des instructions spécifiques sur la configuration et l’ajout du champ à la classe . Continuez à ajouter autant de champs que nécessaire à la classe. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]** pour enregistrer le schéma et la classe.

![Schéma nouvellement créé dans la zone de travail de l’éditeur de schémas, avec les [!UICONTROL Save] en surbrillance.](../../images/ui/resources/classes/save.png)

Si vous avez précédemment créé des schémas qui utilisent cette classe, les nouveaux champs ajoutés apparaîtront automatiquement dans ces schémas.

## Modification d’une classe {#edit-a-class}

>[!NOTE]
>
>Seules les classes personnalisées définies par votre organisation peuvent être entièrement modifiées et personnalisées. Pour les classes de base définies par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte des schémas individuels. Pour plus d’informations, consultez la section sur la [modification des noms d’affichage des champs de schéma](./schemas.md#display-names).
>
>Une fois qu’une classe personnalisée a été enregistrée et utilisée dans l’ingestion de données, seules des modifications supplémentaires peuvent lui être apportées par la suite. Pour plus d’informations, consultez la section [règles d’évolution des schémas](../../schema/composition.md#evolution) .

Vous pouvez modifier une classe par le biais du workflow de schéma en modifiant un schéma existant qui étend la classe ou en créant manuellement un schéma. Il n’est pas possible de modifier directement une classe. Dans l’onglet [!UICONTROL Browse] de l’espace de travail [!UICONTROL Schemas], sélectionnez une classe ou un **[!UICONTROL Create a schema]** existant.

![Éditeur de schémas avec une classe existante et le [!UICONTROL Create a schema] mis en surbrillance.](../../images/ui/resources/classes/edit-class-options.png)

Si vous choisissez de créer un schéma, consultez la section sur la [création d’un schéma](#create-schema) pour plus d’informations. Une fois que vous avez terminé de créer le schéma (ou après avoir sélectionné un schéma existant), l’éditeur de schémas s’affiche. Pour mettre à jour un champ de classe existant, sélectionnez le champ dans la structure du schéma. Les informations du champ s’affichent dans le rail de droite. Assurez-vous de la [!UICONTROL Assign to]
l’option **[!UICONTROL Class]** est sélectionnée ou vos mises à jour n’affectent pas la classe.

![Éditeur de schémas avec un champ sélectionné et mis en surbrillance, et le rail de droite exposé, mettant en surbrillance [!UICONTROL Assign to].](../../images/ui/resources/classes/edit-existing-field.png)

Apportez les modifications souhaitées au champ, en faisant défiler le rail de droite vers le bas pour sélectionner **[!UICONTROL Apply]** enregistrer vos modifications.

>[!IMPORTANT]
>
> Toutes les mises à jour que vous apportez aux champs seront appliquées dans tous les schémas qui utilisent cette classe, conformément aux [ règles d’évolution des schémas ](../../schema/composition.md#evolution).

![Éditeur de schémas avec un champ sélectionné et le rail de droite exposé, mettant en surbrillance [!UICONTROL Apply].](../../images/ui/resources/classes/save-changes.png)

Pour ajouter de nouveaux champs, suivez le guide [ajouter des champs à une classe](#add-fields-to-a-class). Lorsque vous avez terminé, sélectionnez **[!UICONTROL Save]** pour enregistrer le schéma et la classe.

![Éditeur de schémas avec le [!UICONTROL Save] mis en surbrillance.](../../images/ui/resources/classes/save-schema.png)

## Modification de la classe d’un schéma {#schema}

Vous pouvez modifier la classe du schéma à tout moment au cours du processus de création initiale, avant qu’il ne soit enregistré. Toutefois, cette opération doit être effectuée avec précaution, car les groupes de champs ne sont compatibles qu’avec certaines classes. La modification de la classe réinitialise la zone de travail et tous les champs que vous avez ajoutés.
Pour plus d’informations, consultez le guide sur la [création et modification de schémas](./schemas.md#change-class).

## Étapes suivantes {#next-steps}

Ce document explique comment créer et modifier des classes à l’aide de l’interface utilisateur d’Experience Platform. Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schemas], consultez la présentation de l’espace de travail [[!UICONTROL Schemas]](../overview.md).

Pour savoir comment gérer des classes à l’aide de l’API Schema Registry, consultez le guide de point d’entrée [classes](../../api/classes.md).

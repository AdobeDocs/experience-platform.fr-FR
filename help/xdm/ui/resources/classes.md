---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;classe;classes;
solution: Experience Platform
title: Création et modification de classes dans l’interface utilisateur
description: Découvrez comment créer et modifier des classes dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 1b4c3996-2319-45dd-9edd-a5bcad46578b
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 5%

---

# Création et modification de classes dans l’interface utilisateur

Dans le modèle de données d’expérience (XDM), les classes définissent les aspects comportementaux des données qu’un schéma contiendra (enregistrement ou série temporelle). En outre, les classes décrivent le plus petit de nombres de propriétés communes que tous les schémas basés sur cette classe doivent inclure et fournir une manière de fusionner plusieurs jeux de données compatibles.

Adobe fournit plusieurs classes XDM standard (&quot;core&quot;), y compris [!DNL XDM Individual Profile] et [!DNL XDM ExperienceEvent]. Outre ces classes principales, vous pouvez créer vos propres classes personnalisées afin de décrire des cas d’utilisation plus spécifiques à votre organisation.

Ce document présente comment créer, modifier et gérer des classes personnalisées dans l’interface utilisateur de Adobe Experience Platform.

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et les [bases de la composition des schémas](../../schema/composition.md) pour découvrir comment les classes contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) afin de vous familiariser avec les différentes fonctionnalités de [!DNL Schema Editor].

## Création d’une nouvelle classe {#create}

Dans l’espace de travail **[!UICONTROL Schémas]**, sélectionnez **[!UICONTROL Créer un schéma]**, puis sélectionnez **[!UICONTROL Parcourir]** dans la liste déroulante.

![](../../images/ui/resources/classes/browse-classes.png)

Une boîte de dialogue s’affiche, vous permettant de sélectionner une classe dans la liste des classes disponibles. Dans la partie supérieure de la boîte de dialogue, sélectionnez **[!UICONTROL Créer une nouvelle classe]**. Vous pouvez ensuite attribuer à votre nouvelle classe un nom d’affichage (un nom court, descriptif, unique et convivial pour la classe), une description et un comportement pour les données que le schéma définira (&quot;[!UICONTROL Enregistrer]&quot; ou &quot;[!UICONTROL Série temporelle]&quot;).

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Attribuer la classe]**.

![](../../images/ui/resources/classes/class-details.png)

[!DNL Schema Editor] s’affiche, affichant un nouveau schéma dans la zone de travail basé sur la classe personnalisée que vous venez de créer. Comme aucun champ n’a encore été ajouté à la classe, le schéma ne contient qu’un champ `_id`, qui représente l’identifiant unique généré par le système qui est automatiquement appliqué à toutes les ressources dans la balise [!DNL Schema Registry].

![](../../images/ui/resources/classes/schema.png)

>[!IMPORTANT]
>
>Lors de la création d’un schéma qui met en oeuvre une classe définie par votre organisation, n’oubliez pas que les groupes de champs de schéma ne peuvent être utilisés qu’avec des classes compatibles. La classe que vous avez définie étant nouvelle, aucun groupe de champs compatible n’est répertorié dans la boîte de dialogue **[!UICONTROL Ajouter un groupe de champs]** . Vous devez plutôt [créer des groupes de champs](./field-groups.md#create) à utiliser avec cette classe. La prochaine fois que vous composerez un schéma qui implémente la nouvelle classe, les groupes de champs que vous avez définis seront répertoriés et utilisables.

Vous pouvez maintenant commencer [à ajouter des champs à la classe](#add-fields), qui sera partagée par tous les schémas qui utilisent la classe.

## Modification d’une classe existante {#edit}

>[!NOTE]
>
>Seules les classes personnalisées définies par votre organisation peuvent être entièrement modifiées et personnalisées. Pour les classes de base définies par Adobe, seuls les noms d’affichage de leurs champs peuvent être modifiés dans le contexte de schémas individuels. Pour plus d’informations, reportez-vous à la section [Modification des noms d’affichage pour les champs de schéma](./schemas.md#display-names) .
>
>Une fois qu’une classe personnalisée a été enregistrée et utilisée dans l’ingestion de données, seules des modifications supplémentaires peuvent lui être apportées par la suite. Pour plus d’informations, consultez les [règles de l’évolution du schéma](../../schema/composition.md#evolution) .

Pour modifier une classe existante, sélectionnez l’onglet **[!UICONTROL Parcourir]**, puis sélectionnez le nom d’un schéma qui utilise la classe que vous souhaitez modifier.

![](../../images/ui/resources/classes/select-for-edit.png)

>[!TIP]
>
>Vous pouvez utiliser les fonctionnalités de recherche et de filtrage de l’espace de travail pour faciliter la recherche du schéma. Pour plus d’informations, consultez le guide sur l’ [exploration des ressources XDM](../explore.md) .

[!DNL Schema Editor] s’affiche, avec la structure du schéma affichée dans la zone de travail. Vous pouvez maintenant commencer [à ajouter des champs à la classe](#add-fields).

![](../../images/ui/resources/classes/edit.png)

## Ajout de champs à une classe {#add-fields}

Une fois qu’un schéma utilise une classe personnalisée ouverte dans l’ [!UICONTROL éditeur de schémas], vous pouvez commencer à ajouter des champs à la classe. Pour ajouter un nouveau champ, cliquez sur l’icône **plus (+)** en regard du nom du schéma.

![](../../images/ui/resources/classes/add-field.png)

>[!IMPORTANT]
>
>Gardez à l’esprit que tous les champs que vous ajoutez à une classe seront utilisés dans tous les schémas qui utilisent cette classe. Vous devez donc soigneusement examiner les champs qui seront utiles dans tous les cas d’utilisation de schéma. Si vous envisagez d’ajouter un champ qui ne peut être utilisé que dans certains schémas sous cette classe, vous pouvez envisager de l’ajouter à ces schémas en [créant un groupe de champs](./field-groups.md#create) à la place.

Un **[!UICONTROL nouveau champ]** apparaît dans la zone de travail et le rail de droite se met à jour pour afficher les commandes permettant de configurer les propriétés du champ. Consultez le guide sur la [définition des champs dans l’interface utilisateur](../fields/overview.md#define) pour obtenir des instructions spécifiques sur la configuration et l’ajout du champ à la classe .

Continuez à ajouter autant de champs que nécessaire à la classe . Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma et la classe.

![](../../images/ui/resources/classes/save.png)

Si vous avez déjà créé des schémas qui utilisent cette classe, les champs nouvellement ajoutés s’affichent automatiquement dans ces schémas.

## Modification de la classe d’un schéma {#schema}

Vous pouvez modifier la classe du schéma à tout moment pendant le processus de création initial avant qu’il ne soit enregistré. Pour plus d’informations, consultez le guide sur la [création et l’édition de schémas](./schemas.md#change-class) .

## Étapes suivantes

Ce document explique comment créer et modifier des classes à l’aide de l’interface utilisateur de Platform. Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

Pour savoir comment gérer les classes à l’aide de l’API [!DNL Schema Registry], consultez le [guide de point de terminaison des classes](../../api/classes.md).

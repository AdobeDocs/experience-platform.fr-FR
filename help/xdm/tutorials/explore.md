---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Explorez les ressources XDM dans l’interface utilisateur.
description: Ce didacticiel décrit les étapes à suivre pour explorer les schémas, classes, mixins et types de données existants dans l’interface utilisateur de l’Experience Platform.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 49d37cdf14bd03b62fe64116842bacd0f806e5ce
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---


# Explorez les ressources XDM dans l’interface utilisateur.

Dans Adobe Experience Platform, toutes les ressources du modèle de données d’expérience (XDM) sont stockées dans la [!DNL Schema Library], y compris les ressources standard fournies par l’Adobe et les ressources personnalisées définies par votre organisation. Dans l’interface utilisateur de l’Experience Platform, vous pouvez vue la structure et les champs de tout schéma, classe, mixin ou type de données existant dans le [!DNL Schema Library]. Cela s&#39;avère particulièrement utile lors de la planification et de la préparation de l&#39;assimilation de données, car l&#39;interface utilisateur fournit des informations sur les types de données attendus et les cas d&#39;utilisation de chaque champ fourni par ces ressources XDM.

Ce didacticiel décrit les étapes à suivre pour explorer les schémas, classes, mixins et types de données existants dans l’interface utilisateur de l’Experience Platform.

## Rechercher une ressource XDM {#lookup}

In the Platform UI, select **[!UICONTROL Schemas]** in the left navigation. L&#39;espace de travail [!UICONTROL Schémas] fournit un onglet de **[!UICONTROL navigation]** pour explorer toutes les ressources XDM existantes de votre organisation, ainsi que d&#39;autres onglets dédiés pour explorer **[!UICONTROL les classes]**, les **[!UICONTROL mixins et les types Dataplus particulièrement.]******

![](../images/tutorials/explore/tabs.png)

Dans l’onglet [!UICONTROL Parcourir] , vous pouvez utiliser l’icône de filtre (Image![de l’icône de](../images/tutorials/explore/icon.png)filtre) pour afficher les commandes du rail de gauche afin de réduire les résultats répertoriés.

Par exemple, pour filtrer la liste afin de n’afficher que les types de données standard fournis par l’Adobe, sélectionnez **[!UICONTROL Type]** de données et **[!UICONTROL Adobe]** sous les sections **[!UICONTROL Type]** et **[!UICONTROL Propriétaire, respectivement.]**

La bascule **[!UICONTROL Inclus dans le Profil]** vous permet de filtrer les résultats afin de n’afficher que les ressources utilisées dans les schémas qui ont été activés pour une utilisation dans le Profil [client en temps](../../profile/home.md)réel.

![](../images/tutorials/explore/filter.png)

Vous pouvez également utiliser la barre de recherche pour restreindre les résultats aux ressources dont les noms correspondent à la requête de recherche.

![](../images/tutorials/explore/search.png)

Une fois que vous avez trouvé la ressource que vous souhaitez explorer, sélectionnez son nom dans la liste pour la vue de sa structure dans le canevas.

## Explorer une ressource XDM dans la trame {#explore}

Une fois que vous sélectionnez une ressource, sa structure s&#39;ouvre dans la trame.

![](../images/tutorials/explore/canvas.png)

Tous les champs de type objet contenant des sous-propriétés sont réduits par défaut lorsqu’ils apparaissent pour la première fois dans la trame. Pour afficher les sous-propriétés d’un champ, sélectionnez l’icône en regard de son nom.

![](../images/tutorials/explore/field-expand.png)

### Champs générés par le système {#system-fields}

Certains champs de schéma sont précédés d’un trait de soulignement, tel que `_repo` et `_id`. Il s’agit d’espaces réservés pour les champs que le système génère et attribue automatiquement lorsque des données sont ingérées.

En tant que tel, la plupart de ces champs doivent être exclus de la structure de vos données lors de l&#39;assimilation dans la plate-forme, à l&#39;exception principale du champ `_{TENANT_ID}` , sous lequel tous les champs XDM créés sous votre organisation doivent être espacés de noms.

### Types des données {#data-types}

Pour chaque champ affiché dans la zone de travail, le type de données correspondant s’affiche en regard de son nom, indiquant d’un seul coup d’oeil le type de données attendu pour l’assimilation par le champ.

Tout type de données ajouté entre crochets (`[]`) représente un tableau de ce type de données particulier. Par exemple, un type de données **[!UICONTROL String]\[]** indique que le champ attend un tableau de valeurs de chaîne. Un type de données d&#39;élément **[!UICONTROL de]paiement\[]** indique un tableau d&#39;objets conformes au type de données d&#39;élément [!UICONTROL de] paiement.

Si un champ de tableau est basé sur un type d&#39;objet, vous pouvez sélectionner son icône dans la trame pour afficher les attributs attendus pour chaque élément de tableau.

![](../images/tutorials/explore/array-type.png)

### [!UICONTROL Propriétés de champ] {#field-properties}

Lorsque vous sélectionnez le nom d’un champ du canevas, le rail de droite se met à jour pour afficher des détails sur ce champ sous les propriétés **[!UICONTROL de]** champ. Cela peut inclure une description du cas d’utilisation prévu du champ, des valeurs par défaut, des modèles, des formats, que le champ soit obligatoire ou non, etc.

![](../images/tutorials/explore/field-properties.png)

Si le champ que vous inspectez est un champ enum, le rail droit affiche également les valeurs acceptables que le champ attend de recevoir.

![](../images/tutorials/explore/enum-field.png)

### Champs d’identité {#identity}

Lors de l’inspection des schémas qui contiennent des champs d’identité, ces champs sont mis en surbrillance dans la zone de travail avec une icône d’empreinte digitale (Image![de l’icône](../images/tutorials/explore/identity-symbol.png)empreinte digitale). Si vous sélectionnez le nom du champ d&#39;identité, vous pouvez vue des informations supplémentaires telles que l&#39;espace de nommage [d&#39;](../../identity-service/namespaces.md) identité et déterminer si le champ est ou non l&#39;Principale identité du schéma.

![](../images/tutorials/explore/identity-field.png)

### Champs de relation {#relationship}

Les champs de relation sont également surlignés de manière unique dans la trame, en indiquant le nom du schéma de destination référencé par le champ. Si vous sélectionnez le nom du champ de relation, vous pouvez vue l&#39;espace de nommage d&#39;identité de l&#39;identité Principale du schéma de destination.

![](../images/tutorials/explore/relationship-field.png)

>[!NOTE]
>
>Pour plus d&#39;informations sur l&#39;utilisation des relations dans les schémas XDM, consultez le didacticiel sur la [création d&#39;une relation dans l&#39;interface utilisateur](./create-schema-ui.md) .

## Étapes suivantes

Ce document explique comment explorer les ressources XDM existantes dans l’interface utilisateur Experience Platform. Pour plus d&#39;informations sur les différentes fonctionnalités de l&#39;espace de travail [!UICONTROL Schémas] et [!DNL Schema Editor], consultez le didacticiel [sur la création de](./create-schema-ui.md)schémas.
---
keywords: Experience Platform ; accueil ; rubriques populaires ; ui ; IU ; XDM ; système XDM ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données d’expérience ; modèle de données ; modèle de données ; modèle de données ; explorer ; classe ; groupe de champs ; type de données ; schéma ;
solution: Experience Platform
title: Explorer les ressources XDM dans l’interface utilisateur
description: Découvrez comment explorer les schémas, classes, groupes de champs de schéma et types de données existants dans l’interface utilisateur de l’Experience Platform.
topic-legacy: tutorial
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 0%

---

# Explorez les ressources XDM dans l’interface utilisateur.

Dans Adobe Experience Platform, toutes les ressources du modèle de données d’expérience (XDM) sont stockées dans [!DNL Schema Library], y compris les ressources standard fournies par l’Adobe et les ressources personnalisées définies par votre organisation. Dans l&#39;interface utilisateur de l&#39;Experience Platform, vous pouvez vue la structure et les champs de tout schéma, classe, groupe de champs de schéma ou type de données existant dans [!DNL Schema Library]. Cela s&#39;avère particulièrement utile lors de la planification et de la préparation de l&#39;assimilation de données, car l&#39;interface utilisateur fournit des informations sur les types de données attendus et les cas d&#39;utilisation de chaque champ fourni par ces ressources XDM.

Ce didacticiel décrit les étapes à suivre pour explorer les schémas, classes, groupes de champs et types de données existants dans l’interface utilisateur de l’Experience Platform.

## Rechercher une ressource XDM {#lookup}

Dans l’interface utilisateur de la plate-forme, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. L&#39;espace de travail [!UICONTROL Schémas] fournit un onglet **[!UICONTROL Parcourir]** pour explorer toutes les ressources XDM existantes de votre organisation, ainsi que d&#39;autres onglets dédiés pour explorer **[!UICONTROL Classes]**, **[!UICONTROL Groupes de champs]** et **[!UICONTROL Types de données]** spécifiquement.

![](../images/ui/explore/tabs.png)

Sur l’onglet [!UICONTROL Parcourir], vous pouvez utiliser l’icône de filtre (![Image de l’icône de filtre](../images/ui/explore/icon.png)) pour afficher les commandes du rail de gauche afin de réduire les résultats répertoriés.

Par exemple, pour filtrer la liste afin d’afficher uniquement les types de données standard fournis par l’Adobe, sélectionnez **[!UICONTROL Type de données]** et **[!UICONTROL Adobe]** sous les sections **[!UICONTROL Type]** et **[!UICONTROL Propriétaire]**, respectivement.

La bascule **[!UICONTROL Inclus dans le Profil]** vous permet de filtrer les résultats pour n&#39;afficher que les ressources utilisées dans les schémas qui ont été activés pour l&#39;utilisation dans [Profil client en temps réel](../../profile/home.md).

![](../images/ui/explore/filter.png)

Vous pouvez également utiliser la barre de recherche pour affiner davantage les résultats. Lorsque vous recherchez un terme, les principaux éléments représentent des ressources dont les noms correspondent à la requête de recherche. Sous ces éléments, sous **[!UICONTROL Champs standard]**, toute ressource contenant des champs qui correspondent à la requête sera répertoriée. Cela vous permet de rechercher des ressources XDM en fonction du type de données qu&#39;elles contiennent, sans connaître au préalable le nom de la ressource.

![](../images/ui/explore/search.png)

Une fois que vous avez trouvé la ressource que vous souhaitez explorer, sélectionnez son nom dans la liste pour la vue de sa structure dans le canevas.

## Explorez une ressource XDM dans la trame {#explore}

Une fois que vous sélectionnez une ressource, sa structure s&#39;ouvre dans la trame.

![](../images/ui/explore/canvas.png)

Tous les champs de type objet contenant des sous-propriétés sont réduits par défaut lorsqu’ils apparaissent pour la première fois dans la trame. Pour afficher les sous-propriétés d’un champ, sélectionnez l’icône en regard de son nom.

![](../images/ui/explore/field-expand.png)

### Champs générés par le système {#system-fields}

Certains noms de champ sont précédés d’un trait de soulignement, tel que `_repo` et `_id`. Il s’agit d’espaces réservés pour les champs que le système génère et attribue automatiquement lorsque des données sont ingérées.

Par conséquent, la plupart de ces champs doivent être exclus de la structure de vos données lors de l’assimilation dans Platform. La principale exception à cette règle est le champ [`_{TENANT_ID}`](../api/getting-started.md#know-your-tenant_id), sous lequel tous les champs XDM créés sous votre organisation doivent être espacés de noms.

### Types des données {#data-types}

Pour chaque champ affiché dans la zone de travail, le type de données correspondant s’affiche en regard de son nom, indiquant d’un seul coup d’oeil le type de données attendu pour l’assimilation par le champ.

![](../images/ui/explore/data-types.png)

Tout type de données ajouté entre crochets (`[]`) représente un tableau de ce type de données particulier. Par exemple, un type de données **[!UICONTROL String]\[]** indique que le champ attend un tableau de valeurs de chaîne. Un type de données **[!UICONTROL Article de paiement]\[]** indique un tableau d&#39;objets conformes au type de données [!UICONTROL Article de paiement].

Si un champ de tableau est basé sur un type d&#39;objet, vous pouvez sélectionner son icône dans la trame pour afficher les attributs attendus pour chaque élément de tableau.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Propriétés de champ] {#field-properties}

Lorsque vous sélectionnez le nom d’un champ du canevas, le rail de droite se met à jour pour afficher des détails sur ce champ sous **[!UICONTROL Propriétés du champ]**. Cela peut inclure une description du cas d’utilisation prévu du champ, des valeurs par défaut, des modèles, des formats, que le champ soit obligatoire ou non, etc.

![](../images/ui/explore/field-properties.png)

Si le champ que vous inspectez est un champ enum, le rail droit affiche également les valeurs acceptables que le champ attend de recevoir.

![](../images/ui/explore/enum-field.png)

### Champs d&#39;identité {#identity}

Lors de l’inspection des schémas qui contiennent des champs d’identité, ces champs sont répertoriés dans le rail de gauche sous la classe ou le groupe de champs qui les fournit au schéma. Sélectionnez le nom du champ d’identité dans le rail de gauche pour afficher le champ dans la trame, quelle que soit la profondeur de son imbrication.

Les champs d’identité sont surlignés dans la trame avec une icône d’empreinte digitale (![Image d’icône d’empreinte digitale](../images/ui/explore/identity-symbol.png)). Si vous sélectionnez le nom du champ d&#39;identité, vous pouvez vue des informations supplémentaires telles que l&#39;[espace de nommage d&#39;identité](../../identity-service/namespaces.md) et indiquer si le champ est ou non l&#39;identité Principale du schéma.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Pour plus d&#39;informations sur les champs d&#39;identité et leur relation avec les services Plateforme en aval, consultez le guide sur la [définition des champs d&#39;identité](./fields/identity.md).

### Champs de relation {#relationship}

Si vous inspectez un schéma qui contient un champ de relation, le champ sera répertorié dans le rail de gauche sous **[!UICONTROL Relations]**. Sélectionnez le nom du champ de relation dans le rail de gauche pour afficher le champ dans la trame, quelle que soit la profondeur de son imbrication.

Les champs de relation sont également surlignés de manière unique dans la trame, en indiquant le nom du schéma de destination référencé par le champ. Si vous sélectionnez le nom du champ de relation, vous pouvez vue l&#39;espace de nommage d&#39;identité de l&#39;identité Principale du schéma de destination dans le rail de droite.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Pour plus d&#39;informations sur l&#39;utilisation des relations dans les schémas XDM, consultez le didacticiel [Création d&#39;une relation dans l&#39;interface utilisateur](../tutorials/create-schema-ui.md).

## Étapes suivantes

Ce document explique comment explorer les ressources XDM existantes dans l’interface utilisateur Experience Platform. Pour plus d&#39;informations sur les différentes fonctionnalités de l&#39;espace de travail [!UICONTROL Schémas] et de [!DNL Schema Editor], consultez le [[!UICONTROL Schémas] aperçu de l&#39;espace de travail](./overview.md).

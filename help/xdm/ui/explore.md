---
keywords: Experience Platform;accueil;rubriques populaires;ui;IU;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;explorer;classe;groupe de champs;type de données;schéma;
solution: Experience Platform
title: Exploration des ressources de schéma dans l’interface utilisateur
description: Découvrez comment explorer les schémas, classes, groupes de champs de schéma et types de données existants dans l’interface utilisateur de l’Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 7021725e011a1e1d95195c6c7318ecb5afe05ac6
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Exploration des ressources de schéma dans l’interface utilisateur

Dans Adobe Experience Platform, toutes les ressources de schéma du modèle de données d’expérience (XDM) sont stockées dans la variable [!DNL Schema Library], y compris les ressources standard fournies par Adobe et les ressources personnalisées définies par votre organisation. Dans l’interface utilisateur de l’Experience Platform, vous pouvez afficher la structure et les champs de tout schéma, classe, groupe de champs ou type de données existant dans la variable [!DNL Schema Library]. Cela s’avère particulièrement utile lors de la planification et de la préparation de l’ingestion de données, dans la mesure où l’interface utilisateur fournit des informations sur les types de données attendus et les cas d’utilisation de chaque champ fourni par ces ressources XDM.

Ce tutoriel décrit les étapes à suivre pour explorer les schémas, classes, groupes de champs et types de données existants dans l’interface utilisateur de l’Experience Platform.

## Recherche d’une ressource de schéma {#lookup}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. Le [!UICONTROL Schémas] workspace fournit une **[!UICONTROL Parcourir]** pour explorer tous les schémas de votre organisation, ainsi que d’autres onglets dédiés à l’exploration. **[!UICONTROL Classes]**, **[!UICONTROL Groupes de champs]**, et **[!UICONTROL Types de données]** respectivement.

![](../images/ui/explore/tabs.png)

Icône Filtrer (![Image de l’icône de filtre](../images/ui/explore/icon.png)) affiche des commandes dans le rail de gauche pour réduire les résultats répertoriés. Les contrôles affichés diffèrent selon le type de ressource répertoriée.

Par exemple, pour filtrer la liste afin de n’afficher que les types de données standard fournis par Adobe, sélectionnez **[!UICONTROL Type de données]** et **[!UICONTROL Adobe]** sous le **[!UICONTROL Type]** et **[!UICONTROL Propriétaire]** , respectivement.

Le **[!UICONTROL Inclus dans Profile]** activer/désactiver permet de filtrer les résultats afin d’afficher uniquement les ressources utilisées dans les schémas qui ont été activés pour une utilisation dans [Profil client en temps réel](../../profile/home.md).

![](../images/ui/explore/filter.png)

Lors de la mise en liste des ressources sur la variable **[!UICONTROL Classes]**, **[!UICONTROL Groupes de champs]** ou **[!UICONTROL Types de données]** onglets, vous pouvez sélectionner **[!UICONTROL Adobe]** pour afficher uniquement les ressources standard ou **[!UICONTROL Client]** pour afficher uniquement les ressources créées par votre organisation.

![](../images/ui/explore/filter-data-type.png)

Vous pouvez également utiliser la barre de recherche pour affiner davantage les résultats.

![](../images/ui/explore/search.png)

Les ressources affichées dans les résultats de recherche sont triées d’abord par correspondances de titre, puis par correspondances de description. En retour, plus le nombre de correspondances de mot dans l’une de ces catégories est élevé, plus la ressource apparaît dans la liste.

Une fois que vous avez trouvé la ressource à explorer, sélectionnez son nom dans la liste pour afficher sa structure dans la zone de travail.

## Exploration d’une ressource XDM dans la zone de travail {#explore}

Une fois que vous avez sélectionné une ressource, sa structure s’ouvre dans la zone de travail.

![](../images/ui/explore/canvas.png)

Tous les champs de type objet contenant des sous-propriétés sont réduits par défaut lorsqu’ils apparaissent pour la première fois dans la zone de travail. Pour afficher les sous-propriétés d’un champ, sélectionnez l’icône en regard de son nom.

![](../images/ui/explore/field-expand.png)

### Champs générés par le système {#system-fields}

Certains noms de champ sont précédés d’un trait de soulignement, tel que `_repo` et `_id`. Il s’agit d’espaces réservés pour les champs que le système génère et attribue automatiquement lors de l’ingestion des données.

Par conséquent, la plupart de ces champs doivent être exclus de la structure de vos données lors de l’ingestion dans Platform. La principale exception à cette règle est la suivante : [`_{TENANT_ID}` field](../api/getting-started.md#know-your-tenant_id), sous laquelle tous les champs XDM créés sous votre organisation doivent être des espaces de noms.

### Types de données {#data-types}

Pour chaque champ affiché dans la zone de travail, son type de données correspondant est affiché en regard de son nom, indiquant en un coup d’oeil le type de données attendu par le champ pour l’ingestion.

![](../images/ui/explore/data-types.png)

Tout type de données ajouté avec des crochets (`[]`) représente un tableau de ce type de données particulier. Par exemple, un type de données de **[!UICONTROL Chaîne]\[]** indique que le champ attend un tableau de valeurs de chaîne. Un type de données de **[!UICONTROL Élément de paiement]\[]** indique un tableau d’objets conforme à la variable [!UICONTROL Élément de paiement] type de données.

Si un champ de tableau est basé sur un type d’objet, vous pouvez sélectionner son icône dans la zone de travail afin d’afficher les attributs attendus pour chaque élément de tableau.

![](../images/ui/explore/array-type.png)

### [!UICONTROL Propriétés du champ] {#field-properties}

Lorsque vous sélectionnez le nom d’un champ dans la zone de travail, le rail de droite se met à jour pour afficher les détails sur ce champ sous **[!UICONTROL Propriétés du champ]**. Cela peut inclure une description du cas d’utilisation prévu du champ, des valeurs par défaut, des modèles, des formats, si le champ est obligatoire ou non, etc.

![](../images/ui/explore/field-properties.png)

Si le champ que vous inspectez est un champ d’énumération, le rail droit affiche également les valeurs acceptables que le champ s’attend à recevoir.

![](../images/ui/explore/enum-field.png)

### Champs d’identité {#identity}

Lors de l’inspection des schémas qui contiennent des champs d’identité, ces champs sont répertoriés dans le rail de gauche sous la classe ou le groupe de champs qui les fournit au schéma. Sélectionnez le nom du champ d’identité dans le rail de gauche pour afficher le champ dans la zone de travail, quelle que soit la profondeur d’imbrication.

Les champs d’identité sont mis en surbrillance dans la zone de travail avec une icône d’empreinte digitale (![Image d’empreinte digitale](../images/ui/explore/identity-symbol.png)). Si vous sélectionnez le nom du champ d’identité, vous pouvez afficher des informations supplémentaires, telles que la variable [namespace d’identité](../../identity-service/namespaces.md) et si le champ est ou non l’identité Principale du schéma.

![](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Consultez le guide sur la [définition des champs d’identité](./fields/identity.md) pour plus d’informations sur les champs d’identité et leur relation avec les services Platform en aval.

### Champs de relation {#relationship}

Si vous examinez un schéma qui contient un champ de relation, le champ sera répertorié dans le rail de gauche sous **[!UICONTROL Relations]**. Sélectionnez le nom du champ de relation dans le rail de gauche pour afficher le champ dans la zone de travail, quelle que soit la profondeur d’imbrication.

Les champs de relation sont également surlignés de manière unique dans la zone de travail, indiquant le nom du schéma de référence auquel le champ est lié. Si vous sélectionnez le nom du champ de relation, vous pouvez afficher l’espace de noms d’identité de l’identité Principale du schéma de référence dans le rail de droite.

![](../images/ui/explore/relationship-field.png)

>[!NOTE]
>
>Voir le tutoriel sur [création d’une relation dans l’interface utilisateur](../tutorials/relationship-ui.md) pour plus d’informations sur l’utilisation des relations dans les schémas XDM.

## Étapes suivantes

Ce document explique comment explorer les ressources XDM existantes dans l’interface utilisateur Experience Platform. Pour plus d’informations sur les différentes fonctionnalités de la variable [!UICONTROL Schémas] espace de travail et [!DNL Schema Editor], reportez-vous à la section [[!UICONTROL Schémas] présentation de workspace](./overview.md).

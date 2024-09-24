---
keywords: Experience Platform;accueil;rubriques populaires;ui;IU;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;explorer;classe;groupe de champs;type de données;schéma;
solution: Experience Platform
title: Exploration des ressources de schéma dans l’interface utilisateur
description: Découvrez comment explorer les schémas, classes, groupes de champs de schéma et types de données existants dans l’interface utilisateur de l’Experience Platform.
type: Tutorial
exl-id: b527b2a0-e688-4cfe-a176-282182f252f2
source-git-commit: 5f9fdc9eff4d8bba049c03058d24e80e9b89e953
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 0%

---

# Exploration des ressources de schéma dans l’interface utilisateur

Dans Adobe Experience Platform, toutes les ressources de schéma du modèle de données d’expérience (XDM) sont stockées dans le [!DNL Schema Library], y compris les ressources standard fournies par l’Adobe et les ressources personnalisées définies par votre organisation. Dans l’interface utilisateur de l’Experience Platform, vous pouvez afficher la structure et les champs de tout schéma, classe, groupe de champs ou type de données existant dans le [!DNL Schema Library]. Cela s’avère particulièrement utile lors de la planification et de la préparation de l’ingestion de données, dans la mesure où l’interface utilisateur fournit des informations sur les types de données attendus et les cas d’utilisation de chaque champ fourni par ces ressources XDM.

Ce tutoriel décrit les étapes à suivre pour explorer les schémas, classes, groupes de champs et types de données existants dans l’interface utilisateur de l’Experience Platform.

## Recherche d’une ressource de schéma {#lookup}

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche. L’espace de travail [!UICONTROL Schémas] fournit un onglet **[!UICONTROL Parcourir]** pour explorer tous les schémas de votre organisation, ainsi que des onglets dédiés supplémentaires pour explorer respectivement les **[!UICONTROL Classes]**, les **[!UICONTROL Groupes de champs]**, les **[!UICONTROL Types de données]** et les **[!UICONTROL Relations]**.

![Espace de travail des schémas avec plusieurs onglets surlignés.](../images/ui/explore/tabs.png)

L’icône de filtre (![Icône de filtre ](/help/images/icons/filter.png)) affiche les commandes dans le rail de gauche pour réduire les résultats répertoriés. Les filtres de ressources sont disponibles pour les schémas et les relations sur les onglets **[!UICONTROL Parcourir]** et **[!UICONTROL Relations]** respectivement.

Dans l’onglet [!UICONTROL Parcourir] de l’espace de travail [!UICONTROL Schémas], vous pouvez filtrer l’inventaire de vos schémas. Utilisez le bouton d’activation/désactivation **[!UICONTROL Inclus dans le profil]** pour n’afficher que les schémas qui ont été activés pour une utilisation dans [Real-Time Customer Profile](../../profile/home.md). Utilisez le bouton d’activation/désactivation **[!UICONTROL Afficher les schémas ad hoc]** pour filtrer la liste des schémas créés avec des espaces de noms de champs à utiliser uniquement par un seul jeu de données.

![L’onglet [!UICONTROL Parcourir] de l’espace de travail [!UICONTROL Schémas] avec le panneau des filtres en surbrillance.](../images/ui/explore/filters.png)

Sur l’onglet [!UICONTROL Relationship] de l’espace de travail [!UICONTROL Schemas] , vous pouvez filtrer la liste des relations selon quatre critères. Les filtres incluent [!UICONTROL Schéma Source], [!UICONTROL Schéma de destination], [!UICONTROL Classe Source] et la [!UICONTROL Classe de destination]. Le tableau ci-dessous fournit une description des filtres.

| Filtre | Description |
|-----------------------------------|------------|
| [!UICONTROL Schéma Source] | Pour afficher toutes les relations où le schéma sélectionné est le point de départ ou la &quot;source&quot;, sélectionnez un schéma dans le menu déroulant [!UICONTROL Schéma Source]. |
| [!UICONTROL Schéma de destination] | Pour afficher toutes les relations où le schéma sélectionné est la cible ou la &quot;destination&quot;, sélectionnez un schéma dans le menu déroulant [!UICONTROL Schéma destination]. |
| [!UICONTROL Classe Source] | Pour filtrer les relations en fonction de la classe du schéma d’initialisation, sélectionnez une classe dans le menu déroulant [!UICONTROL Classe Source] . |
| [!UICONTROL Classe de destination] | Pour afficher les relations qui se terminent par des schémas d’une classe spécifique, sélectionnez une classe dans le menu déroulant [!UICONTROL Classe de destination] . |

{style="table-layout:auto"}

![L&#39;onglet Relations avec la section Filtres mise en surbrillance.](../images/ui/explore/relationships-filter.png)

Vous pouvez également utiliser la barre de recherche pour affiner davantage les résultats.

![Onglet Parcourir de l’espace de travail des schémas avec le champ de recherche en surbrillance.](../images/ui/explore/search.png)

Les ressources affichées dans les résultats de recherche sont triées d’abord par correspondances de titre, puis par correspondances de description. En retour, plus le nombre de correspondances de mot dans l’une de ces catégories est élevé, plus la ressource apparaît dans la liste.

Une fois que vous avez trouvé la ressource que vous souhaitez explorer, sélectionnez son nom dans la liste pour afficher sa structure dans la zone de travail.

## Exploration d’une ressource XDM dans la zone de travail {#explore}

Lorsque vous sélectionnez une ressource, sa structure s’ouvre dans la zone de travail.

![Le canevas de l’espace de travail Datatype affichant le type de données Commerce.](../images/ui/explore/canvas.png)

Tous les champs de type objet contenant des sous-propriétés sont réduits par défaut lorsqu’ils apparaissent pour la première fois dans la zone de travail. Pour afficher les sous-propriétés d’un champ, sélectionnez l’icône en regard de son nom.

![ Canevas de l’espace de travail Datatype avec champs étendus et sous-propriétés surlignées.](../images/ui/explore/field-expand.png)

### Indicateur de classe standard et de groupe de champs {#standard-class-and-field-group-indicator}

Dans l’éditeur de schémas, les classes standard (générées par un Adobe) et les groupes de champs sont indiqués par l’icône de cadenas (![Icône de cadenas.](/help/images/icons/lock-closed.png). Le cadenas s’affiche dans le rail de gauche en regard du nom de la classe ou du groupe de champs, ainsi qu’en regard de tout champ du diagramme de schéma qui fait partie d’une ressource générée par le système.

![L’éditeur de schéma avec l’icône de cadenas mise en surbrillance](../images/ui/explore/schema-editor-padlock-icon.png)

Pour plus d’informations, reportez-vous à la documentation [Ajouter des champs personnalisés aux groupes de champs standard](./resources/schemas.md) . Vous ne pouvez pas modifier une classe standard.

### Champs générés par le système {#system-fields}

Certains noms de champ sont précédés d’un trait de soulignement, comme `_repo` et `_id`. Il s’agit d’espaces réservés pour les champs que le système génère et attribue automatiquement lors de l’ingestion des données.

Par conséquent, la plupart de ces champs doivent être exclus de la structure de vos données lors de l’ingestion dans Platform. L’exception principale à cette règle est le [`_{TENANT_ID}` champ](../api/getting-started.md#know-your-tenant_id), sous lequel tous les champs XDM créés sous votre organisation doivent se trouver dans l’espace de noms.

### Types de données {#data-types}

Pour chaque champ affiché dans la zone de travail, son type de données correspondant est affiché en regard de son nom, indiquant en un coup d’oeil le type de données attendu par le champ pour l’ingestion.

![Type de données Adresse postale affiché sur la zone de travail avec les types de données associés mis en surbrillance.](../images/ui/explore/data-types.png)

Tout type de données ajouté avec des crochets (`[]`) représente un tableau de ce type de données particulier. Par exemple, un type de données **[!UICONTROL String]\[]** indique que le champ attend un tableau de valeurs de chaîne. Un type de données **[!UICONTROL Article de paiement]\[]** indique un tableau d’objets conformes au type de données [!UICONTROL Article de paiement].

Si un champ de tableau est basé sur un type d’objet, vous pouvez sélectionner son icône dans la zone de travail afin d’afficher les attributs attendus pour chaque élément de tableau.

![Un objet dans la zone de travail avec un champ de tableau en surbrillance et les attributs attendus pour chaque élément de tableau affichés.](../images/ui/explore/array-type.png)

### [!UICONTROL Propriétés du champ] {#field-properties}

Lorsque vous sélectionnez le nom d’un champ dans la zone de travail, le rail de droite se met à jour pour afficher les détails sur ce champ sous **[!UICONTROL Propriétés du champ]**. Cela peut inclure une description du cas d’utilisation prévu du champ, des valeurs par défaut, des modèles, des formats, si le champ est obligatoire ou non, etc.

![Champ sélectionné dans le type de données Commerce avec les propriétés de champ mises en surbrillance.](../images/ui/explore/field-properties.png)

Si le champ que vous inspectez est un champ d’énumération, le rail droit affiche également les valeurs acceptables que le champ s’attend à recevoir.

![ L’éditeur de schémas avec un champ sélectionné, des valeurs d’énumération et des noms d’affichage surlignés dans le rail des propriétés de champ.](../images/ui/explore/enum-field.png)

### Champs d’identité {#identity}

Lors de l’inspection des schémas qui contiennent des champs d’identité, ces champs sont répertoriés dans le rail de gauche sous la classe ou le groupe de champs qui les fournit au schéma. Sélectionnez le nom du champ d’identité dans le rail de gauche pour afficher le champ dans la zone de travail, quelle que soit la profondeur d’imbrication.

Les champs d’identité sont mis en surbrillance dans la zone de travail avec une icône d’empreinte digitale (![Icône d’empreinte digitale ](/help/images/icons/identity-service.png)). Si vous sélectionnez le nom du champ d’identité, vous pouvez afficher des informations supplémentaires telles que l’ [espace de noms d’identité](../../identity-service/features/namespaces.md) et déterminer si le champ est l’identité principale du schéma.

![L’éditeur de schéma avec l’identité du schéma mise en surbrillance dans le rail de gauche, le champ mis en surbrillance dans le schéma et l’espace de noms d’identité mis en surbrillance dans les propriétés du champ.](../images/ui/explore/identity-field.png)

>[!NOTE]
>
>Pour plus d’informations sur les champs d’identité et leur relation avec les services Platform en aval, consultez le guide sur la [définition des champs d’identité](./fields/identity.md) .

### Champs de relation {#relationship}

Si vous examinez un schéma qui contient un champ de relation, le champ sera répertorié dans le rail de gauche sous **[!UICONTROL Relationships]**. Sélectionnez le nom du champ de relation dans le rail de gauche pour afficher le champ dans la zone de travail, quelle que soit la profondeur d’imbrication. Les champs de relation sont également surlignés de manière unique dans la zone de travail, indiquant le nom du schéma de référence auquel le champ est lié. Pour les organisations dotées de fonctionnalités B2B, des noms de relation personnalisés peuvent être écrits et s’afficheront sur la zone de travail dans ces cas.

![L’éditeur de schéma avec le champ de relation et la relation Modifier mise en surbrillance.](../images/ui/explore/relationship-field.png)

Pour afficher l’espace de noms d’identité de l’identité principale du schéma de référence, sélectionnez le champ de relation, puis **[!UICONTROL Modifier la relation]** dans la barre latérale [!UICONTROL Propriétés du champ]. Les paramètres de la relation sont affichés dans la boîte de dialogue [!UICONTROL Modifier la relation] qui s’affiche.

![La boîte de dialogue Modifier la relation avec les paramètres de relation affichés.](../images/ui/explore/edit-relationship-dialog.png)

Pour plus d’informations sur l’utilisation des relations dans les schémas XDM, consultez le tutoriel sur la [création d’une relation dans l’interface utilisateur](../tutorials/relationship-ui.md) .

## Étapes suivantes

Ce document explique comment explorer les ressources XDM existantes dans l’interface utilisateur Experience Platform. Pour plus d’informations sur les différentes fonctionnalités de l’espace de travail [!UICONTROL Schemas] et [!DNL Schema Editor], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail ](./overview.md).

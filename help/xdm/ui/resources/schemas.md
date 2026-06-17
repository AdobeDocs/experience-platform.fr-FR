---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;interface utilisateur;espace de travail;schéma;schémas;
solution: Experience Platform
title: Création et modification de schémas dans l’interface utilisateur
description: Découvrez les bases de la création et de la modification de schémas dans l’interface utilisateur d’Experience Platform.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
TQID: https://experienceleague.adobe.com/yevQxPbQDMaftqQBj5oeLlpGvoINcaQNnLe1eHUgTKk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
  - id: daec7ead-f475-492a-a3b3-02ae08565d6f
subfeature_v2:
  - id: b572b7ff-a413-4173-b2b4-d7d3874f1b9b
  - id: cdd3e38b-fec2-4f39-8b10-83ddaab1ac16
  - id: ee602049-8a18-43df-9299-a689a025a371
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 96edf5301f1fa53cf875c5c791d67bd96e94ad6b
workflow-type: tm+mt
source-wordcount: 6183
ht-degree: 3%

---

# Créer et modifier les schémas dans l’interface utilisateur {#create-edit-schemas-in-ui}

Utilisez l’interface utilisateur de Adobe Experience Platform pour créer, modifier et gérer des schémas de modèle de données d’expérience (XDM) pour votre organisation. Ce guide vous explique comment créer des schémas standard et relationnels, personnaliser les structures des schémas, gérer les schémas à partir de l’espace de travail [!UICONTROL Parcourir] et préparer les schémas en vue d’une utilisation en production.

>[!IMPORTANT]
>
>Les schémas XDM sont extrêmement personnalisables. Par conséquent, les étapes de création d’un schéma peuvent varier en fonction du type de données que vous souhaitez que le schéma capture. Par conséquent, ce document ne couvre que les interactions de base que vous pouvez effectuer avec les schémas dans l’interface utilisateur et exclut les étapes associées, telles que la personnalisation des classes, des groupes de champs de schéma, des types de données et des champs.
>
>Pour une visite complète du processus de création de schéma, suivez le [tutoriel sur la création de schémas](../../tutorials/create-schema-ui.md) afin de créer un exemple de schéma complet et de vous familiariser avec les nombreuses fonctionnalités de l’[!DNL Schema Editor].

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une introduction au rôle de XDM dans l’écosystème Experience Platform et aux [principes de base de la composition des schémas](../../schema/composition.md) pour une présentation de la construction des schémas.

## Créer un schéma {#create}

Dans l’espace de travail [!UICONTROL Schémas], sélectionnez **[!UICONTROL Créer un schéma]** dans le coin supérieur droit. Le menu déroulant « Sélectionner le type de schéma » s’affiche avec des options pour les schémas [!UICONTROL Standard] ou [!UICONTROL Relationnels].

![L’espace de travail Schémas avec l’option [!UICONTROL Créer un schéma] mise en surbrillance et la liste déroulante [!UICONTROL Sélectionner le type de schéma] affichée.](../../images/ui/resources/schemas/create-schema.png)

## Créer un schéma relationnel {#create-relational-schema}

>[!AVAILABILITY]
>
>Les schémas Data Mirror et relationnels sont disponibles pour les détenteurs de licence Adobe Journey Optimizer **Campagnes orchestrées**. Ils sont également disponibles en tant que **version limitée** pour les utilisateurs de Customer Journey Analytics, selon votre licence et l’activation des fonctionnalités. Contactez votre représentant Adobe pour obtenir l’accès.

Sélectionnez **[!UICONTROL Relationnel]** pour définir des schémas de style relationnel structurés avec un contrôle précis des enregistrements. Les schémas relationnels prennent en charge l’application des clés primaires, le contrôle de version au niveau des enregistrements et les relations au niveau du schéma par le biais de clés primaires et étrangères. Ils sont également optimisés pour l’ingestion incrémentielle à l’aide de la capture de données de modification et prennent en charge plusieurs modèles de données utilisés dans les implémentations Campaign Orchestration, Data Distiller et B2B.

Pour en savoir plus, consultez la présentation de [&#128279;](../../data-mirror/overview.md) ou [Schéma relationnel](../../schema/relational.md).

### Créer manuellement {#create-manually}

>[!AVAILABILITY]
>
>Le chargement de fichier DDL est uniquement disponible pour les détenteurs de licence Adobe Journey Optimizer Orchestrated Campaign. L’interface utilisateur peut avoir un aspect différent.

La boîte de dialogue **[!UICONTROL Créer un schéma relationnel]** s’affiche. Vous pouvez choisir entre **[!UICONTROL Créer manuellement]** ou [**[!UICONTROL Télécharger le fichier DDL]**](#upload-ddl-file) pour définir la structure du schéma.

Dans la boîte de dialogue **[!UICONTROL Créer un schéma relationnel]**, sélectionnez **[!UICONTROL Créer manuellement]** puis sélectionnez **[!UICONTROL Suivant]**.

![La boîte de dialogue [!UICONTROL Créer un schéma relationnel] avec [!UICONTROL Créer manuellement] sélectionné et [!UICONTROL Suivant] mis en surbrillance.](../../images/ui/resources/schemas/relational-dialog.png)

La page **[!UICONTROL Détails du schéma relationnel]** s’affiche. Saisissez un nom d’affichage de schéma et une description facultative, puis sélectionnez **[!UICONTROL Terminer]** pour créer le schéma.

![Page [!UICONTROL Détails du schéma relationnel] avec [!UICONTROL Nom d’affichage du schéma], [!UICONTROL Description] et [!UICONTROL Terminer] en surbrillance.](../../images/ui/resources/schemas/relational-details.png)

L’éditeur de schémas s’ouvre avec une zone de travail vide pour définir la structure du schéma. Vous pouvez ajouter des champs comme vous le faites habituellement.

#### Ajout d’un champ d’identifiant de version {#add-version-identifier}

Pour activer le suivi de version et prendre en charge la capture de données de modification, vous devez désigner un champ d’identifiant de version dans votre schéma. Dans l’éditeur de schémas, sélectionnez le signe plus (![A icône plus.](/help/images/icons/plus.png)) à côté du nom du schéma pour ajouter un nouveau champ.

Saisissez un nom de champ tel que `updateSequence` et choisissez un type de données **[!UICONTROL DateHeure]** ou **[!UICONTROL Nombre]**.

Dans le rail de droite, cochez la case **[!UICONTROL Identifiant de version]**, puis sélectionnez **[!UICONTROL Appliquer]** pour confirmer le champ.

![L’éditeur de schémas avec un champ DateTime nommé `updateSequence` ajouté et la case à cocher [!UICONTROL Identifiant de version] sélectionnée.](../../images/ui/resources/schemas/add-version-identifier.png)

>[!IMPORTANT]
>
>Un schéma relationnel doit inclure un champ d’identifiant de version pour prendre en charge les mises à jour au niveau des enregistrements et modifier l’ingestion de la capture de données.

Pour définir des relations, sélectionnez **[!UICONTROL Ajouter une relation]** dans l’éditeur de schémas pour créer des relations clé primaire/étrangère au niveau du schéma. Pour plus d’informations, consultez le tutoriel sur [l’ajout de relations au niveau du schéma](../../tutorials/relationship-ui.md#relationship-field).

Ensuite, passez à [définir des clés primaires](../fields/identity.md#define-a-identity-field) et [ajouter des champs supplémentaires](#add-field-groups) si nécessaire. Pour obtenir des instructions sur la manière d’activer la capture de données de modification dans les sources Experience Platform, consultez le [guide d’ingestion de capture de données de modification](../../../sources/tutorials/api/change-data-capture.md).

>[!NOTE]
>
>Une fois enregistré, le champ [!UICONTROL Type] de la barre latérale [!UICONTROL Propriétés du schéma] indique qu’il s’agit d’un schéma [!UICONTROL Relationnel]. Cela est également indiqué dans la barre latérale des détails dans la vue d’inventaire des schémas.
>![&#x200B; Zone de travail de l’éditeur de schémas présentant une structure de schéma relationnel vide avec le type [!UICONTROL Relationnel] indiqué dans la barre latérale [!UICONTROL Propriétés du schéma]. &#x200B;](../../images/ui/resources/schemas/relational-empty-canvas.png)

### Charger un fichier DDL {#upload-ddl-file}

>[!AVAILABILITY]
>
>Le chargement de fichier DDL est uniquement disponible pour les détenteurs de licence Adobe Journey Optimizer Orchestrated Campaign.

Utilisez ce workflow pour définir le schéma en chargeant un fichier DDL. Dans la boîte de dialogue **[!UICONTROL Créer un schéma relationnel]**, sélectionnez **[!UICONTROL Charger un fichier DDL]**, puis faites glisser un fichier DDL local depuis votre système ou sélectionnez **[!UICONTROL Choisir des fichiers]**. Experience Platform valide le schéma et affiche une coche verte si le chargement du fichier réussit. Sélectionnez **[!UICONTROL Suivant]** pour confirmer le chargement.

![La boîte de dialogue [!UICONTROL Créer un schéma relationnel] avec l’option [!UICONTROL Charger le fichier DDL] sélectionnée et la zone de chargement du fichier affichée, y compris le bouton [!UICONTROL Choisir les fichiers] et la zone de glisser-déposer.](../../images/ui/resources/schemas/upload-ddl-file.png)

La boîte de dialogue [!UICONTROL Sélectionner les entités et les champs à importer] s’affiche et vous permet de prévisualiser le schéma. Vérifiez la structure du schéma et utilisez les boutons radio et les cases à cocher pour vous assurer que chaque entité dispose d’une clé primaire et d’un identifiant de version spécifiés.

>[!IMPORTANT]
>
>La structure de la table doit contenir une **clé primaire** et un **identifiant de version**, tel qu&#39;un champ `updateSequence` de type datetime ou number.
>
>Pour l’ingestion de capture de données de modification, une colonne spéciale nommée `_change_request_type` de type Chaîne est également nécessaire pour activer le traitement incrémentiel. Ce champ indique le type de modification des données (par exemple, `u` (upsert) ou `d` (delete)).

Bien que cela soit nécessaire lors de l’ingestion, les colonnes de contrôle telles que `_change_request_type` ne sont pas stockées dans le schéma et n’apparaissent pas dans la structure de schéma finale. Si tout semble correct, sélectionnez **[!UICONTROL Terminé]** pour créer le schéma.

>[!NOTE]
>
>La taille de fichier maximale prise en charge pour un chargement DDL est de 10 Mo.

![La boîte de dialogue [!UICONTROL Sélectionner les entités et les champs à importer] affiche les champs importés et met en surbrillance [!UICONTROL Terminé].](../../images/ui/resources/schemas/entities-and-files-to-import.png)


Le schéma s’ouvre dans l’éditeur de schémas, où vous pouvez ajuster la structure avant d’enregistrer.

Ensuite, passez à [ajouter des champs supplémentaires](#add-field-groups) et [ajouter des relations supplémentaires au niveau du schéma](../../tutorials/relationship-ui.md#relationship-field) si nécessaire.

Pour obtenir des instructions sur la manière d’activer la capture de données de modification dans les sources Experience Platform, consultez le [guide d’ingestion de capture de données de modification](../../../sources/tutorials/api/change-data-capture.md).

### Création d’un schéma standard {#create-standard-schema}

Sélectionnez **[!UICONTROL Standard]** dans le menu Type de schéma . La boîte de dialogue [!UICONTROL Créer un schéma] s’affiche. Dans cette boîte de dialogue, choisissez un workflow de création de schéma. Vous pouvez créer manuellement un schéma en ajoutant des champs et des groupes de champs, ou charger un fichier CSV pour générer automatiquement un schéma.

![&#x200B; La boîte de dialogue [!UICONTROL Créer un schéma] avec les options du workflow de création de schéma mises en surbrillance.](../../images/ui/resources/schemas/create-a-schema-dialog.png)

### [!BADGE Beta &#x200B;]{type=Informative} création manuelle ou assistée par machine learning de schéma {#manual-or-assisted}

Pour découvrir comment utiliser un algorithme ML afin de recommander une structure de schéma basée sur un fichier csv, consultez le guide de création de schéma assisté par machine learning [machine learning](../ml-assisted-schema-creation.md). Ce guide de l’interface utilisateur se concentre sur le workflow de création manuelle .

### Création manuelle de schéma {#manual-creation}

Le workflow [!UICONTROL Créer un schéma] s’affiche. Vous pouvez choisir une classe de base pour le schéma en sélectionnant **[!UICONTROL Profil individuel]**, **[!UICONTROL Événement d’expérience]** ou **[!UICONTROL Autre]**, suivi de **[!UICONTROL Suivant]** pour confirmer votre choix. Consultez la documentation [[!UICONTROL Profil individuel XDM]](../../classes/individual-profile.md) et [[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md) pour plus d’informations sur ces classes.

![Le workflow [!UICONTROL Créer un schéma] présentant les trois options de classe de base avec [!UICONTROL Suivant] en surbrillance.](../../images/ui/resources/schemas/schema-class-options.png)

Lorsque vous choisissez **[!UICONTROL Autre]**, la liste des classes disponibles s’affiche. À partir de là, vous pouvez parcourir et filtrer les classes préexistantes.

![Le workflow [!UICONTROL Créer un schéma] avec l’option [!UICONTROL Autre] sélectionnée et la liste des classes disponibles s’affiche.](../../images/ui/resources/schemas/other-schema-details.png)

Sélectionnez un bouton radio pour filtrer les classes selon qu’il s’agit de classes personnalisées ou standard. Vous pouvez également filtrer les résultats disponibles en fonction de leur secteur d’activité ou rechercher une classe spécifique à l’aide du champ de recherche.

![Workflow [!UICONTROL Créer un schéma] avec la barre de recherche [!UICONTROL Personnalisé] et [!UICONTROL Industries] mise en surbrillance.](../../images/ui/resources/schemas/filter-and-search.png)

Pour vous aider à choisir la classe appropriée, il existe des icônes d’informations et de prévisualisation pour chaque classe. L’icône d’informations (![Icône d’informations.](/help/images/icons/info.png)) ouvre une boîte de dialogue qui fournit une description de la classe et du secteur auquel elle est associée.

![Le workflow [!UICONTROL Créer un schéma] avec une info-bulle de classe s’ouvre avec la description de la classe et le secteur associé.](../../images/ui/resources/schemas/class-info.png)

L’icône d’aperçu (![Icône d’aperçu.](/help/images/icons/preview.png)) ouvre une boîte de dialogue de prévisualisation pour la classe qui contient un diagramme de schéma et ses propriétés.

![Boîte de dialogue de prévisualisation de la classe présentant le diagramme de schéma et les propriétés de la classe sélectionnée.](../../images/ui/resources/schemas/class-preview.png)

Sélectionnez une ligne pour choisir une classe, puis sélectionnez **[!UICONTROL Suivant]** pour confirmer votre choix.

![Workflow [!UICONTROL Créer un schéma] avec une classe sélectionnée dans le tableau des classes disponibles et l’option [!UICONTROL Suivant] mise en surbrillance.](../../images/ui/resources/schemas/select-class.png)

Après avoir sélectionné une classe, la section [!UICONTROL Nom et révision] s’affiche. Dans cette section, vous indiquez un nom et une description pour identifier votre schéma. &#x200B;La structure de base du schéma (fournie par la classe ) s’affiche dans la zone de travail pour que vous puissiez consulter et vérifier la structure de classe et de schéma sélectionnée.

Saisissez un [!UICONTROL nom d’affichage du schéma] convivial dans le champ de texte. Saisissez ensuite une description appropriée pour vous aider à identifier votre schéma. Une fois que vous avez révisé votre structure de schéma et que vos paramètres vous conviennent, sélectionnez **[!UICONTROL Terminer]** pour créer votre schéma.

![La section [!UICONTROL Nom et révision] du workflow [!UICONTROL Créer un schéma] avec le [!UICONTROL Nom d’affichage du schéma], [!UICONTROL Description] et [!UICONTROL Terminer] en surbrillance.](../../images/ui/resources/schemas/name-and-review.png)

L’éditeur de schémas s’affiche, avec la structure du schéma affichée dans la zone de travail. Si vous le souhaitez, vous pouvez maintenant commencer [à ajouter des champs à la classe](../../ui/resources/classes.md#add-fields).

![&#x200B; Éditeur de schémas affichant la structure de base d’un schéma nouvellement créé dans la zone de travail.](../../images/ui/resources/schemas/edit.png)

## Modification d’un schéma existant {#edit}

>[!NOTE]
>
>Une fois qu’un schéma a été enregistré et utilisé dans l’ingestion de données, seules des modifications supplémentaires peuvent lui être apportées. Pour plus d’informations, consultez la section [règles d’évolution des schémas](../../schema/composition.md#evolution) .

Pour modifier un schéma existant, sélectionnez l’onglet **[!UICONTROL Parcourir]**, puis sélectionnez le nom du schéma à modifier. Vous pouvez également utiliser la barre de recherche pour affiner la liste des options disponibles.

![L’onglet [!UICONTROL Parcourir] de l’espace de travail Schémas affiche en surbrillance le nom du schéma à sélectionner et à modifier.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Vous pouvez utiliser les fonctionnalités de recherche et de filtrage de l’espace de travail pour faciliter la recherche du schéma. Pour plus d’informations, consultez le guide sur l’[exploration des ressources XDM](../explore.md).

Une fois que vous avez sélectionné un schéma, la [!DNL Schema Editor] s’affiche avec la structure du schéma affichée dans la zone de travail. Vous pouvez désormais personnaliser votre schéma à l’aide des outils et options décrits dans la section suivante.

## Personnalisation d’un schéma {#customize-schema}

Une fois qu’un schéma est ouvert dans l’éditeur de schémas, vous pouvez personnaliser sa structure, ses champs et ses propriétés d’affichage. Cette section couvre les principales options de personnalisation disponibles pour adapter les schémas à vos besoins spécifiques.

Utilisez les liens suivants pour accéder directement aux tâches de personnalisation clés de cette section :

- [Basculement du nom d’affichage](#display-name-toggle)
- [Ajout de groupes de champs à un schéma](#add-field-groups)
- [Modifier les noms d’affichage des champs de schéma](#display-names)

### Basculement du nom d’affichage {#display-name-toggle}

Pour votre commodité, l’éditeur de schémas propose un bouton bascule pour basculer entre les noms de champ d’origine et les noms d’affichage plus lisibles. Cette flexibilité permet d’améliorer la visibilité des champs et la modification de vos schémas. Le bouton (bascule) se trouve en haut à droite de la vue de l’éditeur de schémas.

>[!NOTE]
>
>Le passage des noms de champ aux noms d’affichage est purement cosmétique et ne modifie aucune ressource en aval.

![Éditeur de schémas avec [!UICONTROL Afficher les noms d’affichage des champs] mis en surbrillance.](../../images/ui/resources/schemas/display-name-toggle.png)

Les noms d’affichage des groupes de champs standard sont générés par le système, mais peuvent être personnalisés, comme décrit dans la section [noms d’affichage](#display-names). Les noms d’affichage sont reflétés dans plusieurs vues de l’interface utilisateur, y compris les aperçus de mappages et de jeux de données. Le paramètre par défaut est désactivé et affiche les noms de champ selon leurs valeurs d’origine.

### Ajout de groupes de champs à un schéma {#add-field-groups}

>[!NOTE]
>
>Cette section explique comment ajouter des groupes de champs existants à un schéma. Si vous souhaitez créer un groupe de champs personnalisés, consultez le guide sur la [création et modification de groupes de champs](./field-groups.md#create) à la place.

Une fois que vous avez ouvert un schéma dans le [!DNL Schema Editor], vous pouvez y ajouter des champs à l’aide de groupes de champs. Pour commencer, sélectionnez **[!UICONTROL Ajouter]** en regard de **[!UICONTROL Groupes de champs]** dans le rail de gauche.

![Éditeur de schémas avec le bouton [!UICONTROL Ajouter] en surbrillance dans la section [!UICONTROL Groupes de champs] du rail de gauche.](../../images/ui/resources/schemas/add-field-group-button.png)

Une boîte de dialogue s’affiche, affichant une liste de groupes de champs que vous pouvez sélectionner pour le schéma. Comme les groupes de champs ne sont compatibles qu’avec une seule classe, seuls les groupes de champs associés à la classe sélectionnée du schéma seront répertoriés. Par défaut, les groupes de champs répertoriés sont triés en fonction de leur popularité d’utilisation au sein de votre organisation.

La boîte de dialogue [!UICONTROL &#x200B; Ajouter des groupes de champs] affiche les groupes de champs disponibles triés selon la colonne [!UICONTROL Popularité].![&#128279;](../../images/ui/resources/schemas/field-group-popularity.png)

Si vous connaissez l’activité générale ou le domaine fonctionnel des champs que vous souhaitez ajouter, sélectionnez une ou plusieurs catégories sectorielles verticales dans le rail de gauche pour filtrer la liste affichée des groupes de champs.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] avec les filtres [!UICONTROL Secteur] sélectionnés dans le rail de gauche et la colonne [!UICONTROL Secteur] mise en surbrillance.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Pour plus d’informations sur les bonnes pratiques de modélisation des données spécifiques au secteur dans XDM, consultez la documentation sur les [modèles de données du secteur](../../schema/industries/overview.md).

Vous pouvez également utiliser la barre de recherche pour localiser le groupe de champs de votre choix. Les groupes de champs dont le nom correspond à la requête apparaissent en haut de la liste. Sous **[!UICONTROL Champs standard]**, des groupes de champs contenant des champs qui décrivent les attributs de données souhaités s’affichent.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] avec la barre de recherche active et [!UICONTROL Champs standard] les résultats s’affichent.](../../images/ui/resources/schemas/field-group-search.png)

Cochez la case en regard du nom du groupe de champs que vous souhaitez ajouter au schéma. Vous pouvez sélectionner plusieurs groupes de champs dans la liste, chaque groupe de champs sélectionné apparaissant dans le rail de droite.

La boîte de dialogue [!UICONTROL &#x200B; Ajouter des groupes de champs] avec les groupes de champs sélectionnés à l’aide de cases à cocher et les groupes sélectionnés affichés dans le rail de droite![&#128279;](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Pour n’importe quel groupe de champs répertorié, vous pouvez pointer ou placer le focus sur l’icône d’information (![icône d’information](/help/images/icons/info.png)) pour afficher une brève description du type de données capturées par le groupe de champs. Vous pouvez également sélectionner l’icône d’aperçu (![icône d’aperçu](/help/images/icons/preview.png)) pour afficher la structure des champs fournis par le groupe de champs avant de décider de l’ajouter au schéma.

Une fois que vous avez choisi vos groupes de champs, sélectionnez **[!UICONTROL Ajouter des groupes de champs]** pour les ajouter au schéma.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] avec les groupes de champs sélectionnés et [!UICONTROL Ajouter des groupes de champs] mise en surbrillance.](../../images/ui/resources/schemas/add-field-group-finish.png)

La [!DNL Schema Editor] réapparaît avec les champs fournis par le groupe de champs représentés dans la zone de travail.

![&#x200B; Éditeur de schémas affichant les champs du groupe de champs nouvellement ajouté représentés dans la zone de travail.](../../images/ui/resources/schemas/field-groups-added.png)

>[!NOTE]
>
>Dans l’éditeur de schémas, les classes et les groupes de champs standard (générés par Adobe) sont indiqués par l’icône de cadenas ![une icône de cadenas.](/help/images/icons/lock-closed.png). Le cadenas s’affiche dans le rail de gauche à côté du nom de la classe ou du groupe de champs, ainsi qu’à côté de tout champ du diagramme de schéma qui fait partie d’une ressource générée par le système.
>
>![Éditeur de schémas avec l’icône de cadenas mise en surbrillance en regard d’un nom de groupe de champs standard dans le rail de gauche.](../../images/ui/explore/schema-editor-padlock-icon.png)

Après avoir ajouté un groupe de champs à un schéma, vous pouvez éventuellement [supprimer des champs existants](#remove-fields) ou [ajouter de nouveaux champs personnalisés](#add-fields) à ces groupes, en fonction de vos besoins.

#### Supprimer les champs ajoutés des groupes de champs {#remove-fields}

Une fois que vous avez ajouté un groupe de champs à un schéma, vous pouvez supprimer globalement des champs du groupe de champs ou les masquer localement du schéma actuel. Il est essentiel de comprendre la différence entre ces actions pour éviter toute modification involontaire du schéma.

>[!IMPORTANT]
>
>Sélectionner **[!UICONTROL Supprimer]** supprime le champ du groupe de champs lui-même, ce qui affecte *tous* les schémas qui utilisent ce groupe de champs.
>N’utilisez cette option que si vous souhaitez **supprimer le champ de chaque schéma qui inclut le groupe de champs**.

Pour supprimer un champ du groupe de champs, sélectionnez-le dans la zone de travail et sélectionnez **[!UICONTROL Supprimer]** dans le rail de droite. Cet exemple montre le champ `taxId` du groupe **[!UICONTROL Détails démographiques]**.

![L’éditeur de schémas avec un champ sélectionné dans la zone de travail et [!UICONTROL Supprimer] mis en surbrillance dans le rail de droite.](../../images/ui/resources/schemas/remove-single-field.png)

Pour masquer plusieurs champs d’un schéma sans les supprimer du groupe de champs lui-même, utilisez l’option **[!UICONTROL Gérer les champs associés]**. Sélectionnez un champ dans le groupe de la zone de travail, puis sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

![L’éditeur de schémas avec un champ de groupe de champs sélectionné dans la zone de travail et [!UICONTROL Gérer les champs associés] mis en surbrillance dans le rail de droite.](../../images/ui/resources/schemas/manage-related-fields.png)

Une boîte de dialogue s’affiche, affichant la structure du groupe de champs. Utilisez les cases à cocher pour sélectionner ou désélectionner les champs à inclure.

![La boîte de dialogue [!UICONTROL Gérer les champs associés] avec les champs sélectionnés et [!UICONTROL Confirmer] mise en surbrillance.](../../images/ui/resources/schemas/select-fields.png)

Sélectionnez **[!UICONTROL Confirmer]** pour mettre à jour la zone de travail et refléter vos champs sélectionnés.


![&#x200B; Zone de travail de l’éditeur de schémas affichant la structure de schéma mise à jour après avoir confirmé les modifications de visibilité des champs dans la boîte de dialogue [!UICONTROL Gérer les champs associés] &#x200B;](../../images/ui/resources/schemas/fields-added.png).

#### Comportement des champs lors de la suppression ou de l’obsolescence de champs {#field-removal-deprecation-behavior}

Utilisez le tableau ci-dessous pour comprendre la portée de chaque action.

| Action | S’applique uniquement au schéma actuel | Modifie le groupe de champs | Affecte les autres schémas | Description |
|--------------------------|--------------------------------|----------------------|-----------------------|-------------|
| **Supprimer le champ** | Non | Oui | Oui | Supprime le champ du groupe de champs. Cela le supprime de tous les schémas utilisant ce groupe. |
| **Gérer les champs associés** | Oui | Non | Non | Masque uniquement les champs du schéma actuel. Le groupe de champs reste inchangé. |
| **Champ obsolète** | Non | Oui | Oui | Marque le champ comme obsolète dans le groupe de champs. Il n’est plus disponible dans aucun schéma. |

{style="table-layout:auto"}

>[!NOTE]
>
>Ce comportement est cohérent sur les schémas basés sur des enregistrements et sur des événements.

#### Ajouter des champs personnalisés à des groupes de champs {#add-fields}

Après avoir ajouté un groupe de champs à un schéma, vous pouvez définir des champs supplémentaires pour ce groupe. Toutefois, tous les champs ajoutés à un groupe de champs dans un schéma apparaissent également dans tous les autres schémas qui utilisent ce même groupe de champs.

En outre, si un champ personnalisé est ajouté à un groupe de champs standard, ce groupe de champs est converti en groupe de champs personnalisés et le groupe de champs standard d’origine n’est plus disponible.

Si vous souhaitez ajouter un champ personnalisé à un groupe de champs standard, reportez-vous à la [section ci-dessous](#custom-fields-for-standard-groups) pour obtenir des instructions spécifiques. Si vous ajoutez des champs à un groupe de champs personnalisés, reportez-vous à la section sur la [modification de groupes de champs personnalisés](./field-groups.md) dans le guide de l’interface utilisateur des groupes de champs .

Si vous ne souhaitez modifier aucun groupe de champs existant, vous pouvez [créer un groupe de champs personnalisé](./field-groups.md#create) pour définir des champs supplémentaires à la place.

## Ajout de champs à un schéma {#add-fields-to-schema}

L’éditeur de schémas propose plusieurs façons d’ajouter des champs à la structure de votre schéma. Choisissez l’approche qui correspond le mieux à vos besoins spécifiques.

Consultez les liens suivants pour en savoir plus sur les méthodes spécifiques d’ajout de champs à un schéma :

- [Ajouter des champs individuels](#add-individual-fields)
- [Ajouter des champs standard](#add-standard-fields)
- [Ajouter des champ personnalisés](#add-custom-fields)
- [Ajouter des champs personnalisés aux groupes de champs standard](#custom-fields-for-standard-groups)

### Ajout de champs individuels à un schéma {#add-individual-fields}

L’éditeur de schémas vous permet d’ajouter directement des champs individuels à un schéma si vous souhaitez éviter d’ajouter un groupe de champs entier pour un cas d’utilisation spécifique. Vous pouvez [ajouter des champs individuels à partir de groupes de champs standard](#add-standard-fields) ou [ajouter vos propres champs personnalisés](#add-custom-fields) à la place.

>[!IMPORTANT]
>
>Même si l’éditeur de schémas vous permet d’ajouter directement des champs individuels à un schéma, cela ne change pas le fait que tous les champs d’un schéma XDM doivent être fournis par sa classe ou un groupe de champs compatible avec cette classe. Comme les sections ci-dessous l’expliquent, tous les champs individuels sont toujours associés à une classe ou à un groupe de champs en tant qu’étape clé lorsqu’ils sont ajoutés à un schéma.

### Ajout de champs standard à un schéma {#add-standard-fields}

Vous pouvez ajouter directement des champs de groupes de champs standard à un schéma sans avoir à connaître au préalable le groupe de champs correspondant. Pour ajouter un champ standard à un schéma, sélectionnez l’icône plus (**+**) en regard du nom du schéma dans la zone de travail. Un espace réservé **[!UICONTROL Champ sans titre]** apparaît dans la structure du schéma et le rail de droite se met à jour pour afficher les commandes de configuration du champ.

![Zone de travail de l’éditeur de schémas avec un espace réservé [!UICONTROL Champ sans titre] ajouté et des commandes de configuration de champ affichées dans le rail de droite.](../../images/ui/resources/schemas/root-custom-field.png)

Sous **[!UICONTROL Nom du champ]**, commencez à saisir le nom du champ que vous souhaitez ajouter. Le système recherche automatiquement les champs standard correspondant à la requête et les répertorie sous **[!UICONTROL Champs standard recommandés]**, y compris les groupes de champs auxquels ils appartiennent.

![Rail de droite de l’éditeur de schémas affichant [!UICONTROL Champs standard recommandés] correspondant à la requête de nom de champ saisie.](../../images/ui/resources/schemas/standard-field-search.png)

Bien que certains champs standard partagent le même nom, leur structure peut varier en fonction du groupe de champs d’où ils proviennent. Si un champ standard est imbriqué dans un objet parent dans la structure du groupe de champs, le champ parent est également inclus dans le schéma si le champ enfant est ajouté.

Sélectionnez l’icône d’aperçu (![icône d’aperçu](/help/images/icons/preview.png)) à côté d’un champ standard pour afficher la structure de son groupe de champs et mieux comprendre comment il peut être imbriqué. Pour ajouter le champ standard au schéma, sélectionnez l’icône plus (![icône plus](/help/images/icons/add-circle.png)).

![Le panneau de configuration des champs de l’éditeur de schémas avec un aperçu de champ standard s’ouvre et l’icône d’ajout est mise en surbrillance.](../../images/ui/resources/schemas/add-standard-field.png)

La zone de travail se met à jour pour afficher le champ standard ajouté au schéma, y compris les champs parents sous lesquels il est imbriqué dans la structure du groupe de champs. Le nom du groupe de champs est également répertorié sous **[!UICONTROL Groupes de champs]** dans le rail de gauche. Si vous souhaitez ajouter d’autres champs du même groupe de champs, sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

![&#x200B; Zone de travail de l’éditeur de schémas affichant un champ standard ajouté à la structure du schéma, avec ses champs parents visibles et le groupe de champs répertorié dans le rail de gauche.](../../images/ui/resources/schemas/standard-field-added.png)

### Ajout de champs personnalisés à un schéma {#add-custom-fields}

Tout comme pour le workflow des champs standard, vous pouvez également ajouter vos propres champs personnalisés directement à un schéma.

Pour ajouter des champs au niveau racine d’un schéma, sélectionnez l’icône plus (**+**) à côté du nom du schéma dans la zone de travail. Un espace réservé **[!UICONTROL Champ sans titre]** apparaît dans la structure du schéma et le rail de droite se met à jour pour afficher les commandes de configuration du champ.

![&#x200B; Zone de travail de l’éditeur de schémas avec un espace réservé [!UICONTROL Champ sans titre] ajouté au niveau racine et des commandes de configuration de champ dans le rail de droite. &#x200B;](../../images/ui/resources/schemas/root-custom-field.png)

Commencez à saisir le nom du champ que vous souhaitez ajouter et le système lance automatiquement la recherche des champs standard correspondants. Pour créer un champ personnalisé à la place, sélectionnez l’option supérieure avec **([!UICONTROL Nouveau champ])**.

![Le rail de droite de l’éditeur de schémas avec un nom de champ personnalisé saisi et l’option [!UICONTROL Nouveau champ] mise en surbrillance dans les suggestions de nom de champ.](../../images/ui/resources/schemas/custom-field-search.png)

Après avoir fourni un nom d’affichage et un type de données pour le champ, l’étape suivante consiste à affecter le champ à une ressource XDM parent. Si votre schéma utilise une classe personnalisée, vous pouvez choisir d’[ajouter le champ à la classe affectée](#add-to-class) ou à un [groupe de champs](#add-to-field-group) à la place. Cependant, si votre schéma utilise une classe standard, vous ne pouvez affecter le champ personnalisé qu’à un groupe de champs.

#### Affecter le champ à un groupe de champs personnalisés {#add-to-field-group}

>[!NOTE]
>
>Cette section explique uniquement comment affecter le champ à un groupe de champs personnalisés. Si vous souhaitez étendre un groupe de champs standard avec le nouveau champ personnalisé à la place, consultez la section sur l’[ajout de champs personnalisés à des groupes de champs standard](#custom-fields-for-standard-groups).

Sous **[!UICONTROL Affecter à]**, sélectionnez **[!UICONTROL Groupe de champs]**. Si votre schéma utilise une classe standard, il s’agit de la seule option disponible ; elle est sélectionnée par défaut.

Vous devez ensuite sélectionner un groupe de champs pour le nouveau champ à associer. Commencez à saisir le nom du groupe de champs dans la saisie de texte fournie. Si des groupes de champs personnalisés existants correspondent à l’entrée, ils s’affichent dans la liste déroulante. Vous pouvez également saisir un nom unique pour créer un groupe de champs à la place.

![Rail de droite de l’éditeur de schémas avec l’option de groupe de champs [!UICONTROL Affecter à] sélectionnée et le champ d’entrée du nom du groupe de champs en surbrillance.](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Si vous sélectionnez un groupe de champs personnalisés existant, tous les autres schémas qui utilisent ce groupe de champs hériteront également du champ nouvellement ajouté après l’enregistrement de vos modifications. Pour cette raison, sélectionnez un groupe de champs existant uniquement si vous souhaitez ce type de propagation. Sinon, vous devez choisir de créer un groupe de champs personnalisés à la place.

Après avoir sélectionné le groupe de champs dans la liste, sélectionnez **[!UICONTROL Appliquer]**.

![Rail de droite de l’éditeur de schémas présentant la nouvelle configuration de champ personnalisé avec [!UICONTROL Appliquer] en surbrillance.](../../images/ui/resources/schemas/apply-field.png)

Le nouveau champ est ajouté à la zone de travail et dispose d’un espace de noms sous votre [identifiant client](../../api/getting-started.md#know-your-tenant_id) pour éviter les conflits avec les champs XDM standard. Le groupe de champs auquel vous avez associé le nouveau champ s’affiche également sous **[!UICONTROL Groupes de champs]** dans le rail de gauche.

![&#x200B; Zone de travail de l’éditeur de schémas affichant le nouveau champ personnalisé ajouté sous l’espace de noms de l’identifiant du client, avec le groupe de champs associé répertorié dans le rail de gauche. &#x200B;](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>Les autres champs fournis par le groupe de champs personnalisés sélectionné sont supprimés du schéma par défaut. Si vous souhaitez ajouter certains de ces champs au schéma, sélectionnez un champ appartenant au groupe, puis sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

#### Affecter le champ à une classe personnalisée {#add-to-class}

Sous **[!UICONTROL Affecter à]**, sélectionnez **[!UICONTROL Classe]**. Le champ d’entrée ci-dessous est remplacé par le nom de la classe personnalisée du schéma actuel, indiquant que le nouveau champ sera affecté à cette classe.

![L’option [!UICONTROL Classe] sélectionnée pour la nouvelle affectation de champ.](../../images/ui/resources/schemas/assign-field-to-class.png)

Continuez à configurer le champ comme vous le souhaitez et sélectionnez **[!UICONTROL Appliquer]** lorsque vous avez terminé.

![Le rail de droite de l’éditeur de schémas affiche le nouveau champ affecté à une classe personnalisée avec l’option [!UICONTROL Appliquer] mise en surbrillance.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

Le nouveau champ est ajouté à la zone de travail et dispose d’un espace de noms sous votre [identifiant client](../../api/getting-started.md#know-your-tenant_id) pour éviter les conflits avec les champs XDM standard. Si vous sélectionnez le nom de la classe dans le rail de gauche, le nouveau champ s’affiche dans la structure de la classe.

![Le nouveau champ appliqué à la structure de la classe personnalisée, représenté dans la zone de travail.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Ajouter des champs personnalisés aux groupes de champs standard {#custom-fields-for-standard-groups}

Si le schéma sur lequel vous travaillez comporte un champ de type objet fourni par un groupe de champs standard, vous pouvez ajouter vos propres champs personnalisés à cet objet standard.

>[!WARNING]
>
>Tous les champs ajoutés à un groupe de champs dans un schéma apparaissent également dans tous les autres schémas qui utilisent ce même groupe de champs. En outre, si un champ personnalisé est ajouté à un groupe de champs standard, ce groupe de champs est converti en groupe de champs personnalisés et le groupe de champs standard d’origine n’est plus disponible.
>
>Si vous avez participé à la version bêta de cette fonctionnalité, vous recevrez une boîte de dialogue vous informant des groupes de champs standard que vous avez précédemment personnalisés. Une fois que vous avez sélectionné **[!UICONTROL Confirmer]**, les ressources répertoriées sont converties en groupes de champs personnalisés.
>
>![La boîte de dialogue de confirmation de conversion Beta répertoriant les groupes de champs standard précédemment personnalisés avec l’option [!UICONTROL Accepter] mise en surbrillance.](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Pour commencer, sélectionnez l’icône plus (**+**) à côté de la racine de l’objet fourni par le groupe de champs standard.

![&#x200B; Zone de travail de l’éditeur de schémas avec l’icône plus mise en surbrillance en regard d’un objet de groupe de champs standard pour ajouter un champ personnalisé.](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Un message d’avertissement s’affiche, vous invitant à confirmer si vous souhaitez convertir le groupe de champs standard. Sélectionnez **[!UICONTROL Continuer à créer le groupe de champs]** pour continuer.

![La boîte de dialogue d’avertissement de l’éditeur de schémas vous invite à confirmer la conversion d’un groupe de champs standard, avec l’option [!UICONTROL &#x200B; Continuer à créer le groupe de champs &#x200B;] mise en surbrillance.](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

La zone de travail réapparaît avec un espace réservé sans titre pour le nouveau champ. Notez que le nom du groupe de champs standard a été ajouté avec « ([!UICONTROL Extended]) » pour indiquer qu’il a été modifié à partir de la version d’origine. À partir de là, utilisez les commandes du rail de droite pour définir les propriétés du champ.

![&#x200B; Zone de travail de l’éditeur de schémas affichant le groupe de champs standard renommé avec le suffixe [!UICONTROL étendu] et un champ d’espace réservé sans titre ajouté.](../../images/ui/resources/schemas/standard-field-group-converted.png)

Après avoir appliqué vos modifications, le nouveau champ s’affiche sous l’espace de noms de votre identifiant client dans l’objet standard. Cet espace de noms imbriqué empêche les conflits de nom de champ au sein du groupe de champs lui-même afin d’éviter de rompre les modifications dans d’autres schémas qui utilisent le même groupe de champs.

![&#x200B; Zone de travail de l’éditeur de schémas affichant le nouveau champ personnalisé ajouté sous l’espace de noms de l’identifiant du client dans le groupe de champs standard converti.](../../images/ui/resources/schemas/added-to-standard-object.png)

### Modifier les noms d’affichage des champs de schéma {#display-names}

Une fois que vous avez affecté une classe et ajouté des groupes de champs à un schéma, vous pouvez modifier les noms d’affichage de l’un des champs du schéma, que ces champs aient été fournis par des ressources XDM standard ou personnalisées.

>[!NOTE]
>
>Gardez à l’esprit que les noms d’affichage des champs qui appartiennent à des classes ou à des groupes de champs standard ne peuvent être modifiés que dans le contexte d’un schéma spécifique. En d’autres termes, la modification du nom d’affichage d’un champ standard dans un schéma n’affecte pas les autres schémas qui utilisent la même classe ou le même groupe de champs associé.
>
>Une fois que vous avez apporté des modifications aux noms d’affichage des champs d’un schéma, ces modifications sont immédiatement répercutées dans tous les jeux de données existants basés sur ce schéma.

Remplacez les noms de champ par les noms d’affichage en appuyant sur **[!UICONTROL Afficher les noms d’affichage des champs]**. Pour modifier le nom d’affichage d’un champ de schéma, sélectionnez le champ dans la zone de travail. Dans le rail de droite, indiquez le nouveau nom sous **[!UICONTROL Nom d’affichage]**.

![Éditeur de schémas avec un champ sélectionné dans la zone de travail et le champ [!UICONTROL Nom d’affichage] en surbrillance dans le rail de droite.](../../images/ui/resources/schemas/display-name.png)

Sélectionnez **[!UICONTROL Appliquer]** dans le rail de droite, et la zone de travail se met à jour pour afficher le nouveau nom d’affichage du champ. Sélectionnez **[!UICONTROL Enregistrer]** pour appliquer les modifications au schéma.

![&#x200B; Zone de travail de l’éditeur de schémas affichant le nom d’affichage du champ mis à jour, avec l’option [!UICONTROL Enregistrer] mise en surbrillance.](../../images/ui/resources/schemas/display-name-changed.png)

## Gérer les schémas {#manage-schemas}

Les tâches de gestion des schémas sont disponibles à deux emplacements principaux dans l’interface utilisateur d’Experience Platform. Choisissez le workflow approprié en fonction de l’emplacement où vous utilisez vos schémas.

### Gestion des schémas à partir de la vue Parcourir {#manage-from-browse}

Cette section décrit les actions de schéma disponibles dans l’onglet **[!UICONTROL Parcourir]**. Pour plus d’informations sur la découverte, le filtrage et l’organisation des schémas, consultez la section [exploration des ressources XDM](../explore.md).

![L’onglet [!UICONTROL Parcourir] de l’espace de travail Schémas s’ouvre pour une ligne de schéma et affiche des actions intégrées, notamment [!UICONTROL Modifier], [!UICONTROL Supprimer], [!UICONTROL Appliquer des libellés] et [!UICONTROL Gérer les balises].](../../images/ui/explore/schema-inline-actions.png)

Les sections suivantes décrivent les actions de gestion des schémas disponibles dans l’onglet **[!UICONTROL Parcourir]**. Ces actions sont accessibles par le biais du menu représentant des points de suspension (...) en regard de chaque ligne de schéma.

| Action | Description |
|--------|-------------|
| [!UICONTROL Modifier les propriétés d’un schéma] | Modifie les informations de base sur le schéma, notamment le nom d’affichage, la description et les balises sans ouvrir l’éditeur de schémas. Pour obtenir des instructions détaillées, voir [Modifier les propriétés du schéma](#edit-schema-properties). |
| [!UICONTROL Supprimer le schéma] | Supprime le schéma de votre organisation. Disponible uniquement pour les schémas non activés pour le profil client en temps réel et sans jeux de données associés. Pour obtenir des instructions détaillées, voir [Supprimer le schéma](#delete-schema). |
| [!UICONTROL Appliquer des libellés] (gouvernance des données) | Attribue des libellés d’utilisation des données pour classer les schémas en fonction des politiques de confidentialité et des exigences de conformité. Les libellés appliqués au niveau du schéma se propagent à tous les jeux de données créés à partir de ce schéma. Pour obtenir des instructions détaillées, voir [Appliquer des libellés de gouvernance des données](#apply-data-governance-labels). |
| [!UICONTROL Créer un jeu de données] | Crée un nouveau jeu de données à partir du schéma sélectionné. Pour obtenir des instructions détaillées, voir [Créer un jeu de données](#create-dataset). |
| [!UICONTROL Gérer les balises] | Ajoute ou supprime des balises définies par l’utilisateur pour l’organisation du schéma. Pour obtenir des instructions détaillées, voir [Gestion des balises](#manage-tags). |
| [!UICONTROL Déplacer vers le dossier] | Déplace les schémas dans les hiérarchies de dossiers. Pour obtenir des instructions détaillées, voir [&#x200B; Déplacer vers le dossier &#x200B;](#move-to-folder). |
| [!UICONTROL Ajouter au package &#x200B;] | Inclut le schéma dans un package d’outils Sandbox pour un déploiement dans les environnements. Pour obtenir des instructions détaillées, voir [&#x200B; Ajouter au package &#x200B;](#add-to-package). |
| [!UICONTROL Copier la structure JSON] | Copie la représentation JSON complète du schéma dans le presse-papiers. Pour obtenir des instructions détaillées, voir [Copie de la structure JSON](#copy-json-structure). |
| [!UICONTROL Télécharger l’exemple de fichier] | Génère et télécharge un fichier de données d’exemple conforme à la structure du schéma. Pour obtenir des instructions détaillées, voir [&#x200B; Télécharger l’exemple de fichier &#x200B;](#download-sample-file). |

{style="table-layout:auto"}

>[!NOTE]
>
>Les fichiers d’exemple servent à tester la structure du schéma et ne doivent pas contenir de données de production.

#### Modification des propriétés d’un schéma {#edit-schema-properties}

Permet d’accéder directement à l’éditeur de schémas avec votre schéma prérempli.

#### Supprimer le schéma {#delete-schema}

Supprime le schéma de votre organisation. La suppression est disponible uniquement pour les schémas qui n’ont pas été activés pour le profil client en temps réel et qui n’ont aucun jeu de données associé. Une fois supprimé, le schéma ne peut pas être récupéré.

#### Appliquer les libellés de gouvernance des données {#apply-data-governance-labels}

Permet d’accéder directement à l’onglet [!UICONTROL Libellé] de l’espace de travail Schémas. Pour obtenir des instructions complètes, reportez-vous à la documentation [Gérer les libellés d’utilisation des données pour un schéma](https://experienceleague.adobe.com/fr/docs/experience-platform/xdm/tutorials/labels#select-schema-field).

#### Création d’un jeu de données {#create-dataset}

>[!AVAILABILITY]
>
>Cette action est disponible uniquement pour les schémas standard (non relationnels).

Ouvre la boîte de dialogue **[!UICONTROL Créer un jeu de données à partir d’un schéma]** avec le nom du schéma source pré-renseigné. Saisissez un jeu de données **[!UICONTROL Nom]** et, éventuellement, une **[!UICONTROL Description]**, puis sélectionnez **[!UICONTROL Créer un jeu de données]** pour créer le jeu de données.

![La boîte de dialogue [!UICONTROL Créer un jeu de données à partir d’un schéma] avec les champs [!UICONTROL Nom] et [!UICONTROL Description] en surbrillance et le bouton [!UICONTROL Créer un jeu de données].](../../images/ui/explore/create-dataset-from-schema-dialog.png)

Une fois le jeu de données créé, il s’ouvre dans l’espace de travail [!UICONTROL Jeux de données].

#### Gérer les balises {#manage-tags}

Ouvre la boîte de dialogue [!UICONTROL Ajouter ou supprimer des balises] dans laquelle vous pouvez affecter ou supprimer des balises définies par l’utilisateur du schéma. Les balises affectées à un schéma apparaissent dans l’inventaire des schémas et peuvent être utilisées à des fins de filtrage. Pour plus d’informations sur l’organisation basée sur les balises, voir [exploration des ressources XDM](../explore.md).

#### Déplacer vers le dossier {#move-to-folder}

Ouvre la boîte de dialogue [!UICONTROL Déplacer] dans laquelle vous pouvez sélectionner un dossier de destination ou en créer un nouveau. Les schémas organisés en dossiers apparaissent dans la hiérarchie des dossiers dans le rail de gauche. Pour plus d’informations sur l’organisation basée sur les dossiers, voir [exploration des ressources XDM](../explore.md).

#### Ajouter au package {#add-to-package}

Inclut le schéma dans un package d’outils Sandbox pour un déploiement dans les environnements. Le schéma doit répondre aux exigences d’éligibilité du package. Les packages contenant des schémas peuvent être exportés et importés entre des sandbox.

#### Copier la structure JSON {#copy-json-structure}

Copie la représentation JSON complète du schéma dans le presse-papiers. La sortie correspond à la structure du schéma telle qu’elle est stockée dans le registre des schémas et peut être utilisée pour les opérations de l’API ou le partage de schéma.

#### Télécharger le fichier d’exemple {#download-sample-file}

Génère et télécharge un fichier de données d’exemple conforme à la structure du schéma. Le fichier contient des exemples de valeurs pour chaque champ défini dans le schéma. Les fichiers d’exemple sont destinés uniquement au test de la structure du schéma et ne doivent pas contenir de données de production.

### Gestion des schémas à partir de l’éditeur de schémas {#manage-from-editor}

Dans l’éditeur de schémas, vous pouvez effectuer des actions rapides pour copier la structure JSON du schéma ou supprimer le schéma s’il n’a pas été activé pour le profil client en temps réel et ne comporte aucun jeu de données associé. Sélectionnez [!UICONTROL Plus] en haut de la vue pour afficher une liste déroulante avec des actions rapides.

![L’éditeur de schémas avec le bouton [!UICONTROL Plus] en surbrillance et le menu déroulant des actions rapides affiché.](../../images/tutorials/create-schema/more-actions.png)

La fonctionnalité Copier la structure JSON vous permet de voir à quoi ressemblerait un exemple de payload pendant que vous créez le schéma et vos pipelines de données. Elle s’avère particulièrement utile dans les cas où le schéma contient des structures de mappage d’objets complexes, telles qu’un mappage d’identités.

## Finalisation d’un schéma {#finalize-schema}

Une fois la personnalisation de la structure et des champs du schéma terminée, vous devrez peut-être effectuer des étapes supplémentaires pour préparer l’utilisation en production. Ces dernières étapes de configuration garantissent que votre schéma est correctement intégré aux services Experience Platform.

### Activer un schéma pour le profil client en temps réel {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Activation d&#39;un schéma pour Profil"
>abstract="Lorsqu’un schéma est activé pour Profil, tous les jeux de données créés à partir de ce schéma participent au profil client en temps réel, qui fusionne les données de différentes sources pour créer une vue complète de chaque client ou cliente. Une fois qu&#39;un schéma est utilisé pour ingérer des données dans Profil, il ne peut pas être désactivé. Pour plus d&#39;informations, consultez la documentation."

Le [profil client en temps réel](../../../profile/home.md) fusionne des données provenant de sources disparates afin de créer une vue complète de chaque client individuel. Si vous souhaitez que les données capturées par un schéma participent à ce processus, vous devez activer le schéma pour une utilisation dans [!DNL Profile].

>[!IMPORTANT]
>
>Pour activer un schéma pour [!DNL Profile], un champ d’identité principale doit être défini. Pour plus d’informations, consultez le guide sur la [définition de champs d’identité](../fields/identity.md).

Pour activer le schéma, commencez par sélectionner le nom du schéma dans le rail de gauche, puis sélectionnez le bouton bascule **[!UICONTROL Profil]** dans le rail de droite.

![L’éditeur de schémas avec le nom du schéma sélectionné dans le rail de gauche et le bouton [!UICONTROL Profil] en surbrillance dans le rail de droite.](../../images/ui/resources/schemas/profile-toggle.png)

Une fenêtre contextuelle s’affiche, vous avertissant qu’une fois qu’un schéma a été activé et enregistré, il ne peut pas être désactivé. Sélectionnez **[!UICONTROL Activer]** pour continuer.

![La fenêtre contextuelle de confirmation [!UICONTROL Activer pour le profil] avec le bouton [!UICONTROL Activer] en surbrillance.](../../images/ui/resources/schemas/profile-confirm.png)

La zone de travail réapparaît avec le bouton [!UICONTROL Profile] activé.

>[!IMPORTANT]
>
>Puisque le schéma n’est pas encore enregistré, c’est le point de non-retour si vous changez d’avis sur la possibilité de laisser le schéma participer au profil client en temps réel : une fois que vous avez enregistré un schéma activé, il ne peut plus être désactivé. Sélectionnez à nouveau le bouton (bascule) **[!UICONTROL Profil]** pour désactiver le schéma.

Pour terminer le processus, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma.

![Rail de droite de l’éditeur de schémas affichant le bouton (bascule) [!UICONTROL Profil] à l’état activé.](../../images/ui/resources/schemas/profile-enabled.png)

Le schéma peut désormais être utilisé dans le profil client en temps réel. Lorsqu’Experience Platform ingère des données dans des jeux de données basés sur ce schéma, ces données sont intégrées aux données de profil fusionnées.

### Modification de la classe d’un schéma {#change-class}

Vous pouvez modifier la classe d’un schéma à tout moment au cours du processus de composition initiale, avant que le schéma ne soit enregistré.

>[!WARNING]
>
>La réattribution de la classe d’un schéma doit être effectuée avec une extrême prudence. Les groupes de champs ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialisera la zone de travail et tous les champs que vous avez ajoutés.

Pour réaffecter une classe, sélectionnez **[!UICONTROL Affecter]** dans la partie gauche de la zone de travail.

![Zone de travail de l’éditeur de schémas avec le bouton [!UICONTROL Attribuer] en surbrillance sur le côté gauche.](../../images/ui/resources/schemas/assign-class-button.png)

Une boîte de dialogue s’affiche. Elle répertorie toutes les classes disponibles, y compris celles définies par votre organisation (le propriétaire étant « [!UICONTROL Client] »), ainsi que les classes standard définies par Adobe.

Sélectionnez une classe dans la liste pour afficher sa description dans la partie droite de la boîte de dialogue. Vous pouvez également sélectionner **[!UICONTROL Prévisualiser la structure de la classe]** pour afficher les champs et les métadonnées associés à la classe. Sélectionnez **[!UICONTROL Attribuer une classe]** pour continuer.

![La boîte de dialogue [!UICONTROL Attribuer une classe] qui affiche les classes disponibles avec la description de classe sélectionnée affichée et [!UICONTROL Attribuer une classe] en surbrillance.](../../images/ui/resources/schemas/assign-class.png)

Une nouvelle boîte de dialogue s’ouvre, vous demandant de confirmer que vous souhaitez attribuer une nouvelle classe. Sélectionnez **[!UICONTROL Attribuer]** pour confirmer.

![Boîte de dialogue de confirmation de réaffectation de classe avec le bouton [!UICONTROL Affecter] en surbrillance.](../../images/ui/resources/schemas/assign-confirm.png)

Après avoir confirmé le changement de classe, la zone de travail sera réinitialisée et toute progression de la composition sera perdue.

## Étapes suivantes {#next-steps}

Ce document présente les principes de base de la création et de la modification de schémas dans l’interface utilisateur d’Experience Platform. Il est vivement recommandé de consulter le [tutoriel sur la création de schéma](../../tutorials/create-schema-ui.md) pour un workflow complet de création d’un schéma complet dans l’interface utilisateur, y compris la création de groupes de champs personnalisés et de types de données pour des cas d’utilisation uniques.

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la présentation de l’espace de travail [[!UICONTROL Schémas]](../overview.md).

Pour savoir comment gérer les schémas dans l’API [!DNL Schema Registry], consultez le guide [sur les points d’entrée des schémas](../../api/schemas.md).

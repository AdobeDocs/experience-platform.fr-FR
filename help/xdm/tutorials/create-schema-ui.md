---
keywords: Experience Platform;accueil;rubriques populaires;iu;IU;XDM;système XDM;modèle de données d’expérience;Modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;éditeur de schémas;éditeur de schémas;schéma;schémas;schémas;schémas;créer
solution: Experience Platform
title: Créer un schéma à l’aide de l’éditeur de schémas
type: Tutorial
description: Ce tutoriel décrit les étapes de création d’un schéma à l’aide de l’éditeur de schémas d’Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '4670'
ht-degree: 60%

---

# Créer un schéma à l’aide de l’[!DNL Schema Editor]

L’interface utilisateur d’Adobe Experience Platform vous permet de créer et de gérer des schémas de [!DNL Experience Data Model] (XDM) dans une zone de travail visuelle interactive appelée l’[!DNL Schema Editor]. Ce tutoriel explique comment créer un schéma à l’aide de l’[!DNL Schema Editor].

À des fins de démonstration, les étapes de ce tutoriel concernent la création d’un exemple de schéma qui décrit les membres d’un programme de fidélité des clients. Vous pouvez utiliser ces étapes pour créer un schéma différent pour vos propres besoins. Cependant, il est recommandé de suivre d’abord la création de l’exemple de schéma pour découvrir les fonctionnalités de l’[!DNL Schema Editor].

>[!NOTE]
>
>Si vous ingérez des données CSV dans Experience Platform, vous pouvez [mapper ces données à un schéma XDM créé par des recommandations générées par l’IA](../../ingestion/tutorials/map-csv/recommendations.md) (actuellement en version bêta) sans avoir à créer manuellement le schéma.
>
>Si vous préférez composer un schéma à l’aide de l’API [!DNL Schema Registry], veuillez commencer par lire le [[!DNL Schema Registry] guide du développeur](../api/getting-started.md) avant de vous lancer dans le tutoriel sur la [création d’un schéma à l’aide de l’API](create-schema-api.md).

## Prise en main

Ce tutoriel demande une bonne compréhension des différents aspects d’Adobe Experience Platform relatifs à la création de schémas. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux concepts suivants :

* [[!DNL Experience Data Model (XDM)]](../home.md) : cadre normalisé selon lequel [!DNL Experience Platform] organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../schema/composition.md) : présentation des schémas XDM et de leurs blocs de création, notamment les classes, les groupes de champs de schéma, les types de données et les champs individuels.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Ouvrir l’espace de travail [!UICONTROL Schemas] {#browse}

L’espace de travail [!UICONTROL Schemas] de l’interface utilisateur de [!DNL Experience Platform] permet de visualiser les [!DNL Schema Library] et d’afficher et de gérer les schémas disponibles pour votre organisation. L’espace de travail comprend également l’[!DNL Schema Editor], la zone de travail sur laquelle vous allez composer un schéma tout au long de ce tutoriel.

Après vous être connecté à [!DNL Experience Platform], sélectionnez **[!UICONTROL Schemas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail **[!UICONTROL Schemas]**. L’onglet **[!UICONTROL Browse]** affiche une liste des schémas (une représentation de la [!DNL Schema Library]) que vous pouvez afficher et personnaliser. La liste comprend le nom, le type, la classe et le comportement (enregistrement ou série chronologique) sur lesquels repose le schéma, ainsi que la date et l’heure de la dernière modification du schéma.

Reportez-vous au guide sur l’[exploration des ressources XDM existantes dans l’interface utilisateur](../ui/explore.md) pour plus d’informations.

## Création et attribution d’un nom à un schéma {#create}

Pour commencer à composer un schéma, sélectionnez **[!UICONTROL Create schema]** dans le coin supérieur droit de l’espace de travail **[!UICONTROL Schemas]**.

![Onglet [!UICONTROL Schemas] de l’espace de travail [!UICONTROL Browse] avec le [!UICONTROL Create schema] en surbrillance.](../images/tutorials/create-schema/create-schema-button.png)

La boîte de dialogue [!UICONTROL Create a schema] s’affiche. Dans cette boîte de dialogue, vous pouvez choisir de créer manuellement un schéma en ajoutant des champs et des groupes de champs, ou de charger un fichier CSV et d’utiliser des algorithmes ML pour générer un schéma. Sélectionnez un workflow de création de schéma dans la boîte de dialogue.

![La boîte de dialogue Créer un schéma avec les options de workflow et sélectionnez en surbrillance.](../images/tutorials/create-schema/create-a-schema-dialog.png)

### [!BADGE Beta &#x200B;]{type=Informative} création manuelle ou assistée par machine learning de schéma {#manual-or-assisted}

Pour découvrir comment utiliser un algorithme ML afin de recommander une structure de schéma basée sur un fichier chargé, consultez le guide de création de schéma assisté par machine learning [machine learning](../ui/ml-assisted-schema-creation.md). Ce guide de l’interface utilisateur se concentre sur le workflow de création manuelle .

### Choisir une classe de base {#choose-a-class}

Le workflow [!UICONTROL Create schema] s’affiche. Choisissez ensuite une classe de base pour le schéma. Vous pouvez choisir entre les classes principales [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent], ou [!UICONTROL Other] si ces classes ne répondent pas à vos besoins. L’option [!UICONTROL Other] des classes vous permet de [créer une classe](#create-new-class) ou de choisir parmi d’autres classes préexistantes.

Pour plus d’informations sur ces classes, consultez la documentation [[!UICONTROL XDM individual profile]](../classes/individual-profile.md) et [[!UICONTROL XDM ExperienceEvent]](../classes/experienceevent.md) . Pour les besoins de ce tutoriel, sélectionnez **[!UICONTROL XDM Individual Profile]** suivi de **[!UICONTROL Next]**.

![Workflow de [!UICONTROL Create schema] avec les options et [!UICONTROL XDM individual profile] de [!UICONTROL Next] mises en surbrillance.](../images/tutorials/create-schema/individual-profile-base-class.png)

### Nom et révision {#name-and-review}

Après avoir sélectionné une classe, la section [!UICONTROL Name and review] s’affiche. Dans cette section, vous indiquez un nom et une description pour identifier votre schéma. Plusieurs éléments importants doivent être pris en compte lors du choix d’un nom pour votre schéma :

* Le nom d’un schéma doit être court et descriptif afin qu’il puisse être facilement retrouvé par la suite.
* Le nom d’un schéma doit être unique, ce qui signifie qu’il doit également être suffisamment précis pour ne pas être réutilisé à l’avenir. Par exemple, si votre organisation dispose de programmes de fidélité distincts pour différentes marques, nous vous conseillons de nommer votre schéma « Brand A Loyalty Members » pour faciliter la distinction avec d’autres schémas relatifs à la fidélité que vous pourriez définir ultérieurement.
* Vous pouvez également utiliser la description du schéma pour fournir toute information contextuelle supplémentaire le concernant.

Ce tutoriel décrit la composition d’un schéma pour ingérer les données relatives aux membres d’un programme de fidélité, c’est pourquoi le schéma est nommé « [!DNL Loyalty Members] ».

&#x200B;La structure de base du schéma (fournie par la classe ) s’affiche dans la zone de travail pour que vous puissiez consulter et vérifier la structure de classe et de schéma sélectionnée.

Saisissez un [!UICONTROL Schema display name] convivial dans le champ de texte. Saisissez ensuite une description appropriée pour vous aider à identifier votre schéma. Une fois que vous avez révisé votre structure de schéma et que vos paramètres vous conviennent, sélectionnez **[!UICONTROL Finish]** pour créer votre schéma.

![Section [!UICONTROL Name and review] du workflow de [!UICONTROL Create schema] avec les [!UICONTROL Schema display name], [!UICONTROL Description] et [!UICONTROL Finish] en surbrillance.](../images/ui/resources/schemas/name-and-review.png)

### Composer le schéma {#compose-your-schema}

L’[!DNL Schema Editor] apparaît. C’est la zone de travail sur laquelle vous allez composer votre schéma. Le schéma doté d’un titre est automatiquement créé dans la section **[!UICONTROL Structure]** de la zone de travail lorsque vous accédez à l’éditeur, avec les champs standard inclus dans la classe de base que vous avez sélectionnée. La classe affectée pour le schéma est également répertoriée sous **[!UICONTROL Class]** dans **[!UICONTROL Composition]** section .

>[!NOTE]
>
>Vous pouvez mettre à jour le nom d’affichage et la description facultative du schéma à partir de la barre latérale **[!UICONTROL Schema properties]**. Une fois qu’un nouveau nom est saisi, la zone de travail se met automatiquement à jour pour refléter le nouveau nom du schéma.

![L’éditeur de schémas avec la classe de base et le diagramme de schéma mis en surbrillance.](../images/tutorials/create-schema/loyalty-members-schema-editor.png)

>[!NOTE]
>
>Vous pouvez [modifier la classe d’un schéma](#change-class) à tout moment au cours du processus de composition initial avant que le schéma ne soit enregistré, mais cela doit être fait avec la plus grande prudence. Les groupes de champs ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialisera la zone de travail et tous les champs que vous avez ajoutés.

## Ajouter un groupe de champs {#field-group}

Vous pouvez maintenant commencer à ajouter des champs à votre schéma grâce à l’ajout de groupes de schémas. Un groupe de champs est un groupe d’un ou de plusieurs champs souvent utilisés conjointement pour décrire un concept particulier. Ce tutoriel utilise des groupes de champs pour décrire les membres du programme de fidélité et recueillir des informations clés telles que le nom, la date d’anniversaire, le numéro de téléphone, l’adresse, etc.

Pour ajouter un groupe de champs, sélectionnez **[!UICONTROL Add]** dans la sous-section **[!UICONTROL Field groups]**.

![Éditeur de schémas avec le bouton Ajouter des groupes de champs en surbrillance.](../images/tutorials/create-schema/add-field-group-button.png)

Une nouvelle boîte de dialogue apparait. Elle présente la liste des groupes de champs disponibles. Chaque groupe de champs est uniquement destiné à une utilisation avec une classe spécifique. Par conséquent, la boîte de dialogue ne répertorie que les groupes de champs compatibles avec la classe que vous avez sélectionnée (dans ce cas, la classe [!DNL XDM Individual Profile]). Si vous utilisez une classe XDM standard, la liste des groupes de champs sera triée intelligemment en fonction de la popularité de l’utilisation.

![Boîte de dialogue [!UICONTROL Add field groups].](../images/tutorials/create-schema/field-group-popularity.png)

Vous pouvez utiliser l’un des filtres dans le rail de gauche pour limiter la liste des groupes de champs standard à des [secteurs](../schema/industries/overview.md) comme la vente au détail, les services financiers et les services de santé.

![La boîte de dialogue [!UICONTROL Add field groups] avec les groupes de champs du secteur est mise en surbrillance.](../images/tutorials/create-schema/industry-field-groups.png)

Lorsqu’un groupe de champs est sélectionné dans la liste, il s’affiche dans le rail de droite. Si vous le souhaitez, vous pouvez sélectionner plusieurs groupes de champs en les ajoutant chacun à la liste dans le rail de droite avant de confirmer la sélection. En outre, l’icône qui s’affiche sur le côté droit du groupe de champs sélectionné vous permet de prévisualiser la structure des champs qu’il présente.

![La boîte de dialogue [!UICONTROL Add field groups] avec l’icône d’aperçu du groupe de champs sélectionné mise en surbrillance.](../images/tutorials/create-schema/preview-field-group-button.png)

Lors de la prévisualisation d’un groupe de champs, une description détaillée du schéma du groupe de champs est fournie dans le rail droit. Vous pouvez également parcourir les champs du groupe de champs dans la zone de travail. Lorsque vous sélectionnez différents champs, le rail de droite se met à jour pour afficher les détails du champ en question. Sélectionnez **[!UICONTROL Back]** lorsque vous avez terminé la prévisualisation pour revenir à la boîte de dialogue de sélection du groupe de champs.

![La boîte de dialogue [!UICONTROL Preview field group] avec le groupe de champs Détails démographiques est prévisualisée.](../images/tutorials/create-schema/preview-field-group.png)

Pour ce tutoriel, sélectionnez le groupe de champs **[!UICONTROL Demographic Details]**, puis sélectionnez **[!UICONTROL Add field group]**.

![La boîte de dialogue [!UICONTROL Add field groups] avec le groupe de champs Détails démographiques sélectionné et [!UICONTROL Add field groups] mise en surbrillance.](../images/tutorials/create-schema/demographic-details.png)

La zone de travail du schéma réapparaît. La section **[!UICONTROL Field groups]** répertorie désormais « [!UICONTROL Demographic Details] » et la section **[!UICONTROL Structure]** inclut les champs fournis par le groupe de champs. Vous pouvez sélectionner le nom du groupe de champs sous la section **[!UICONTROL Field groups]** pour mettre en surbrillance les champs spécifiques qu’il fournit dans la zone de travail.

![Éditeur de schémas avec les groupes de champs Détails démographiques mis en surbrillance.](../images/tutorials/create-schema/demographic-details-structure.png)

>[!NOTE]
>
>Dans l’éditeur de schémas, les classes et les groupes de champs standard (générés par Adobe) sont indiqués par l’icône de cadenas (icône de cadenas ![A).](/help/images/icons/lock-closed.png). Le cadenas s’affiche dans le rail de gauche à côté du nom de la classe ou du groupe de champs, ainsi qu’à côté de tout champ du diagramme de schéma qui fait partie d’une ressource générée par le système.
>
>![Éditeur de schémas avec l’icône de cadenas mise en surbrillance](../images/ui/explore/padlock-icon-highlight.png)

Ce groupe de champs fournit plusieurs champs sous le nom de niveau supérieur `person` avec le type de données « [!UICONTROL Person] ». Ce groupe de champs décrit les informations sur un individu, notamment son nom, sa date de naissance et son genre.

>[!NOTE]
>
>N’oubliez pas que les champs peuvent utiliser des types scalaires (chaîne, entier, tableau ou date), ainsi que tout type de données (un groupe de champs représentant un concept commun) défini dans [!DNL Schema Registry].

Notez que le champ `name` possède un type de données « [!UICONTROL Full name] », ce qui signifie qu’il décrit lui aussi un concept commun et contient des sous-champs liés au nom, tels que le prénom, le nom de famille, le titre de courtoisie et le suffixe.

Sélectionnez les différents champs dans la zone de travail pour afficher les champs supplémentaires contribuant à la structure du schéma.

## Ajouter d’autres groupes de champs {#field-group-2}

Vous pouvez maintenant répéter les mêmes étapes pour ajouter un autre groupe de champs. Lorsque la boîte de dialogue **[!UICONTROL Add field group]** s’affiche cette fois-ci, vous remarquerez que le groupe de champs « [!UICONTROL Demographic Details] » est grisé et que la case à cocher adjacente ne peut pas être sélectionnée. Cela vous évite de dupliquer accidentellement des groupes de champs que vous avez déjà inclus dans le schéma actuel.

Pour ce tutoriel, sélectionnez les groupes de champs standard **[!UICONTROL Personal Contact Details]** et **[!UICONTROL Loyalty Details]** dans la liste, puis sélectionnez **[!UICONTROL Add field groups]** pour les ajouter au schéma.

![Boîte de dialogue [!UICONTROL Add field groups] avec deux nouveaux groupes de champs sélectionnés et [!UICONTROL Add field groups] mis en surbrillance.](../images/tutorials/create-schema/more-field-groups.png)

La zone de travail réapparaît avec les groupes de champs ajoutés sous **[!UICONTROL Field groups]** dans la section **[!UICONTROL Composition]** et leurs champs composites ajoutés à la structure du schéma.

![L’éditeur de schémas avec la nouvelle structure de schéma composite mise en surbrillance.](../images/tutorials/create-schema/updated-structure.png)

## Définir un groupe de champs personnalisé {#define-field-group}

Le schéma [!UICONTROL Loyalty Members] est destiné à capturer des données relatives aux membres d’un programme de fidélité. Le groupe de champs de [!UICONTROL Loyalty Details] standard que vous avez ajouté au schéma fournit la plupart de ces informations, notamment le type de programme, les points, la date d’inscription, etc.

Cependant, il peut arriver que vous souhaitiez inclure d’autres champs personnalisés non couverts par des groupes de champs standard afin d’atteindre vos cas d’utilisation. Dans le cas de l’ajout de champs de fidélité personnalisés, vous disposez de deux options :

1. Créer un groupe de champs personnalisé pour capturer ces champs. Il s’agit de la méthode qui sera abordée dans ce tutoriel.
1. Étendez le groupe de champs standard [!UICONTROL Loyalty Details] avec des champs personnalisés. Cela entraîne la conversion de [!UICONTROL Loyalty Details] en un groupe de champs personnalisés et le groupe de champs standard d’origine ne sera plus disponible. Pour plus d’informations sur [!UICONTROL Schemas]l’ajout de champs personnalisés à la structure des groupes de champs standard[, consultez le guide de l’interface utilisateur &#x200B;](../ui/resources/schemas.md#custom-fields-for-standard-groups) .

Pour créer un groupe de champs, sélectionnez **[!UICONTROL Add]** dans la sous-section **[!UICONTROL Field groups]** comme avant, mais cette fois, sélectionnez **[!UICONTROL Create New Field group]** dans la partie supérieure de la boîte de dialogue qui s’affiche. Vous êtes alors invité à fournir un nom d’affichage et une description pour le nouveau groupe de champs. Pour ce tutoriel, nommez le nouveau groupe de champs « [!DNL Custom Loyalty Details] », puis sélectionnez **[!UICONTROL Add field groups]**.

![La boîte de dialogue [!UICONTROL Add field groups] avec [!UICONTROL Create new field group], [!UICONTROL Display name] et [!UICONTROL Description] mis en surbrillance.](../images/tutorials/create-schema/create-new-field-group.png)

>[!NOTE]
>
>Comme pour les noms de classe, le nom du groupe de champs doit être court et simple, décrivant ce que le groupe de champs va apporter au schéma. Ces noms sont également uniques. Vous ne pourrez donc pas réutiliser le nom et devrez donc veiller à ce qu’il soit suffisamment spécifique.

« [!DNL Custom Loyalty Details] » devrait maintenant apparaître sous **[!UICONTROL Field groups]** sur le côté gauche de la zone de travail, mais aucun champ n’y est encore associé et, par conséquent, aucun nouveau champ n’apparaît sous **[!UICONTROL Structure]**.

## Ajouter des champs au groupe de champs {#field-group-fields}

Maintenant que vous avez créé le groupe de champs « [!DNL Custom Loyalty Details] », il est temps de définir les champs que le groupe de champs va ajouter au schéma.

Pour commencer, sélectionnez l’icône **plus (+)** située à côté du nom du schéma dans la zone de travail.

![Éditeur de schémas avec l’icône plus mise en surbrillance.](../images/tutorials/create-schema/add-field.png)

Un espace réservé « [!UICONTROL Untitled Field] » apparaît dans la zone de travail, et le rail de droite se met à jour pour afficher les options de configuration du champ.

![L’éditeur de schémas avec un [!UICONTROL Untitled Field] et le schéma [!UICONTROL Field properties] mis en surbrillance.](../images/tutorials/create-schema/untitled-field.png)

Dans ce scénario, le schéma doit comporter un champ de type objet qui décrit en détail le niveau de fidélité actuel de la personne. À l’aide des commandes du rail de droite, commencez à créer un champ de `loyaltyTier` de type « [!UICONTROL Object] » qui sera utilisé pour contenir vos champs associés.

Sous **[!UICONTROL Assign to]**, vous devez sélectionner un groupe de champs auquel affecter le champ. N’oubliez pas que tous les champs de schéma appartiennent à une classe ou à un groupe de champs. Comme ce schéma utilise une classe standard, votre seule option est de sélectionner un groupe de champs. Commencez à saisir le nom « [!DNL Custom Loyalty Details] », puis sélectionnez le groupe de champs dans la liste.

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Apply]**.

![L’éditeur de schémas avec l’objet Niveau de fidélité ajouté au schéma [!UICONTROL Field properties] mis en surbrillance.](../images/tutorials/create-schema/loyalty-tier-object.png)

Les modifications sont appliquées et le nouvel objet « `loyaltyTier` » s’affiche. Puisqu’il s’agit d’un champ personnalisé, il est automatiquement imbriqué dans un espace de noms d’objet associé à l’identifiant du client de votre organisation, précédé d’un trait de soulignement (`_tenantId` dans cet exemple).

![L’éditeur de schémas avec l’identifiant du client et le niveau de fidélité mis en surbrillance dans le diagramme de schéma.](../images/tutorials/create-schema/tenant-id.png)

>[!NOTE]
>
>La présence de l’ID du client indique que les champs que vous ajoutez sont contenus dans l’espace de noms de votre organisation.
>
>En d’autres termes, les champs que vous ajoutez sont propres à votre organisation et vont être enregistrés dans [!DNL Schema Registry] dans une zone spécifique accessible uniquement par votre organisation. Les champs que vous définissez doivent toujours être ajoutés à votre espace de noms client pour empêcher les conflits avec des noms provenant d’autres classes, groupes de champs, types de données et champs standard.

Sélectionnez l’icône **plus (+)** à côté de l’objet `loyaltyTier` pour commencer à ajouter des sous-champs. Un espace réservé pour le nouveau champ apparaît et la section **[!UICONTROL Field properties]** est visible sur le côté droit de la zone de travail.

![L’éditeur de schémas avec l’identifiant du client et le nouveau sous-champ ajouté au niveau de fidélité dans le diagramme de schéma.](../images/tutorials/create-schema/new-field-in-loyalty-tier-object.png)

Chaque champ nécessite les informations suivantes :

* **[!UICONTROL Field Name]:** Nom du champ, écrit de préférence en CamelCase. Aucune espace n’est autorisé. Il s’agit du nom utilisé pour référencer le champ dans le code et dans d’autres applications en aval.
   * Exemple : loyaltyLevel
* **[!UICONTROL Display Name]:** nom du champ, écrit en casse de titre. Il s’agit du nom qui s’affiche dans la zone de travail lors de l’affichage ou de la modification du schéma.
   * Exemple : Loyalty Level
* **[!UICONTROL Type]:** type de données du champ. Cela inclut les types scalaires de base et tous les types de données définis dans [!DNL Schema Registry]. Exemples : [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone number], etc.
* **[!UICONTROL Description]:** Une description facultative du champ doit être incluse avec un maximum de 200 caractères.

Le premier champ de l’objet `loyaltyTier` sera une chaîne de caractères appelée `id`, représentant l’ID du niveau actuel du membre du programme de fidélité. L’ID de niveau sera unique pour chaque membre du programme de fidélité, car cette entreprise définit différents seuils de point de niveau de fidélité pour chaque client en fonction de différents facteurs. Définissez le type du nouveau champ sur « [!UICONTROL String] » et la section **[!UICONTROL Field properties]** se remplit de plusieurs options pour l’application de contraintes, y compris la valeur par défaut, le format et la longueur maximale. Pour en savoir plus, consultez la documentation sur [les bonnes pratiques relatives aux champs de validation des données](../schema/best-practices.md#data-validation-fields).

![L’éditeur de schémas avec les valeurs de propriété du champ du nouveau champ d’identifiant mises en surbrillance.](../images/tutorials/create-schema/string-constraints.png)

Comme `id` est une chaîne à structure libre générée de manière aléatoire, aucune autre contrainte n’est nécessaire. Sélectionnez **[!UICONTROL Apply]** pour appliquer vos modifications.

![Éditeur de schémas avec le champ d’identifiant ajouté et mis en surbrillance.](../images/tutorials/create-schema/id-field-added.png)

## Ajouter des champs supplémentaires au groupe de champs {#field-group-fields-2}

Maintenant que vous avez ajouté le champ `id`, vous pouvez ajouter des champs supplémentaires pour recueillir des informations relatives à la fidélité, par exemple :

* Seuil de point actuel (entier) : nombre minimal de points de fidélité que le membre doit conserver pour rester au niveau actuel.
* Seuil de point de niveau supérieur (entier) : nombre de points de fidélité que le membre doit acquérir pour passer au niveau supérieur.
* Date d’entrée en vigueur (date et heure) : date à laquelle le membre du programme de fidélité a rejoint ce niveau.

Pour ajouter chaque champ au schéma, sélectionnez l’icône **plus (+)** à côté de l’objet `loyalty` et renseignez les informations requises.

Une fois cette étape terminée, l’objet `loyaltyTier` contiendra des champs pour `id`, `currentThreshold`, `nextThreshold`, et `effectiveDate`.

![Éditeur de schémas avec l’objet Niveau de fidélité mis en surbrillance.](../images/tutorials/create-schema/loyalty-tier-object-fields.png)

## Ajouter un champ d’énumération au groupe de champs {#enum}

Lorsque vous définissez des champs dans le [!DNL Schema Editor], vous pouvez appliquer certaines options supplémentaires aux types de champs de base afin de fournir d’autres contraintes aux données que le champ peut contenir. Les cas d’utilisation de ces contraintes sont expliqués dans le tableau suivant :

| Contrainte | Description |
| --- | --- |
| [!UICONTROL Required] | Indique que le champ est obligatoire pour l’ingestion de données. Toute donnée chargée dans un jeu de données basé sur ce schéma qui ne contient pas ce champ sera défaillante lors de l’ingestion. |
| [!UICONTROL Array] | Indique que le champ contient un tableau de valeurs, chacune avec le type de données spécifié. Par exemple, l’utilisation de cette contrainte sur un champ avec un type de données « [!UICONTROL String] » indique que le champ contiendra un tableau de chaînes. |
| [!UICONTROL Enum & Suggested Values] | Une énumération indique que ce champ doit contenir une des valeurs d’une liste énumérée de valeurs possibles. Vous pouvez également utiliser cette option pour fournir une liste des valeurs suggérées pour un champ de chaîne sans limiter le champ à ces valeurs. |
| [!UICONTROL Identity] | Indique que ce champ est un champ d’identité. Vous trouverez plus d’informations sur les champs d’identité [dans la suite de ce tutoriel](#identity-field). |
| [!UICONTROL Relationship] | Bien que les relations de schéma puissent être déduites par l’utilisation du schéma d’union et [!DNL Real-Time Customer Profile], cela s’applique uniquement aux schémas partageant la même classe. La contrainte [!UICONTROL Relationship] indique que ce champ fait référence à l’identité principale d’un schéma basée sur une classe différente, ce qui implique une relation entre les deux schémas. Pour plus d’informations, consultez le tutoriel sur [la définition d’une relation](./relationship-ui.md). |

{style="table-layout:auto"}

>[!NOTE]
>
>Tous les champs obligatoires d’identité ou de relation sont répertoriés dans leurs sections respectives du rail de gauche, ce qui vous permet de localiser facilement ces champs, quelle que soit la complexité du schéma.

Pour ce tutoriel, l’objet `loyaltyTier` dans le schéma nécessite un nouveau champ d’énumération qui décrit la classe de niveau, où la valeur ne peut être que l’une des quatre options possibles. Pour ajouter ce champ au schéma, sélectionnez l’icône **plus (+)** à côté de l’objet `loyaltyTier` et renseignez les champs requis pour **[!UICONTROL Field name]** et **[!UICONTROL Display name]**. Par **[!UICONTROL Type]**, sélectionnez « [!UICONTROL String] ».

![Éditeur de schémas avec l’objet de classe de niveau ajouté et mis en surbrillance dans le [!UICONTROL Field properties].](../images/tutorials/create-schema/tier-class-type.png)

D’autres cases à cocher s’affichent pour le champ une fois son type sélectionné, y compris les cases à cocher pour **[!UICONTROL Array]**, **[!UICONTROL Enum & Suggested Values]**, **[!UICONTROL Identity]** et **[!UICONTROL Relationship]**.

Cochez la case **[!UICONTROL Enum & Suggested Values]**, puis sélectionnez **[!UICONTROL Enum]**. Vous pouvez saisir ici les **[!UICONTROL Value]** (en Camel Case - casse mixte) et **[!UICONTROL Display Name]** (nom facultatif et facile à lire écrit en Title Case - 1ère lettre des mots en majuscule) pour chaque classe de fidélité acceptable.

Une fois toutes les propriétés de champ renseignées, sélectionnez **[!UICONTROL Apply]** pour ajouter le champ `tierClass` à l’objet `loyaltyTier`.

![Les propriétés des champs énumération et suggérer des valeurs sont terminées avec [!UICONTROL Apply] mise en surbrillance.](../images/tutorials/create-schema/tier-class-enum.png)

## Conversion d’un objet à plusieurs champs en un type de données {#datatype}

L’objet `loyaltyTier` contient désormais plusieurs champs et représente une structure de données commune qui peut s’avérer utile dans d’autres schémas. Le [!DNL Schema Editor] vous permet d’appliquer facilement des objets à champs multiples réutilisables en convertissant la structure de ces objets en types de données.

Les types de données permettent l’utilisation cohérente de structures à champs multiples, avec plus de flexibilité qu’un groupe de champs, car elles peuvent être utilisées n’importe où dans un schéma. Pour ce faire, définissez la valeur de **[!UICONTROL Type]** du champ sur celle de tout type de données défini dans le [!DNL Schema Registry].

Pour convertir l’objet `loyaltyTier` en type de données, sélectionnez le champ `loyaltyTier` dans la zone de travail, puis sélectionnez **[!UICONTROL Convert to new data type]** sur le côté droit de l’éditeur sous **[!UICONTROL Field properties]**.

![Éditeur de schémas avec l’objet loyaltyTier et le [!UICONTROL Convert to new data type] mis en surbrillance.](../images/tutorials/create-schema/convert-data-type.png)

Une notification s’affiche, confirmant que la conversion de l’objet a réussi. Dans la zone de travail, vous pouvez maintenant voir que le champ `loyaltyTier` comporte désormais une icône de lien et que le rail droit indique qu’il possède un type de données « [!DNL Loyalty Tier] ».

![L’éditeur de schémas avec l’objet loyaltyTier et le nouveau nom d’affichage mis en surbrillance.](../images/tutorials/create-schema/loyalty-tier-data-type.png)

Dans un prochain schéma, vous pourrez désormais attribuer un champ en tant que type « [!DNL Loyalty Tier] », ce qui inclurait automatiquement des champs pour l’ID, la classe de niveau, les seuils de point et la date d’entrée en vigueur.

>[!NOTE]
>
>Vous pouvez également créer et modifier des types de données personnalisés indépendamment de la modification des schémas. Consultez le guide sur la [création et modification des types de données](../ui/resources/data-types.md) pour plus d’informations.

## Rechercher et filtrer des champs de schéma

Votre schéma contient désormais plusieurs groupes de champs en plus des champs fournis par sa classe de base. Lorsque vous utilisez des schémas plus volumineux, vous pouvez cocher les cases situées à côté des noms des groupes de champs dans le rail de gauche pour filtrer les champs affichés uniquement par rapport aux groupes de champs qui vous intéressent.

![Certaines cases à cocher sont sélectionnées dans la section Groupes de champs de l’éditeur de schémas pour réduire la taille du diagramme de schéma.](../images/tutorials/create-schema/filter-by-field-group.png)

Si vous recherchez un champ spécifique dans votre schéma, vous pouvez également utiliser la barre de recherche pour filtrer les champs affichés par nom, quel que soit le groupe de champs sous lequel ils sont fournis.

![Champ de recherche de l’éditeur de schémas avec les résultats pertinents mis en surbrillance sur la zone de travail.](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La fonction de recherche prend en compte les filtres de groupes de champs sélectionnés lors de l’affichage des champs correspondants. Si une requête de recherche n’affiche pas les résultats attendus, vous devrez peut-être vérifier par deux fois que vous n’êtes pas en train de filtrer un groupe de champs approprié.

## Définition d’un champ de schéma comme champ d’identité {#identity-field}

La structure de données standard fournie par les schémas peut être exploitée pour identifier les données appartenant à la même personne sur plusieurs sources, ce qui permet d’utiliser divers cas d’utilisation en aval, tels que la segmentation, la création de rapports, l’analyse de la science des données, etc. Pour regrouper des données en fonction d’identités individuelles, les champs clés doivent être marqués comme des champs [!UICONTROL Identity] dans les schémas applicables.

[!DNL Experience Platform] permet d’indiquer facilement un champ d’identité grâce à une case à cocher **[!UICONTROL Identity]** dans le [!DNL Schema Editor]. Cependant, vous devez déterminer quel champ est le meilleur candidat à utiliser comme identité, en fonction de la nature de vos données.

Par exemple, il peut y avoir des milliers de membres du programme de fidélité appartenant au même niveau de fidélité, et plusieurs d’entre eux peuvent partager la même adresse physique. Dans ce scénario, cependant, chaque membre du programme de fidélité fournit lors de l’inscription son adresse électronique personnelle. Puisque les adresses e-mail personnelles sont généralement gérées par une seule personne, le `personalEmail.address` de champ (fourni par le groupe de champs [!UICONTROL Personal Contact Details] ) est un bon candidat pour un champ d’identité.

>[!IMPORTANT]
>
>Les étapes décrites ci-dessous expliquent comment ajouter un descripteur d’identité à un champ de schéma existant. Au lieu de définir des champs d’identité dans la structure du schéma lui-même, vous pouvez également utiliser un champ `identityMap` pour contenir des informations d’identité.
>
>Si vous envisagez d’utiliser `identityMap`, gardez à l’esprit qu’il remplacera toute identité principale que vous ajoutez directement au schéma. Pour plus d’informations, consultez la section sur `identityMap` dans les [principes de base du guide de composition de schémas](../schema/composition.md#identityMap).

Sélectionnez le champ `personalEmail.address` dans la zone de travail, et la case à cocher **[!UICONTROL Identity]** apparaît sous **[!UICONTROL Field properties]**. Cochez la case et vous aurez la possibilité de la définir comme **[!UICONTROL Primary identity]**. Cochez également cette case.

>[!NOTE]
>
>Chaque schéma ne peut contenir qu’un seul champ d’identité principal. Une fois qu’un champ du schéma a été défini comme identité principale, vous recevrez un message d’erreur si vous tentez par la suite de définir un autre champ d’identité du schéma comme identité principale.

Ensuite, vous devez fournir un **[!UICONTROL Identity namespace]** à partir de la liste des espaces de noms prédéfinis dans la liste déroulante. Puisque ce champ correspond à l’adresse e-mail du client, sélectionnez « [!UICONTROL Email] » dans la liste déroulante. Sélectionnez **[!UICONTROL Apply]** pour confirmer les mises à jour du champ `personalEmail.address` .

![Éditeur de schémas avec l’adresse e-mail mise en surbrillance et la case à cocher Identité du Principal activée.](../images/tutorials/create-schema/primary-identity.png)

>[!NOTE]
>
>Pour obtenir la liste des espaces de noms standard et leurs définitions, consultez la [[!DNL Identity Service] documentation](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Après application de la modification, l’icône `personalEmail.address` affiche un symbole d’empreinte digitale, indiquant qu’il s’agit désormais d’un champ d’identité. Le champ est également répertorié dans le rail de gauche sous **[!UICONTROL Identities]**.

![L’éditeur de schémas avec l’adresse e-mail et le champ d’identité en surbrillance dans la barre latérale de composition de schémas.](../images/tutorials/create-schema/identity-applied.png)

Désormais, toutes les données ingérées dans le champ `personalEmail.address` seront utilisées pour aider à identifier cet individu et à établir une vue unique de ce client. Pour en savoir plus sur l’utilisation des identités dans [!DNL Experience Platform], veuillez consultez la documentation d’[[!DNL Identity Service]](../../identity-service/home.md).

## Activer le schéma pour l’utiliser dans [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) exploite les données d’identité dans [!DNL Experience Platform] afin de fournir une vue holistique de chaque client individuel. Le service crée des profils fiables et complets des attributs des clients, ainsi que des comptes horodatés de chaque interaction des clients dans n’importe quel système intégré à [!DNL Experience Platform].

Pour qu’un schéma puisse être utilisé avec [!DNL Real-Time Customer Profile], il doit avoir une identité principale définie. Vous recevrez un message d’erreur si vous tentez d’activer un schéma sans avoir préalablement défini une identité principale.

![Boîte de dialogue Identité principale manquante.](../images/tutorials/create-schema/missing-primary-identity.png)

Pour utiliser le schéma « Membres du programme de fidélité » dans [!DNL Profile], commencez par sélectionner le titre du schéma dans la zone de travail.

Dans la partie droite de l’éditeur, des informations sur le schéma sont affichées, notamment son nom d’affichage, sa description et son type. En plus de ces informations, vous trouverez également un bouton bascule **[!UICONTROL Profile]** .

![L’éditeur de schémas avec la racine de schéma et le bouton Activer pour le profil mis en surbrillance.](../images/tutorials/create-schema/profile-toggle.png)

Sélectionnez **[!UICONTROL Profile]** et une fenêtre contextuelle s’affiche, vous demandant de confirmer que vous souhaitez activer le schéma pour [!DNL Profile].

![Boîte de dialogue de confirmation Activer pour le profil.](../images/tutorials/create-schema/enable-profile.png)

>[!WARNING]
>
>Une fois qu’un schéma a été activé pour [!DNL Real-Time Customer Profile] et enregistré, il ne peut pas être désactivé.

Sélectionnez **[!UICONTROL Enable]** pour confirmer votre choix. Vous pouvez de nouveau sélectionner le bouton (bascule) **[!UICONTROL Profile]** pour désactiver le schéma si vous le souhaitez, mais une fois que le schéma a été enregistré alors que [!DNL Profile] est activé, il ne peut plus être désactivé.

## Actions supplémentaires {#more}

Dans l’éditeur de schémas, vous pouvez également effectuer des actions rapides pour copier la structure JSON du schéma ou supprimer le schéma. Sélectionnez [!UICONTROL More] en haut de la vue pour afficher une liste déroulante avec des actions rapides.

![Éditeur de schémas avec le bouton Plus en surbrillance et les options de liste déroulante affichées.](../images/tutorials/create-schema/more-actions.png)

### Supprimer un schéma {#delete-a-schema}

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_profileenabledwithdatasets"
>title="Impossible de supprimer le schéma"
>abstract="Le schéma ne peut pas être supprimé, car il a été activé pour Profile et contient des jeux de données associés."

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_profileenablednodatasets"
>title="Impossible de supprimer le schéma"
>abstract="Le schéma ne peut pas être supprimé, car il a été activé pour Profile."

>[!CONTEXTUALHELP]
>id="platform_schemas_delete_withdatasetsnotprofileenabled"
>title="Impossible de supprimer le schéma"
>abstract="Le schéma ne peut pas être supprimé, car il comporte des jeux de données associés."

Un schéma peut être supprimé de l’interface utilisateur de l’éditeur de schémas à l’aide d’actions [!UICONTROL More], ainsi que des détails du schéma dans l’onglet [!UICONTROL Browse] . Certaines conditions empêchent la suppression d’un schéma. Un schéma ne peut pas être supprimé si :

* Le schéma est activé pour Profil.
* Le schéma est activé pour Profil et est associé à des jeux de données.
* Le schéma est associé à des jeux de données mais n’est pas activé pour Profil.

### Copier la structure JSON {#copy-json-structure}

Sélectionnez **[!UICONTROL Copy JSON structure]** pour générer une payload d’exportation pour tout schéma de la bibliothèque des schémas. Cette action copie la structure JSON dans le presse-papiers. Le fichier JSON exporté peut ensuite être utilisé pour importer le schéma et les ressources associées dans un autre sandbox ou une autre organisation. Cela rend le partage et la réutilisation des schémas entre différents environnements simples et efficaces.

## Étapes suivantes et ressources supplémentaires

Maintenant que vous avez fini de composer le schéma, vous pouvez voir le schéma complet dans la zone de travail. Sélectionnez **[!UICONTROL Save]** et le schéma sera enregistré dans le [!DNL Schema Library], ce qui le rendra accessible par le [!DNL Schema Registry].

Votre nouveau schéma peut maintenant être utilisé pour ingérer des données dans [!DNL Experience Platform]. Pour rappel, une fois que le schéma a été utilisé pour ingérer des données, seules des modifications additives peuvent être apportées. Reportez-vous aux [principes de base de la composition des schémas](../schema/composition.md) pour plus d’informations sur le contrôle de version des schémas.

Vous pouvez maintenant suivre le tutoriel sur la [définition d’une relation de schéma dans l’interface utilisateur](./relationship-ui.md) pour ajouter un nouveau champ de relation au schéma « Membres du programme de fidélité ».

Vous pouvez également consulter et gérer le schéma « Membres du programme de fidélité » à l’aide de l’API [!DNL Schema Registry]. Pour commencer à utiliser l’API, consultez d’abord le [[!DNL Schema Registry API] guide de développement](../api/getting-started.md).

### Ressources vidéo

>[!WARNING]
>
>L’interface utilisateur [!DNL Experience Platform] affichée dans les vidéos suivantes est obsolète. Consultez la documentation pour découvrir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.

La vidéo suivante montre comment créer un schéma simple dans l’interface utilisateur [!DNL Experience Platform].

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

La vidéo suivante est destinée à vous aider à mieux comprendre l’utilisation des groupes et classes de champ.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Annexe

Les sections suivantes apportent des informations supplémentaires sur l’utilisation de [!DNL Schema Editor].

### Création d’une nouvelle classe {#create-new-class}

[!DNL Experience Platform] offre la possibilité de définir un schéma basé sur une classe propre à votre organisation. Pour apprendre à créer une nouvelle classe, consultez le guide sur la [création et modification de classes dans l’interface utilisateur](../ui/resources/classes.md#create).

### Modification de la classe d’un schéma {#change-class}

Vous pouvez modifier la classe d’un schéma à tout moment au cours du processus de composition initiale, avant que le schéma ne soit enregistré.

>[!WARNING]
>
>La réattribution de la classe d’un schéma doit être effectuée avec une extrême prudence. Les groupes de champs ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialisera la zone de travail et tous les champs que vous avez ajoutés.

Pour apprendre à modifier la classe d’un schéma, consultez le guide sur la [gestion des schémas dans l’interface utilisateur](../ui/resources/schemas.md#change-class).

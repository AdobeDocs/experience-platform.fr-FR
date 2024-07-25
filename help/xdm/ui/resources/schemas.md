---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;schéma;schémas
solution: Experience Platform
title: Création et modification de schémas dans l’interface utilisateur
description: Découvrez les principes de base de la création et de l’édition de schémas dans l’interface utilisateur de l’Experience Platform.
exl-id: be83ce96-65b5-4a4a-8834-16f7ef9ec7d1
source-git-commit: 19f1f64434d655d3b19260460519018fc9c8e174
workflow-type: tm+mt
source-wordcount: '3736'
ht-degree: 3%

---

# Créer et modifier les schémas dans l’interface utilisateur {#create-edit-schemas-in-ui}

Ce guide explique comment créer, modifier et gérer des schémas de modèle de données d’expérience (XDM) pour votre organisation dans l’interface utilisateur de Adobe Experience Platform.

>[!IMPORTANT]
>
>Les schémas XDM sont extrêmement personnalisables. Par conséquent, les étapes de création d’un schéma peuvent varier en fonction du type de données que vous souhaitez que le schéma capture. Par conséquent, ce document couvre uniquement les interactions de base que vous pouvez effectuer avec les schémas dans l’interface utilisateur et exclut les étapes associées telles que la personnalisation des classes, des groupes de champs de schéma, des types de données et des champs.
>
>Pour une présentation complète du processus de création de schéma, suivez le [tutoriel de création de schéma](../../tutorials/create-schema-ui.md) pour créer un exemple complet de schéma et vous familiariser avec les nombreuses fonctionnalités de [!DNL Schema Editor].

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et aux [ principes de base de la composition des schémas](../../schema/composition.md) pour une présentation de la manière dont les schémas sont construits.

## Créer un schéma {#create}

>[!NOTE]
>
>Cette section explique comment créer manuellement un nouveau schéma dans l’interface utilisateur. Si vous ingérez des données CSV dans Platform, vous pouvez choisir de [mapper ces données à un schéma XDM créé par les recommandations générées par l’IA](../../../ingestion/tutorials/map-csv/recommendations.md) (actuellement en version bêta) sans avoir à créer manuellement le schéma.

Dans l’espace de travail [!UICONTROL Schémas], sélectionnez **[!UICONTROL Créer un schéma]** dans le coin supérieur droit.

![ L’espace de travail des schémas avec [!UICONTROL Créer un schéma] surligné.](../../images/ui/resources/schemas/create-schema.png)

Le workflow [!UICONTROL Créer un schéma] s’affiche. Vous pouvez choisir une classe de base pour le schéma en sélectionnant **[!UICONTROL Individual Profile]**, **[!UICONTROL Experience Event]** ou **[!UICONTROL Other]**, suivi de **[!UICONTROL Next]** pour confirmer votre choix. Pour plus d’informations sur ces classes, consultez la documentation [XDM Individual profile](../../classes/individual-profile.md) et [XDM ExperienceEvent](../../classes/experienceevent.md) .

![Le workflow [!UICONTROL Créer un schéma] avec les trois options de classe et [!UICONTROL Suivant] mis en surbrillance.](../../images/ui/resources/schemas/schema-class-options.png)

Une fois que vous avez sélectionné une classe, la section [!UICONTROL Nom et révision] s’affiche. Dans cette section, vous fournissez un nom et une description pour identifier votre schéma. &#x200B;La structure de base du schéma (fournie par la classe) s’affiche dans la zone de travail afin que vous puissiez examiner et vérifier la classe et la structure de schéma sélectionnés.

Saisissez un [!UICONTROL nom d’affichage de schéma] convivial dans le champ de texte. Saisissez ensuite une description appropriée pour vous aider à identifier votre schéma. Une fois la structure de votre schéma revue et vos paramètres satisfaits, sélectionnez **[!UICONTROL Terminer]** pour créer votre schéma.

![La section [!UICONTROL Nom et révision] du workflow [!UICONTROL Créer un schéma] avec le [!UICONTROL nom d’affichage du schéma], la [!UICONTROL Description] et la [!UICONTROL Terminer] mise en surbrillance.](../../images/ui/resources/schemas/name-and-review.png)

L&#39;onglet [!UICONTROL Schéma] [!UICONTROL Parcourir] s&#39;affiche. Le schéma que vous venez de créer est maintenant répertorié dans la bibliothèque de schémas et peut être modifié dans le [!DNL Schema Editor].

![ L&#39;onglet Parcourir de l&#39;espace de travail des schémas affichant votre schéma que vous venez de créer.](../../images/ui/resources/schemas/example-schema.png)

## Modifier un schéma existant {#edit}

>[!NOTE]
>
>Une fois qu’un schéma a été enregistré et utilisé dans l’ingestion de données, seules des modifications additifs peuvent lui être apportées. Pour plus d’informations, voir les [règles de l’évolution du schéma](../../schema/composition.md#evolution) .

Pour modifier un schéma existant, sélectionnez l’onglet **[!UICONTROL Parcourir]**, puis sélectionnez le nom du schéma à modifier. Vous pouvez également utiliser la barre de recherche pour réduire la liste des options disponibles.

![ L’espace de travail du schéma avec un schéma en surbrillance.](../../images/ui/resources/schemas/edit-schema.png)

>[!TIP]
>
>Vous pouvez utiliser les fonctionnalités de recherche et de filtrage de l’espace de travail pour faciliter la recherche du schéma. Pour plus d’informations, consultez le guide sur l’ [exploration des ressources XDM](../explore.md) .

Une fois que vous avez sélectionné un schéma, le [!DNL Schema Editor] apparaît avec la structure du schéma affichée dans la zone de travail. Vous pouvez désormais [ajouter des groupes de champs](#add-field-groups) au schéma (ou [ajouter des champs individuels](#add-individual-fields) à partir de ces groupes), [modifier les noms d’affichage des champs](#display-names) ou [modifier les groupes de champs personnalisés existants](./field-groups.md#edit) si le schéma en utilise un.

## Actions supplémentaires {#more}

Dans l’éditeur de schémas, vous pouvez également exécuter des actions rapides pour copier la structure JSON du schéma ou supprimer le schéma s’il n’a pas été activé pour Real-time Customer Profile ou s’il comporte des jeux de données associés. Sélectionnez [!UICONTROL Plus] en haut de la vue pour afficher une liste déroulante avec des actions rapides.

La fonctionnalité Copier la structure JSON vous permet de voir à quoi ressemblerait un exemple de payload pendant que vous créez encore le schéma et vos pipelines de données. Elle s’avère particulièrement utile dans les situations où il existe des structures de mappage d’objet complexes dans le schéma, telles qu’une carte d’identité.

![ L’éditeur de schémas avec le bouton Plus en surbrillance et les options de liste déroulante s’affichent.](../../images/tutorials/create-schema/more-actions.png)

## Bascule du nom d’affichage {#display-name-toggle}

Pour votre commodité, l’éditeur de schémas propose un bouton d’activation/désactivation pour modifier les noms de champ d’origine et les noms d’affichage plus lisibles. Cette flexibilité permet d’améliorer la visibilité des champs et l’édition de vos schémas. Le bouton bascule se trouve en haut à droite de la vue de l’éditeur de schémas.

>[!NOTE]
>
>Le changement des noms de champ en noms d’affichage est purement cosmétique et ne modifie aucune ressource en aval.

![ L’éditeur de schémas avec [!UICONTROL  Afficher les noms d’affichage pour les champs] surligné.](../../images/ui/resources/schemas/display-name-toggle.png)

Les noms d’affichage des groupes de champs standard sont générés par le système, mais peuvent être personnalisés, comme décrit dans la section [noms d’affichage](#display-names) . Les noms d’affichage sont reflétés dans plusieurs vues d’interface utilisateur, y compris les aperçus de mappage et de jeu de données. Le paramètre par défaut est désactivé et affiche les noms des champs selon leurs valeurs d’origine.

## Ajout de groupes de champs à un schéma {#add-field-groups}

>[!NOTE]
>
>Cette section explique comment ajouter des groupes de champs existants à un schéma. Si vous souhaitez créer un groupe de champs personnalisé, reportez-vous au guide sur la [création et modification de groupes de champs](./field-groups.md#create) à la place.

Une fois que vous avez ouvert un schéma dans [!DNL Schema Editor], vous pouvez ajouter des champs au schéma à l’aide de groupes de champs. Pour commencer, sélectionnez **[!UICONTROL Ajouter]** en regard de **[!UICONTROL Groupes de champs]** dans le rail de gauche.

![L’éditeur de schémas avec l’ [!UICONTROL ajout] de la section [!UICONTROL Groupes de champs] mise en surbrillance.](../../images/ui/resources/schemas/add-field-group-button.png)

Une boîte de dialogue s’affiche, affichant la liste des groupes de champs que vous pouvez sélectionner pour le schéma. Puisque les groupes de champs ne sont compatibles qu’avec une seule classe, seuls les groupes de champs associés à la classe sélectionnée du schéma sont répertoriés. Par défaut, les groupes de champs répertoriés sont triés en fonction de leur popularité d’utilisation au sein de votre entreprise.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] est mise en surbrillance avec la colonne [!UICONTROL Popularité] mise en surbrillance.](../../images/ui/resources/schemas/field-group-popularity.png)

Si vous connaissez l’activité générale ou le domaine d’activité des champs que vous souhaitez ajouter, sélectionnez une ou plusieurs des catégories de secteur vertical dans le rail de gauche pour filtrer la liste affichée des groupes de champs.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] est mise en surbrillance avec les filtres [!UICONTROL Secteur] et la colonne [!UICONTROL Secteur] mise en surbrillance.](../../images/ui/resources/schemas/industry-filter.png)

>[!NOTE]
>
>Pour plus d’informations sur les bonnes pratiques de modélisation des données spécifiques à un secteur d’activité dans XDM, consultez la documentation sur les [modèles de données du secteur](../../schema/industries/overview.md).

Vous pouvez également utiliser la barre de recherche pour localiser le groupe de champs souhaité. Les groupes de champs dont le nom correspond à la requête apparaissent en haut de la liste. Sous **[!UICONTROL Champs standard]**, des groupes de champs contenant des champs qui décrivent les attributs de données souhaités s’affichent.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] avec la fonction de recherche [!UICONTROL Champs standard] mise en surbrillance.](../../images/ui/resources/schemas/field-group-search.png)

Cochez la case en regard du nom du groupe de champs que vous souhaitez ajouter au schéma. Vous pouvez sélectionner plusieurs groupes de champs dans la liste, chaque groupe de champs sélectionné apparaissant dans le rail de droite.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] avec la fonction de sélection de case à cocher mise en surbrillance.](../../images/ui/resources/schemas/add-field-group.png)

>[!TIP]
>
>Pour tout groupe de champs répertorié, vous pouvez pointer ou vous concentrer sur l’icône d’informations (![icône d’information](/help/images/icons/info.png)) pour afficher une brève description du type de données que le groupe de champs capture. Vous pouvez également sélectionner l’icône d’aperçu (![icône d’aperçu](/help/images/icons/preview.png)) pour afficher la structure des champs fournis par le groupe de champs avant de décider de l’ajouter au schéma.

Une fois que vous avez choisi vos groupes de champs, sélectionnez **[!UICONTROL Ajouter des groupes de champs]** pour les ajouter au schéma.

![La boîte de dialogue [!UICONTROL Ajouter des groupes de champs] avec les groupes de champs sélectionnés et [!UICONTROL Ajouter des groupes de champs] surlignée.](../../images/ui/resources/schemas/add-field-group-finish.png)

[!DNL Schema Editor] réapparaît avec les champs fournis par le groupe de champs représentés dans la zone de travail.

![ [!DNL Schema Editor] avec un exemple de schéma affiché.](../../images/ui/resources/schemas/field-groups-added.png)

>[!NOTE]
>
>Dans l’éditeur de schémas, les classes standard (générées par un Adobe) et les groupes de champs sont indiqués par l’icône de cadenas (![Icône de cadenas.](/help/images/icons/lock-closed.png). Le cadenas s’affiche dans le rail de gauche en regard du nom de la classe ou du groupe de champs, ainsi qu’en regard de tout champ du diagramme de schéma qui fait partie d’une ressource générée par le système.
>
>![L’éditeur de schéma avec l’icône de cadenas mise en surbrillance](../../images/ui/explore/schema-editor-padlock-icon.png)

Après avoir ajouté un groupe de champs à un schéma, vous pouvez éventuellement [supprimer des champs existants](#remove-fields) ou [ajouter de nouveaux champs personnalisés](#add-fields) à ces groupes, en fonction de vos besoins.

### Supprimer les champs ajoutés des groupes de champs {#remove-fields}

Après avoir ajouté un groupe de champs à un schéma, vous pouvez supprimer tous les champs dont vous n’avez pas besoin.

>[!NOTE]
>
>La suppression de champs d’un groupe de champs affecte uniquement le schéma en cours de traitement et n’affecte pas le groupe de champs lui-même. Si vous supprimez des champs dans un schéma, ces champs sont toujours disponibles dans tous les autres schémas qui utilisent le même groupe de champs.

Dans l’exemple suivant, le groupe de champs standard **[!UICONTROL Demographic Details]** a été ajouté à un schéma. Pour supprimer un champ unique, tel que `taxId`, sélectionnez le champ dans la zone de travail, puis sélectionnez **[!UICONTROL Supprimer]** dans le rail de droite.

![Le [!DNL Schema Editor] avec [!UICONTROL Supprimer] surligné. Cette action supprime un seul champ.](../../images/ui/resources/schemas/remove-single-field.png)

Si vous souhaitez supprimer plusieurs champs, vous pouvez gérer le groupe dans son ensemble. Sélectionnez un champ appartenant au groupe dans la zone de travail, puis sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

![Le [!DNL Schema Editor] avec [!UICONTROL Gérer les champs connexes] mis en surbrillance.](../../images/ui/resources/schemas/manage-related-fields.png)

Une boîte de dialogue s’affiche, indiquant la structure du groupe de champs en question. À partir de là, vous pouvez utiliser les cases à cocher fournies pour sélectionner ou désélectionner les champs dont vous avez besoin. Lorsque vous êtes satisfait, sélectionnez **[!UICONTROL Confirmer]**.

![ La boîte de dialogue [!UICONTROL Gérer les champs connexes] avec les champs sélectionnés et l’option [!UICONTROL Confirmer] mise en surbrillance.](../../images/ui/resources/schemas/select-fields.png)

Le canevas réapparaît avec uniquement les champs sélectionnés présents dans la structure du schéma.

![Champs ajoutés](../../images/ui/resources/schemas/fields-added.png)

### Ajout de champs personnalisés aux groupes de champs {#add-fields}

Après avoir ajouté un groupe de champs à un schéma, vous pouvez définir des champs supplémentaires pour ce groupe. Cependant, tous les champs ajoutés à un groupe de champs dans un schéma apparaîtront également dans tous les autres schémas qui utilisent ce même groupe de champs.

En outre, si un champ personnalisé est ajouté à un groupe de champs standard, ce groupe sera converti en groupe de champs personnalisé et le groupe de champs standard d’origine ne sera plus disponible.

Si vous souhaitez ajouter un champ personnalisé à un groupe de champs standard, reportez-vous à la [section ci-dessous](#custom-fields-for-standard-groups) pour obtenir des instructions spécifiques. Si vous ajoutez des champs à un groupe de champs personnalisé, reportez-vous à la section sur la [modification des groupes de champs personnalisés](./field-groups.md) du guide de l’interface utilisateur des groupes de champs.

Si vous ne souhaitez modifier aucun groupe de champs existant, vous pouvez [créer un nouveau groupe de champs personnalisés](./field-groups.md#create) pour définir des champs supplémentaires à la place.

## Ajout de champs individuels à un schéma {#add-individual-fields}

L’éditeur de schémas vous permet d’ajouter des champs individuels directement à un schéma si vous souhaitez éviter d’ajouter un groupe de champs entier pour un cas d’utilisation spécifique. Vous pouvez [ajouter des champs individuels à partir de groupes de champs standard](#add-standard-fields) ou [ajouter vos propres champs personnalisés](#add-custom-fields) à la place.

>[!IMPORTANT]
>
>Même si l’éditeur de schémas permet fonctionnellement d’ajouter des champs individuels directement à un schéma, cela ne change pas le fait que tous les champs d’un schéma XDM doivent être fournis par sa classe ou un groupe de champs compatible avec cette classe. Comme les sections ci-dessous l’expliquent, tous les champs individuels sont toujours associés à une classe ou à un groupe de champs comme étape clé lorsqu’ils sont ajoutés à un schéma.

### Ajouter des champs standard {#add-standard-fields}

Vous pouvez ajouter directement à un schéma des champs provenant de groupes de champs standard sans avoir à connaître au préalable le groupe de champs correspondant. Pour ajouter un champ standard à un schéma, sélectionnez l’icône plus (**+**) en regard du nom du schéma dans la zone de travail. Un espace réservé **[!UICONTROL Champ sans titre]** apparaît dans la structure du schéma et le rail de droite est mis à jour pour afficher les commandes permettant de configurer le champ.

![Espace réservé du champ](../../images/ui/resources/schemas/root-custom-field.png)

Sous **[!UICONTROL Nom du champ]**, commencez à saisir le nom du champ que vous souhaitez ajouter. Le système recherche automatiquement les champs standard correspondant à la requête et les répertorie sous **[!UICONTROL Champs standard recommandés]**, y compris les groupes de champs auxquels ils appartiennent.

![Champs standard recommandés](../../images/ui/resources/schemas/standard-field-search.png)

Bien que certains champs standard portent le même nom, leur structure peut varier en fonction du groupe de champs d’où ils proviennent. Si un champ standard est imbriqué dans un objet parent dans la structure du groupe de champs, le champ parent sera également inclus dans le schéma si le champ enfant est ajouté.

Sélectionnez l’icône d’aperçu (![Icône Aperçu](/help/images/icons/preview.png)) en regard d’un champ standard pour afficher la structure de son groupe de champs et mieux comprendre comment il peut être imbriqué. Pour ajouter le champ standard au schéma, sélectionnez l’icône plus (![Icône Plus](/help/images/icons/add-circle.png)).

![Ajouter un champ standard](../../images/ui/resources/schemas/add-standard-field.png)

Le canevas se met à jour pour afficher le champ standard ajouté au schéma, y compris tous les champs parents sous lesquels il est imbriqué dans la structure du groupe de champs. Le nom du groupe de champs est également répertorié sous **[!UICONTROL Groupes de champs]** dans le rail de gauche. Si vous souhaitez ajouter d’autres champs du même groupe de champs, sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

![Champ standard ajouté](../../images/ui/resources/schemas/standard-field-added.png)

### Ajouter des champ personnalisés       {#add-custom-fields}

Tout comme le workflow pour les champs standard, vous pouvez également ajouter vos propres champs personnalisés directement à un schéma.

Pour ajouter des champs au niveau racine d’un schéma, sélectionnez l’icône plus (**+**) en regard du nom du schéma dans la zone de travail. Un espace réservé **[!UICONTROL Champ sans titre]** apparaît dans la structure du schéma et le rail de droite est mis à jour pour afficher les commandes permettant de configurer le champ.

![Champ personnalisé racine](../../images/ui/resources/schemas/root-custom-field.png)

Commencez à saisir le nom du champ que vous souhaitez ajouter, et le système commence automatiquement à rechercher les champs standards correspondants. Pour créer un champ personnalisé à la place, sélectionnez l’option supérieure ajoutée avec **([!UICONTROL Nouveau champ])**.

![Nouveau champ](../../images/ui/resources/schemas/custom-field-search.png)

Après avoir fourni un nom d’affichage et un type de données pour le champ, l’étape suivante consiste à attribuer le champ à une ressource XDM parente. Si votre schéma utilise une classe personnalisée, vous pouvez choisir d’[ajouter le champ à la classe affectée](#add-to-class) ou un [groupe de champs](#add-to-field-group) à la place. Cependant, si votre schéma utilise une classe standard, vous ne pouvez affecter le champ personnalisé qu’à un groupe de champs.

#### Affecter le champ à un groupe de champs personnalisé {#add-to-field-group}

>[!NOTE]
>
>Cette section décrit uniquement comment affecter le champ à un groupe de champs personnalisé. Si vous souhaitez étendre un groupe de champs standard avec le nouveau champ personnalisé à la place, reportez-vous à la section sur l’ [ajout de champs personnalisés aux groupes de champs standard](#custom-fields-for-standard-groups).

Sous **[!UICONTROL Attribuer à]**, sélectionnez **[!UICONTROL Groupe de champs]**. Si votre schéma utilise une classe standard, il s’agit de la seule option disponible et elle est sélectionnée par défaut.

Vous devez ensuite sélectionner un groupe de champs pour le nouveau champ à associer. Commencez à saisir le nom du groupe de champs dans la saisie de texte fournie. Si des groupes de champs personnalisés correspondent à l’entrée, ils s’affichent dans la liste déroulante. Vous pouvez également saisir un nom unique pour créer un groupe de champs.

![Sélectionner un groupe de champs](../../images/ui/resources/schemas/select-field-group.png)

>[!WARNING]
>
>Si vous sélectionnez un groupe de champs personnalisé existant, tout autre schéma qui l’emploie héritera également du nouveau champ ajouté après avoir enregistré vos modifications. Pour cette raison, sélectionnez un groupe de champs existant uniquement si vous souhaitez ce type de propagation. Dans le cas contraire, vous devez choisir de créer un groupe de champs personnalisé.

Après avoir sélectionné le groupe de champs dans la liste, sélectionnez **[!UICONTROL Appliquer]**.

![Appliquer le champ](../../images/ui/resources/schemas/apply-field.png)

Le nouveau champ est ajouté à la zone de travail et est un espace de noms situé sous votre [ID de tenant](../../api/getting-started.md#know-your-tenant_id) pour éviter les conflits avec les champs XDM standard. Le groupe de champs auquel vous avez associé le nouveau champ apparaît également sous **[!UICONTROL Groupes de champs]** dans le rail de gauche.

![ID de tenant](../../images/ui/resources/schemas/tenantId.png)

>[!NOTE]
>
>Les autres champs fournis par le groupe de champs personnalisé sélectionné sont supprimés du schéma par défaut. Si vous souhaitez ajouter certains de ces champs au schéma, sélectionnez un champ appartenant au groupe, puis sélectionnez **[!UICONTROL Gérer les champs associés]** dans le rail de droite.

#### Affectation du champ à une classe personnalisée {#add-to-class}

Sous **[!UICONTROL Attribuer à]**, sélectionnez **[!UICONTROL Classe]**. Le champ d’entrée ci-dessous est remplacé par le nom de la classe personnalisée du schéma actuel, indiquant que le nouveau champ sera affecté à cette classe.

![L’option [!UICONTROL Classe] sélectionnée pour la nouvelle affectation de champ.](../../images/ui/resources/schemas/assign-field-to-class.png)

Continuez à configurer le champ selon vos besoins et sélectionnez **[!UICONTROL Appliquer]** une fois terminé.

![[!UICONTROL Appliquer] sélectionné pour le nouveau champ.](../../images/ui/resources/schemas/assign-field-to-class-apply.png)

Le nouveau champ est ajouté à la zone de travail et est un espace de noms situé sous votre [ID de tenant](../../api/getting-started.md#know-your-tenant_id) pour éviter les conflits avec les champs XDM standard. Si vous sélectionnez le nom de la classe dans le rail de gauche, le nouveau champ s’affiche dans la structure de la classe.

![Le nouveau champ appliqué à la structure de la classe personnalisée, représenté dans la zone de travail.](../../images/ui/resources/schemas/assign-field-to-class-applied.png)

### Ajouter des champs personnalisés à la structure des groupes de champs standard {#custom-fields-for-standard-groups}

Si le schéma sur lequel vous travaillez comporte un champ de type objet fourni par un groupe de champs standard, vous pouvez ajouter vos propres champs personnalisés à cet objet standard.

>[!WARNING]
>
>Tous les champs ajoutés à un groupe de champs dans un schéma apparaîtront également dans tous les autres schémas qui utilisent ce même groupe de champs. En outre, si un champ personnalisé est ajouté à un groupe de champs standard, ce groupe sera converti en groupe de champs personnalisé et le groupe de champs standard d’origine ne sera plus disponible.
>
>Si vous avez participé à la version bêta de cette fonctionnalité, vous recevrez une boîte de dialogue vous informant des groupes de champs standard que vous avez précédemment personnalisés. Une fois que vous avez sélectionné **[!UICONTROL Accepter]**, les ressources répertoriées sont converties en groupes de champs personnalisés.
>
>![Boîte de dialogue de confirmation pour convertir des groupes de champs standard](../../images/ui/resources/schemas/beta-extension-confirmation.png)

Pour commencer, sélectionnez l’icône plus (**+**) en regard de la racine de l’objet fourni par le groupe de champs standard.

![Ajouter un champ à l’objet standard](../../images/ui/resources/schemas/add-field-to-standard-object.png)

Un message d’avertissement s’affiche, vous invitant à confirmer la conversion du groupe de champs standard. Sélectionnez **[!UICONTROL Continuer la création du groupe de champs]** pour continuer.

![Confirmer la conversion du groupe de champs](../../images/ui/resources/schemas/confirm-field-group-conversion.png)

Le canevas réapparaît avec un espace réservé sans titre pour le nouveau champ. Notez que le nom du groupe de champs standard a été ajouté à &quot;([!UICONTROL Extended])&quot; pour indiquer qu’il a été modifié à partir de la version d’origine. À partir de là, utilisez les commandes du rail de droite pour définir les propriétés du champ.

![Champ ajouté à l’objet standard](../../images/ui/resources/schemas/standard-field-group-converted.png)

Après avoir appliqué vos modifications, le nouveau champ s’affiche sous l’espace de noms de l’identifiant du client dans l’objet standard. Cet espace de noms imbriqué empêche les conflits de nom de champ dans le groupe de champs lui-même afin d’éviter de rompre les modifications dans d’autres schémas qui utilisent le même groupe de champs.

![Champ ajouté à l’objet standard](../../images/ui/resources/schemas/added-to-standard-object.png)

## Activer un schéma pour le profil client en temps réel {#profile}

>[!CONTEXTUALHELP]
>id="platform_schemas_enableforprofile"
>title="Activation d&#39;un schéma pour Profil"
>abstract="Lorsqu&#39;un schéma est activé pour Profil, tous les jeux de données créés à partir de ce schéma participent au profil client en temps réel, qui fusionne les données de différentes sources pour créer une vue complète de chaque client. Une fois qu&#39;un schéma est utilisé pour ingérer des données dans Profil, il ne peut pas être désactivé. Pour plus d&#39;informations, consultez la documentation."

[Real-Time Customer Profile](../../../profile/home.md) fusionne les données de sources disparates afin de construire une vue complète de chaque client. Si vous souhaitez que les données capturées par un schéma participent à ce processus, vous devez activer le schéma à utiliser dans [!DNL Profile].

>[!IMPORTANT]
>
>Pour activer un schéma pour [!DNL Profile], un champ d’identité principal doit être défini. Pour plus d’informations, consultez le guide sur la [définition des champs d’identité](../fields/identity.md) .

Pour activer le schéma, commencez par sélectionner le nom du schéma dans le rail de gauche, puis sélectionnez le bouton d’activation/désactivation **[!UICONTROL Profile]** dans le rail de droite.

![](../../images/ui/resources/schemas/profile-toggle.png)

Une fenêtre contextuelle s’affiche, vous avertissant qu’une fois qu’un schéma a été activé et enregistré, il ne peut pas être désactivé. Sélectionnez **[!UICONTROL Activer]** pour continuer.

![](../../images/ui/resources/schemas/profile-confirm.png)

Le canevas réapparaît avec le bouton bascule [!UICONTROL Profile] activé.

>[!IMPORTANT]
>
>Comme le schéma n’est pas encore enregistré, il s’agit d’un point de non-retour si vous changez d’avis concernant la possibilité de laisser le schéma participer à Real-Time Customer Profile : une fois que vous avez enregistré un schéma activé, il ne peut plus être désactivé. Sélectionnez à nouveau le bouton d’activation/désactivation **[!UICONTROL Profile]** pour désactiver le schéma.

Pour terminer le processus, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer le schéma.

![](../../images/ui/resources/schemas/profile-enabled.png)

Le schéma est désormais activé pour une utilisation dans Real-Time Customer Profile. Lorsque Platform ingère des données dans des jeux de données en fonction de ce schéma, ces données sont intégrées à vos données de profil fusionnées.

## Modification des noms d’affichage des champs de schéma {#display-names}

Une fois que vous avez affecté une classe et ajouté des groupes de champs à un schéma, vous pouvez modifier les noms d’affichage de l’un des champs du schéma, que ces champs aient été fournis par des ressources XDM standard ou personnalisées.

>[!NOTE]
>
>Gardez à l’esprit que les noms d’affichage des champs appartenant à des classes standard ou à des groupes de champs ne peuvent être modifiés que dans le contexte d’un schéma spécifique. En d’autres termes, la modification du nom d’affichage d’un champ standard dans un schéma n’affecte pas les autres schémas qui utilisent la même classe ou le même groupe de champs associé.
>
>Une fois que vous avez apporté des modifications aux noms d’affichage des champs d’un schéma, ces modifications sont immédiatement répercutées dans tous les jeux de données existants basés sur ce schéma.

Pour modifier le nom d’affichage d’un champ de schéma, sélectionnez le champ dans la zone de travail. Dans le rail de droite, indiquez le nouveau nom sous **[!UICONTROL Nom d’affichage]**.

![](../../images/ui/resources/schemas/display-name.png)

Sélectionnez **[!UICONTROL Appliquer]** dans le rail de droite et les mises à jour du canevas pour afficher le nouveau nom d’affichage du champ. Sélectionnez **[!UICONTROL Enregistrer]** pour appliquer les modifications au schéma.

![](../../images/ui/resources/schemas/display-name-changed.png)

## Modification de la classe d’un schéma {#change-class}

Vous pouvez modifier la classe d’un schéma à tout moment au cours du processus de composition initiale, avant que le schéma ne soit enregistré.

>[!WARNING]
>
>La réattribution de la classe d’un schéma doit être effectuée avec une extrême prudence. Les groupes de champs ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialisera la zone de travail et tous les champs que vous avez ajoutés.

Pour réaffecter une classe, sélectionnez **[!UICONTROL Attribuer]** dans la partie gauche du canevas.

![](../../images/ui/resources/schemas/assign-class-button.png)

Une boîte de dialogue s’affiche, qui affiche une liste de toutes les classes disponibles, y compris toutes celles définies par votre organisation (le propriétaire étant &quot;[!UICONTROL Customer]&quot;) ainsi que les classes standard définies par l’Adobe.

Sélectionnez une classe dans la liste pour afficher sa description sur le côté droit de la boîte de dialogue. Vous pouvez également sélectionner **[!UICONTROL Preview class structure]** pour afficher les champs et les métadonnées associés à la classe. Sélectionnez **[!UICONTROL Attribuer la classe]** pour continuer.

![](../../images/ui/resources/schemas/assign-class.png)

Une nouvelle boîte de dialogue s’ouvre, vous demandant de confirmer que vous souhaitez attribuer une nouvelle classe. Sélectionnez **[!UICONTROL Attribuer]** pour confirmer.

![](../../images/ui/resources/schemas/assign-confirm.png)

Après avoir confirmé la modification de classe, le canevas est réinitialisé et toute progression de la composition est perdue.

## Étapes suivantes {#next-steps}

Ce document couvrait les principes de base de la création et de la modification de schémas dans l’interface utilisateur de Platform. Il est vivement recommandé de consulter le [tutoriel de création de schéma](../../tutorials/create-schema-ui.md) pour obtenir un processus complet de création d’un schéma complet dans l’interface utilisateur, y compris la création de groupes de champs personnalisés et de types de données pour des cas d’utilisation uniques.

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

Pour savoir comment gérer les schémas dans l’API [!DNL Schema Registry], consultez le [guide de point d’entrée des schémas](../../api/schemas.md).

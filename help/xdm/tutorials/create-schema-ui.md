---
keywords: Experience Platform;accueil;rubriques populaires;ui;IU;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;éditeur de schémas;éditeur de schémas;schéma;schémas;schémas;schémas;créer
solution: Experience Platform
title: Création d’un schéma à l’aide de l’éditeur de schémas
topic-legacy: tutorial
type: Tutorial
description: Ce tutoriel décrit les étapes de création d’un schéma à l’aide de l’éditeur de schémas d’Experience Platform.
exl-id: 3edeb879-3ce4-4adb-a0bd-8d7ad2ec6102
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '3754'
ht-degree: 12%

---

# Créez un schéma à l’aide du [!DNL Schema Editor]

L’interface utilisateur de Adobe Experience Platform vous permet de créer et de gérer des [!DNL Experience Data Model] Schémas (XDM) dans une zone de travail visuelle interactive appelée [!DNL Schema Editor]. Ce tutoriel explique comment créer un schéma à l’aide du [!DNL Schema Editor].

>[!NOTE]
>
>À des fins de démonstration, les étapes de ce tutoriel impliquent la création d’un exemple de schéma qui décrit les membres d’un programme de fidélité des clients. Bien que vous puissiez utiliser ces étapes pour créer un schéma différent à vos propres fins, il est recommandé de suivre d’abord la création de l’exemple de schéma pour découvrir les fonctionnalités de [!DNL Schema Editor].

Si vous préférez composer un schéma à l’aide de la méthode [!DNL Schema Registry] à la place, commencez par lire la variable [[!DNL Schema Registry] guide de développement](../api/getting-started.md) avant de lancer le tutoriel sur [création d’un schéma à l’aide de l’API](create-schema-api.md).

## Prise en main

Ce tutoriel nécessite une compréhension pratique des différents aspects de Adobe Experience Platform impliqués dans la création de schémas. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux concepts suivants :

* [[!DNL Experience Data Model (XDM)]](../home.md) : cadre normalisé selon lequel [!DNL Platform] organise les données de l’expérience client.
   * [Principes de base de la composition des schémas](../schema/composition.md): Présentation des schémas XDM et de leurs blocs de création, notamment les classes, les groupes de champs de schéma, les types de données et les champs individuels.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md) : fournit un profil de consommateur unifié en temps réel, basé sur des données agrégées provenant de plusieurs sources.

## Ouvrez le [!UICONTROL Schémas] workspace {#browse}

Le [!UICONTROL Schémas] de l’espace de travail [!DNL Platform] L’interface utilisateur d’ offre une visualisation de la [!DNL Schema Library], ce qui vous permet d’afficher la gestion des schémas disponibles pour votre organisation. L’espace de travail comprend également la fonction [!DNL Schema Editor], le canevas sur lequel vous pouvez composer un schéma tout au long de ce tutoriel.

Après vous être connecté à [!DNL Experience Platform], sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir la **[!UICONTROL Schémas]** workspace. Le **[!UICONTROL Parcourir]** affiche une liste des schémas (une représentation de la fonction [!DNL Schema Library]) que vous pouvez afficher et personnaliser. La liste comprend le nom, le type, la classe et le comportement (enregistrement ou série chronologique) sur lesquels repose le schéma, ainsi que la date et l’heure de la dernière modification du schéma.

Consultez le guide sur la [exploration des ressources XDM existantes dans l’interface utilisateur](../ui/explore.md) pour plus d’informations.

## Création et attribution d’un nom à un schéma {#create}

Pour commencer à composer un schéma, sélectionnez **[!UICONTROL Créer un schéma]** dans le coin supérieur droit du **[!UICONTROL Schémas]** workspace. Un menu déroulant s’affiche, vous permettant de choisir entre les classes principales. [!UICONTROL XDM Individual Profile] et [!UICONTROL XDM ExperienceEvent]. Si ces classes ne répondent pas à vos besoins, vous pouvez également sélectionner **[!UICONTROL Parcourir]** pour effectuer un choix parmi d’autres classes disponibles ou [créer une classe](#create-new-class).

Pour les besoins de ce tutoriel, sélectionnez **[!UICONTROL XDM Individual Profile]**.

![](../images/tutorials/create-schema/create_schema_button.png)

Puisque vous avez choisi une classe XDM standard sur laquelle baser le schéma, la variable **[!UICONTROL Ajouter un groupe de champs]** s’affiche, ce qui vous permet de commencer immédiatement à ajouter des champs au schéma. Pour l’instant, sélectionnez **[!UICONTROL Annuler]** pour quitter la boîte de dialogue.

![](../images/tutorials/create-schema/cancel-field-group.png)

Le [!DNL Schema Editor] apparaît. C’est le canevas sur lequel vous allez composer votre schéma. Un schéma sans titre est automatiquement créé dans la variable **[!UICONTROL Structure]** de la zone de travail lorsque vous arrivez dans l’éditeur, avec les champs standard inclus dans tous les schémas en fonction de cette classe. La classe affectée pour le schéma est également répertoriée sous **[!UICONTROL Classe]** in **[!UICONTROL Composition]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Vous pouvez [modifier la classe d’un schéma](#change-class) à tout moment au cours du processus de composition initial avant que le schéma ne soit enregistré, mais cela doit être fait avec la plus grande prudence. Les groupes de champs ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialise le canevas et les champs que vous avez ajoutés.

Utilisez les champs situés à droite de l’éditeur pour fournir un nom d’affichage et une description facultative du schéma. Une fois qu’un nom est saisi, le canevas se met à jour pour tenir compte du nouveau nom du schéma.

![](../images/tutorials/create-schema/name_schema.png)

Plusieurs éléments importants doivent être pris en compte lors du choix d’un nom pour votre schéma :

* Les noms des schémas doivent être courts et descriptifs afin que le schéma puisse être facilement retrouvé ultérieurement.
* Le nom d’un schéma doit être unique, ce qui signifie qu’il doit également être suffisamment précis pour ne pas être réutilisé à l’avenir. Par exemple, si votre organisation dispose de programmes de fidélité distincts pour différentes marques, nous vous conseillons de nommer votre schéma « Brand A Loyalty Members » pour faciliter la distinction avec d’autres schémas relatifs à la fidélité que vous pourriez définir ultérieurement.
* Vous pouvez également utiliser la description du schéma pour fournir toute information contextuelle supplémentaire concernant le schéma.

Ce tutoriel compose un schéma pour ingérer des données relatives aux membres d’un programme de fidélité. Par conséquent, le schéma est appelé &quot;Loyalty Members&quot;.

## Ajouter un groupe de champs {#field-group}

Vous pouvez maintenant commencer à ajouter des champs à votre schéma en ajoutant des groupes de champs. Un groupe de champs est un groupe d’un ou de plusieurs champs souvent utilisés conjointement pour décrire un concept particulier. Ce tutoriel utilise des groupes de champs pour décrire les membres du programme de fidélité et recueillir des informations clés telles que le nom, l’anniversaire, le numéro de téléphone, l’adresse, etc.

Pour ajouter un groupe de champs, sélectionnez **[!UICONTROL Ajouter]** dans le **[!UICONTROL Groupes de champs]** sous-section .

![](../images/tutorials/create-schema/add-field-group-button.png)

Une nouvelle boîte de dialogue s’affiche, affichant une liste des groupes de champs disponibles. Chaque groupe de champs est destiné uniquement à une utilisation avec une classe spécifique. Par conséquent, la boîte de dialogue répertorie uniquement les groupes de champs compatibles avec la classe que vous avez sélectionnée (dans ce cas, la variable [!DNL XDM Individual Profile] ). Si vous utilisez une classe XDM standard, la liste des groupes de champs sera triée intelligemment en fonction de la popularité de l’utilisation.

![](../images/tutorials/create-schema/field-group-popularity.png)

Si vous sélectionnez un groupe de champs dans la liste, il s’affiche dans le rail de droite. Vous pouvez sélectionner plusieurs groupes de champs si vous le souhaitez, en ajoutant chacun d’eux à la liste dans le rail de droite avant de le confirmer. En outre, une icône s’affiche sur le côté droit du groupe de champs actuellement sélectionné, ce qui permet de prévisualiser la structure des champs qu’il fournit.

![](../images/tutorials/create-schema/preview-field-group-button.png)

Lors de la prévisualisation d’un groupe de champs, une description détaillée du schéma du groupe de champs est fournie dans le rail droit. Vous pouvez également parcourir les champs du groupe de champs dans la zone de travail fournie. Lorsque vous sélectionnez différents champs, le rail de droite se met à jour pour afficher les détails du champ en question. Sélectionner **[!UICONTROL Précédent]** lorsque vous avez terminé la prévisualisation, revenez à la boîte de dialogue de sélection du groupe de champs.

![](../images/tutorials/create-schema/preview-field-group.png)

Pour ce tutoriel, sélectionnez la variable **[!UICONTROL Détails démographiques]** groupe de champs, puis sélectionnez **[!UICONTROL Ajouter un groupe de champs]**.

![](../images/tutorials/create-schema/demographic-details.png)

Le canevas du schéma réapparaît. Le **[!UICONTROL Groupes de champs]** La section répertorie désormais &quot;[!UICONTROL Détails démographiques]&quot; et la variable **[!UICONTROL Structure]** inclut les champs fournis par le groupe de champs. Vous pouvez sélectionner le nom du groupe de champs sous le champ **[!UICONTROL Groupes de champs]** pour mettre en surbrillance les champs spécifiques qu’il fournit dans la zone de travail.

![](../images/tutorials/create-schema/demographic-details-structure.png)

Ce groupe de champs met à disposition plusieurs champs sous le nom de niveau supérieur. `person` avec le type de données &quot;[!UICONTROL Personne]&quot;. Ce groupe de champs décrit les informations sur un individu, notamment son nom, sa date de naissance et son genre.

>[!NOTE]
>
>N’oubliez pas que les champs peuvent utiliser des types scalaires (chaîne, entier, tableau ou date, par exemple), ainsi que tout type de données (un groupe de champs représentant un concept commun) défini dans la variable [!DNL Schema Registry].

Notez que la variable `name` a un type de données &quot;[!UICONTROL Nom de la personne]&quot;, ce qui signifie qu’il décrit également un concept commun et contient des sous-champs liés au nom, tels que le prénom, le nom, le titre de politesse et le suffixe.

Sélectionnez les différents champs de la zone de travail pour afficher les champs supplémentaires qui contribuent à la structure du schéma.

## Ajouter un autre groupe de champs {#field-group-2}

Vous pouvez maintenant répéter les mêmes étapes pour ajouter un autre groupe de champs. Lorsque vous affichez la variable **[!UICONTROL Ajouter un groupe de champs]** cette fois, notez que le[!UICONTROL Détails démographiques]&quot;a été grisé et la case à cocher à côté ne peut pas être sélectionnée. Cela vous évite de dupliquer accidentellement des groupes de champs que vous avez déjà inclus dans le schéma actuel.

Pour ce tutoriel, sélectionnez le[!DNL Personal Contact Details]&quot; groupe de champs dans la boîte de dialogue, puis sélectionnez **[!UICONTROL Ajouter un groupe de champs]** pour l’ajouter au schéma.

![](../images/tutorials/create-schema/personal-contact-details.png)

Une fois ajouté, le canevas réapparaît. &quot;[!UICONTROL Détails du contact personnel]&quot; est désormais répertorié sous **[!UICONTROL Groupes de champs]** dans le **[!UICONTROL Composition]** Les champs et pour l’adresse du domicile, le téléphone mobile, etc. ont été ajoutés sous **[!UICONTROL Structure]**.

Semblable au `name` , les champs que vous venez d’ajouter représentent des concepts à plusieurs champs. Par exemple : `homeAddress` possède un type de données &quot;[!UICONTROL Adresse postale]&quot; et `mobilePhone` possède un type de données &quot;[!UICONTROL Numéro de téléphone]&quot;. Vous pouvez sélectionner chacun de ces champs pour les développer et afficher les champs supplémentaires inclus dans le type de données.

![](../images/tutorials/create-schema/personal-contact-details-structure.png)

## Définition d’un groupe de champs personnalisé {#define-field-group}

Le &quot;[!UICONTROL Loyalty Members]&quot;est destiné à capturer des données relatives aux membres d’un programme de fidélité. Il nécessite donc des champs spécifiques liés à la fidélité.

Il existe un standard [!UICONTROL Détails de fidélité] groupe de champs que vous pouvez ajouter au schéma pour capturer des champs communs liés à un programme de fidélité. Bien qu’il soit vivement conseillé d’utiliser des groupes de champs standard pour représenter les concepts capturés par vos schémas, la structure du groupe de champs de fidélité standard peut ne pas être en mesure de capturer toutes les données pertinentes pour votre programme de fidélité spécifique. Dans ce scénario, vous pouvez choisir de définir un nouveau groupe de champs personnalisé pour capturer ces champs à la place.

Ouvrez le **[!UICONTROL Ajouter un groupe de champs]** à nouveau, mais cette fois, sélectionnez **[!UICONTROL Créer un groupe de champs]** près du sommet. Vous êtes alors invité à fournir un nom d’affichage et une description pour votre groupe de champs.

![](../images/tutorials/create-schema/create-new-field-group.png)

Comme pour les noms de classe, le nom du groupe de champs doit être court et simple, décrivant ce que le groupe de champs va apporter au schéma. Ces noms sont également uniques. Vous ne pourrez donc pas réutiliser le nom et devrez donc veiller à ce qu’il soit suffisamment spécifique.

Pour ce tutoriel, nommez le nouveau groupe de champs &quot;Loyalty Details&quot;.

Sélectionner **[!UICONTROL Ajouter un groupe de champs]** pour revenir au [!DNL Schema Editor]. &quot;[!UICONTROL Détails de fidélité]&quot; devrait maintenant apparaître sous **[!UICONTROL Groupes de champs]** sur le côté gauche du canevas, mais aucun champ n’y est encore associé et aucun nouveau champ n’apparaît donc sous **[!UICONTROL Structure]**.

## Ajouter des champs au groupe de champs {#field-group-fields}

Maintenant que vous avez créé le groupe de champs &quot;Loyalty Details&quot;, il est temps de définir les champs que le groupe de champs va ajouter au schéma.

Pour commencer, sélectionnez le nom du groupe de champs dans le **[!UICONTROL Groupes de champs]** . Une fois que vous avez effectué cette opération, les propriétés du groupe de champs s’affichent sur le côté droit de l’éditeur et un **plus (+)** s’affiche en regard du nom du schéma sous **[!UICONTROL Structure]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Sélectionnez la **plus (+)** en regard de &quot;[!DNL Loyalty Members]&quot; pour créer un noeud dans la structure. Ce noeud (appelé `_tenantId` dans cet exemple) représente l’identifiant du client de votre organisation IMS, précédé d’un trait de soulignement. La présence de l’identifiant du client indique que les champs que vous ajoutez sont contenus dans l’espace de noms de votre organisation.

En d’autres termes, les champs que vous ajoutez sont propres à votre organisation et vont être enregistrés dans la variable [!DNL Schema Registry] dans une zone spécifique accessible uniquement à votre entreprise. Les champs que vous définissez doivent toujours être ajoutés à votre espace de noms client pour empêcher les collisions avec des noms provenant d’autres classes, groupes de champs, types de données et champs standard.

Dans ce noeud, l’espace de noms est un &quot;[!UICONTROL Nouveau champ]&quot;. C’est le début du &quot;[!UICONTROL Détails de fidélité]&quot;.

![](../images/tutorials/create-schema/new_field_loyalty.png)

En utilisant les contrôles sur le côté droit de l&#39;éditeur, commencez par créer une `loyalty` champ de type &quot;[!UICONTROL Objet]&quot; qui sera utilisé pour contenir vos champs liés à la fidélité. Lorsque vous avez terminé, sélectionnez **[!UICONTROL Appliquer]**.

![](../images/tutorials/create-schema/loyalty_object.png)

Les modifications sont appliquées et le `loyalty` s’affiche. Sélectionnez la **plus (+)** en regard de l’objet pour ajouter des champs supplémentaires liés à la fidélité. Un &quot;[!UICONTROL Nouveau champ]&quot; apparaît et la variable **[!UICONTROL Propriétés du champ]** est visible sur le côté droit de la zone de travail.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Chaque champ nécessite les informations suivantes :

* **[!UICONTROL Nom du champ]:** Nom du champ, écrit en majuscules. Exemple : loyaltyLevel
* **[!UICONTROL Nom d’affichage]:** Nom du champ, écrit en majuscules de titre. Exemple : Loyalty Level
* **[!UICONTROL Type]:** Type de données du champ. Cela inclut les types scalaires de base et tous les types de données définis dans la variable [!DNL Schema Registry]. Exemples : [!UICONTROL Chaîne], [!UICONTROL Entier], [!UICONTROL Booléen], [!UICONTROL Personne], [!UICONTROL Adresse], [!UICONTROL Numéro de téléphone], etc.
* **[!UICONTROL Description]:** Une description facultative du champ doit être incluse, écrite en majuscules, avec un maximum de 200 caractères.

Le premier champ de la variable `Loyalty` sera une chaîne appelée `loyaltyId`. Lorsque vous définissez le type du nouveau champ sur &quot;[!UICONTROL Chaîne]&quot;, la variable **[!UICONTROL Propriétés du champ]** est renseignée avec plusieurs options permettant d’appliquer des contraintes, notamment la valeur par défaut, le format et la longueur maximale.

![](../images/tutorials/create-schema/string_constraints.png)

Différentes options de contraintes sont disponibles selon le type de données sélectionné. Depuis `loyaltyId` sera une adresse électronique, sélectionnez &quot;[!UICONTROL email]&quot; de la **[!UICONTROL Format]** menu déroulant. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer vos modifications.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Ajouter d’autres champs au groupe de champs {#field-group-fields-2}

Maintenant que vous avez ajouté la variable `loyaltyId` , vous pouvez ajouter des champs supplémentaires pour capturer des informations relatives à la fidélité, telles que :

* Points (entier)
* Member-since (date)

Pour ajouter chaque champ au schéma, sélectionnez l’option **plus (+)** en regard de l’icône `loyalty` et renseignez les informations requises.

Une fois l’opération terminée, l’objet Loyalty contient des champs pour l’identifiant de fidélité, les points et le membre depuis.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Ajouter un champ d’énumération au groupe de champs {#enum}

Lors de la définition de champs dans la variable [!DNL Schema Editor], vous pouvez appliquer d’autres options aux types de champ de base afin de fournir des contraintes supplémentaires sur les données que le champ peut contenir. Les cas d’utilisation de ces contraintes sont expliqués dans le tableau suivant :

| Contrainte | Description |
| --- | --- |
| [!UICONTROL Obligatoire] | Indique que le champ est requis pour l’ingestion des données. Toute donnée chargée dans un ensemble de données basé sur ce schéma qui ne contient pas ce champ sera défaillante lors de l’ingestion. |
| [!UICONTROL Tableau] | Indique que le champ contient un tableau de valeurs, chacune avec le type de données spécifié. Par exemple, l’utilisation de cette contrainte sur un champ avec un type de données &quot;[!UICONTROL Chaîne]&quot; indique que le champ contiendra un tableau de chaînes. |
| [!UICONTROL Énumération] | Indique que ce champ doit contenir l’une des valeurs d’une liste énumérée de valeurs possibles. |
| [!UICONTROL Identité] | Indique que ce champ est un champ d’identité. Vous trouverez plus d’informations sur les champs d’identité [dans la suite de ce tutoriel](#identity-field). |
| [!UICONTROL Relation] | Bien que les relations de schéma puissent être déduites par l’utilisation du schéma d’union et [!DNL Real-Time Customer Profile], cela s’applique uniquement aux schémas qui partagent la même classe. Le [!UICONTROL Relation] La contrainte indique que ce champ fait référence à l’identité Principale d’un schéma basée sur une classe différente, ce qui implique une relation entre les deux schémas. Voir le tutoriel sur [définition d’une relation](./relationship-ui.md) pour plus d’informations. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Les champs obligatoires, d’identité ou de relation s’affichent dans le rail de gauche, ce qui vous permet de localiser facilement ces champs, quelle que soit la complexité du schéma.
>
>![](../images/tutorials/create-schema/left-rail-special.png)

Pour ce tutoriel, la variable [!DNL "loyalty"] dans le schéma nécessite un nouveau champ d’énumération qui décrit le &quot;niveau de fidélité&quot; d’un client, où la valeur ne peut être que l’une des quatre options possibles. Pour ajouter ce champ au schéma, sélectionnez l’option **plus (+)** en regard de l’icône `loyalty` et remplissez les champs requis pour **[!UICONTROL Nom du champ]** et **[!UICONTROL Nom d’affichage]**. Pour **[!UICONTROL Type]**, sélectionnez &quot;[!UICONTROL Chaîne]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

D’autres cases à cocher s’affichent pour le champ une fois son type sélectionné, y compris les cases à cocher pour **[!UICONTROL Tableau]**, **[!UICONTROL Enum]**, et **[!UICONTROL Identité]**.

Sélectionnez la **[!UICONTROL Enum]** pour ouvrir la **[!UICONTROL Valeurs d’énumération]** ci-dessous. Ici, vous pouvez saisir la **[!UICONTROL valeur]** (en Camel Case) et le **[!UICONTROL libellé]** (nom facultatif et facile à lire écrit en Title Case) pour chaque niveau de fidélité acceptable.

Une fois toutes les propriétés de champ renseignées, sélectionnez **[!UICONTROL Appliquer]** pour ajouter le[!DNL loyaltyLevel]&quot; au champ `loyalty` .

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversion d’un objet à plusieurs champs en un type de données {#datatype}

Le `loyalty` contient désormais plusieurs champs spécifiques à la fidélité et représente une structure de données commune qui peut s’avérer utile dans d’autres schémas. Le [!DNL Schema Editor] permet d’appliquer facilement des objets à champs multiples réutilisables en convertissant la structure de ces objets en types de données.

Les types de données permettent l’utilisation cohérente de structures à champs multiples et offrent plus de flexibilité qu’un groupe de champs, car ils peuvent être utilisés n’importe où dans un schéma. Pour ce faire, définissez la variable **[!UICONTROL Type]** à celle de tout type de données défini dans la variable [!DNL Schema Registry].

Pour convertir la variable `loyalty` pour un type de données, sélectionnez l’objet `loyalty` champ sous **[!UICONTROL Structure]**, puis sélectionnez **[!UICONTROL Convertir en nouveau type de données]** sur le côté droit de l’éditeur sous **[!UICONTROL Propriétés du champ]**. Une fenêtre contextuelle verte s’affiche, confirmant que la conversion de l’objet a réussi.

![](../images/tutorials/create-schema/convert-data-type.png)

Maintenant, quand vous regardez sous le nez **[!UICONTROL Structure]**, vous pouvez voir que la variable `loyalty` a un type de données &quot;[!DNL Loyalty]&quot; et les champs comportent de petites icônes de verrouillage, indiquant qu’ils ne sont plus des champs individuels, mais qu’ils appartiennent plutôt à un type de données à plusieurs champs.

![](../images/tutorials/create-schema/loyalty_data_type.png)

Dans un prochain schéma, vous pourrez désormais attribuer un champ sous la forme &quot;[!DNL Loyalty]&quot; et il inclurait automatiquement des champs pour l’ID, le niveau de fidélité, le membre depuis et les points.

>[!NOTE]
>
>Vous pouvez également créer et modifier des types de données personnalisés indépendamment de la modification des schémas. Consultez le guide sur la [création et modification des types de données](../ui/resources/data-types.md) pour plus d’informations.

## Recherche et filtrage des champs de schéma

Votre schéma contient désormais plusieurs groupes de champs en plus des champs fournis par sa classe de base. Lorsque vous utilisez des schémas plus volumineux, vous pouvez cocher les cases en regard des noms des groupes de champs dans le rail de gauche pour filtrer les champs affichés uniquement par rapport aux groupes de champs qui vous intéressent.

![](../images/tutorials/create-schema/filter-by-field-group.png)

Si vous recherchez un champ spécifique dans votre schéma, vous pouvez également utiliser la barre de recherche pour filtrer les champs affichés par nom, quel que soit le groupe de champs sous lequel ils sont fournis.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La fonction de recherche prend en compte les filtres de groupe de champs sélectionnés lors de l’affichage des champs correspondants. Si une requête de recherche n’affiche pas les résultats attendus, vous devrez peut-être vérifier deux fois que vous ne filtrez aucun groupe de champs approprié.

## Définition d’un champ de schéma comme champ d’identité {#identity-field}

La structure de données standard fournie par les schémas peut être utilisée pour identifier les données appartenant à la même personne sur plusieurs sources, ce qui permet d’utiliser divers cas d’utilisation en aval, tels que la segmentation, la création de rapports, l’analyse de la science des données, etc. Pour regrouper des données en fonction d’identités individuelles, les champs clés doivent être marqués comme [!UICONTROL Identité] dans les schémas applicables.

[!DNL Experience Platform] permet de désigner facilement un champ d’identité à l’aide d’une **[!UICONTROL Identité]** dans la [!DNL Schema Editor]. Cependant, vous devez déterminer quel champ est le meilleur candidat à utiliser comme identité, en fonction de la nature de vos données.

Par exemple, il peut y avoir des milliers de membres du programme de fidélité appartenant au même &quot;niveau de fidélité&quot;, mais chaque membre du programme de fidélité a une `loyaltyId` (qui, dans ce cas, est l’adresse électronique du membre individuel). Le fait que `loyaltyId` est un identifiant unique pour chaque membre qui en fait un bon candidat pour un champ d’identité, tandis que `loyaltyLevel` ne l’est pas.

>[!IMPORTANT]
>
>Les étapes décrites ci-dessous expliquent comment ajouter un descripteur d’identité à un champ de schéma existant. Au lieu de définir des champs d’identité dans la structure du schéma lui-même, vous pouvez également utiliser une `identityMap` pour contenir des informations d’identité.
>
>Si vous envisagez d’utiliser `identityMap`, gardez à l’esprit qu’il remplacera toute identité Principale que vous ajoutez directement au schéma. Voir la section sur `identityMap` dans le [principes de base du guide de composition de schémas](../schema/composition.md#identityMap) pour plus d’informations.

Dans le **[!UICONTROL Structure]** de l’éditeur, sélectionnez l’option `loyaltyId` et le champ **[!UICONTROL Identité]** la case à cocher apparaît sous **[!UICONTROL Propriétés du champ]**. Cochez la case et sélectionnez l’option permettant de définir cette valeur comme **[!UICONTROL Identité Principal]** apparaît. Cochez également cette case.

>[!NOTE]
>
>Chaque schéma ne peut contenir qu’un seul champ d’identité principal. Une fois qu’un champ de schéma a été défini comme identité Principale, vous recevrez un message d’erreur si vous tentez par la suite de définir un autre champ d’identité dans le schéma comme Principal.

Ensuite, vous devez fournir un **[!UICONTROL Espace de noms d’identité]** dans la liste des espaces de noms prédéfinis dans la liste déroulante. Depuis `loyaltyId` est l’adresse électronique du client, sélectionnez &quot;[!UICONTROL Email]&quot; dans la liste déroulante. Sélectionner **[!UICONTROL Appliquer]** pour confirmer les mises à jour de la variable `loyaltyId` champ .

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Pour obtenir la liste des espaces de noms standard et leurs définitions, voir [[!DNL Identity Service] documentation](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Après application de la modification, l’icône pour `loyaltyId` affiche un symbole d’empreinte digitale, indiquant qu’il s’agit désormais d’un champ d’identité.

![](../images/tutorials/create-schema/identity-applied.png)

Désormais, toutes les données ingérées dans la variable `loyaltyId` sera utilisé pour aider à identifier cet individu et à assembler une vue unique de ce client. Pour en savoir plus sur l’utilisation des identités dans [!DNL Experience Platform], veuillez consulter la section [[!DNL Identity Service]](../../identity-service/home.md) documentation.

## Activation du schéma à utiliser dans [!DNL Real-Time Customer Profile] {#profile}

[[!DNL Real-Time Customer Profile]](../../profile/home.md) tire parti des données d’identité dans [!DNL Experience Platform] afin de fournir une vue d’ensemble de chaque client. Le service crée des profils robustes de 360° d’attributs du client, ainsi que des comptes horodatés de chaque interaction que les clients ont eue avec n’importe quel système intégré à [!DNL Experience Platform].

Pour qu’un schéma puisse être utilisé avec [!DNL Real-Time Customer Profile], une identité Principale doit être définie pour celui-ci. Vous recevrez un message d’erreur si vous tentez d’activer un schéma sans d’abord définir une identité Principale.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

Pour activer le schéma &quot;Loyalty Members&quot; à utiliser dans [!DNL Profile], commencez par sélectionner &quot;[!DNL Loyalty Members]&quot; dans la variable **[!UICONTROL Structure]** de l’éditeur.

Dans la partie droite de l’éditeur, des informations sur le schéma sont affichées, notamment son nom d’affichage, sa description et son type. Outre ces informations, il existe une **[!UICONTROL Profil]** bouton bascule .

![](../images/tutorials/create-schema/profile-toggle.png)

Sélectionner **[!UICONTROL Profil]** et une fenêtre contextuelle s’affiche, vous demandant de confirmer que vous souhaitez activer le schéma pour [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Une fois qu’un schéma a été activé pour [!DNL Real-Time Customer Profile] et enregistré, il ne peut pas être désactivé.

Sélectionner **[!UICONTROL Activer]** pour confirmer votre choix. Vous pouvez sélectionner la variable **[!UICONTROL Profil]** basculez à nouveau pour désactiver le schéma si vous le souhaitez, mais une fois le schéma enregistré pendant [!DNL Profile] est activée, elle ne peut plus être désactivée.

## Étapes suivantes et ressources supplémentaires

Maintenant que vous avez fini de composer le schéma, vous pouvez voir le schéma complet dans la zone de travail. Sélectionner **[!UICONTROL Enregistrer]** et le schéma sera enregistré dans la variable [!DNL Schema Library], en le rendant accessible par le [!DNL Schema Registry].

Votre nouveau schéma peut maintenant être utilisé pour ingérer des données dans [!DNL Platform]. Pour rappel, une fois que le schéma a été utilisé pour ingérer des données, seules des modifications additives peuvent être apportées. Reportez-vous aux [principes de base de la composition des schémas](../schema/composition.md) pour plus d’informations sur le contrôle de version des schémas.

Vous pouvez maintenant suivre le tutoriel sur [définition d’une relation de schéma dans l’interface utilisateur](./relationship-ui.md) pour ajouter un nouveau champ de relation au schéma &quot;Loyalty Members&quot;.

Le schéma &quot;Loyalty Members&quot; peut également être visualisé et géré à l’aide de la variable [!DNL Schema Registry] API. Pour commencer à utiliser l’API, lisez d’abord le [[!DNL Schema Registry API] guide de développement](../api/getting-started.md).

### Ressources vidéo

>[!WARNING]
>
>Le [!DNL Platform] L’interface utilisateur affichée dans les vidéos suivantes est obsolète. Consultez la documentation pour découvrir les dernières captures dʼécran et fonctionnalités de lʼinterface utilisateur.

La vidéo suivante montre comment créer un schéma simple dans le [!DNL Platform] Interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

La vidéo suivante est destinée à vous aider à mieux comprendre l’utilisation des groupes et classes de terrain.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Annexe

Les sections suivantes apportent des informations supplémentaires sur l’utilisation de la variable [!DNL Schema Editor].

### Création d’une nouvelle classe {#create-new-class}

[!DNL Experience Platform] offre la possibilité de définir un schéma basé sur une classe propre à votre organisation. Pour savoir comment créer une classe, consultez le guide sur [création et modification de classes dans l’interface utilisateur](../ui/resources/classes.md#create).

### Modification de la classe d’un schéma {#change-class}

Vous pouvez modifier la classe d’un schéma à tout moment pendant le processus de composition initial avant l’enregistrement du schéma.

>[!WARNING]
>
>La réattribution de la classe pour un schéma doit être effectuée avec une extrême prudence. Les groupes de champs ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialise le canevas et les champs que vous avez ajoutés.

Pour savoir comment modifier la classe d’un schéma, consultez le guide sur [gestion des schémas dans l’interface utilisateur](../ui/resources/schemas.md).

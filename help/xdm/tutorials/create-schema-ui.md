---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create
solution: Experience Platform
title: Création d’un schéma à l’aide de l’éditeur de schémas
topic: tutorials
description: Ce tutoriel décrit les étapes de création d’un schéma à l’aide de l’éditeur de schémas d’Experience Platform.
translation-type: tm+mt
source-git-commit: f0d3aad649fa550443db0fc5168c848ae85fb459
workflow-type: tm+mt
source-wordcount: '3835'
ht-degree: 17%

---


# Créez un schéma à l’aide de la variable [!DNL Schema Editor]

L’interface utilisateur de Adobe Experience Platform vous permet de créer et de gérer [!DNL Experience Data Model] (XDM) des schémas dans une trame visuelle interactive appelée le [!DNL Schema Editor]. Ce didacticiel explique comment créer un schéma à l’aide du [!DNL Schema Editor].

>[!NOTE]
>
>À des fins de démonstration, les étapes de ce didacticiel impliquent la création d’un exemple de schéma décrivant les membres d’un programme de fidélité de la clientèle. Bien que vous puissiez utiliser ces étapes pour créer un schéma différent à vos propres fins, il est recommandé de commencer par créer l’exemple de schéma pour découvrir les fonctionnalités du [!DNL Schema Editor].

If you prefer to compose a schema using the [!DNL Schema Registry] API instead, start by reading the [[!DNL Schema Registry] developer guide](../api/getting-started.md) before attempting the tutorial on [creating a schema using the API](create-schema-api.md).

## Prise en main

Ce tutoriel exige une compréhension pratique des différents aspects de Adobe Experience Platform impliqués dans la création de schémas. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux concepts suivants :

* [[ ! Modèle de données d’expérience DNL (XDM)]](../home.md): Cadre normalisé selon lequel [!DNL Platform] organiser les données d’expérience client.
   * [Principes de base de la composition des schémas](../schema/composition.md) : présentation des schémas XDM et de leurs blocs de création, notamment les classes, les mixins, les types de données et les champs.
* [[ !Profil client en temps réel DNL]](../../profile/home.md): Fournit un profil de consommation unifié en temps réel basé sur des données agrégées provenant de plusieurs sources.

## Browse existing schemas in the [!UICONTROL Schemas] workspace {#browse}

L’espace de travail [!UICONTROL Schémas] de l’ [!DNL Platform] interface utilisateur fournit une visualisation du [!DNL Schema Library]rapport, ce qui vous permet de gérer les schémas disponibles pour votre entreprise par vue. The workspace also includes the [!DNL Schema Editor], the canvas on which you can compose a schema throughout this tutorial.

Après vous être connecté [!DNL Experience Platform], sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir l&#39;espace de travail **[!UICONTROL Schémas]** . L’onglet **[!UICONTROL Parcourir]** affiche une liste de schémas (une représentation du [!DNL Schema Library]) que vous pouvez vue et personnaliser. La liste comprend le nom, le type, la classe et le comportement (enregistrement ou série chronologique) sur lesquels repose le schéma, ainsi que la date et l’heure de la dernière modification du schéma.

Sélectionnez l’icône de filtre en regard de la barre de recherche pour utiliser les fonctionnalités de filtrage pour toutes les ressources du registre, y compris les classes, les mixins et les types de données. Vous pouvez également filtrer les ressources selon qu’elles appartiennent à un Adobe ou à votre organisation et si elles ont été activées pour être utilisées dans [!DNL Real-time Customer Profile].

![](../images/tutorials/create-schema/schemas_filter.png)

## Création et attribution d’un nom à un schéma {#create}

To begin composing a schema, select **[!UICONTROL Create schema]** in the top-right corner of the **[!UICONTROL Schemas]** workspace. Un menu déroulant s&#39;affiche, vous permettant de choisir entre les classes de base [!UICONTROL XDM Individuel Profil] et [!UICONTROL XDM ExperienceEvent]. Si ces classes ne répondent pas à vos besoins, vous pouvez également sélectionner **[!UICONTROL Parcourir]** pour choisir parmi d&#39;autres classes disponibles ou [créer une nouvelle classe](#create-new-class).

Pour les besoins de ce didacticiel, sélectionnez Profil **** XDM individuel.

![](../images/tutorials/create-schema/create_schema_button.png)

Le [!DNL Schema Editor] apparaît. C’est le canevas sur lequel vous allez composer votre schéma. Puisque vous avez choisi une classe XDM standard pour baser le schéma, un schéma sans titre est automatiquement créé dans la section **[!UICONTROL Structure]** du canevas lorsque vous arrivez dans l&#39;éditeur, avec les champs standard inclus dans tous les schémas en fonction de cette classe. La classe assignée pour le schéma est également répertoriée sous **[!UICONTROL Classe]** dans la section **[!UICONTROL Composition]** .

![](../images/tutorials/create-schema/schema_editor.png)

>[!NOTE]
>
>Vous pouvez [modifier la classe d’un schéma](#change-class) à tout moment au cours du processus de composition initial avant que le schéma ne soit enregistré, mais cela doit être fait avec la plus grande prudence. Les mixins ne sont compatibles qu&#39;avec certaines classes. Par conséquent, modifier la classe réinitialise le canevas et les champs que vous avez ajoutés.

Utilisez les champs situés à droite de l’éditeur pour fournir un nom d’affichage et une description facultative du schéma. Une fois qu’un nom est saisi, le canevas se met à jour pour tenir compte du nouveau nom du schéma.

![](../images/tutorials/create-schema/name_schema.png)

Plusieurs éléments importants doivent être pris en compte lors du choix d’un nom pour votre schéma :

* Les noms des schémas doivent être courts et descriptifs afin que le schéma puisse être facilement trouvé plus tard.
* Le nom d’un schéma doit être unique, ce qui signifie qu’il doit également être suffisamment précis pour ne pas être réutilisé à l’avenir. Par exemple, si votre organisation dispose de programmes de fidélité distincts pour différentes marques, nous vous conseillons de nommer votre schéma « Brand A Loyalty Members » pour faciliter la distinction avec d’autres schémas relatifs à la fidélité que vous pourriez définir ultérieurement.
* Vous pouvez également utiliser la description du schéma pour fournir toute information contextuelle supplémentaire concernant le schéma.

Ce didacticiel compose un schéma d’assimilation de données relatives aux membres d’un programme de fidélité. Par conséquent, le schéma est nommé &quot;Membres de fidélité&quot;.

## Ajout d’un mixin {#mixin}

Vous pouvez maintenant commencer à ajouter des champs à votre schéma grâce à l’ajout de mixins. Un mixin est un groupe d’un ou de plusieurs champs qui sont souvent utilisés ensemble pour décrire un concept particulier. Ce tutoriel utilise des mixins pour décrire les membres du programme de fidélité et recueillir des informations clés telles que le nom, la date d’anniversaire, le numéro de téléphone, l’adresse, etc.

To add a mixin, select **[!UICONTROL Add]** in the **[!UICONTROL Mixins]** sub-section.

![](../images/tutorials/create-schema/add_mixin_button.png)

Une nouvelle boîte de dialogue s’affiche, affichant une liste de mixins disponibles. Chaque mixin n&#39;est destiné qu&#39;à une classe spécifique. Par conséquent, la boîte de dialogue ne liste que les mixins compatibles avec la classe que vous avez sélectionnée (dans ce cas, la [!DNL XDM Individual Profile] classe). Si vous utilisez une classe XDM standard, la liste des mixins sera triée intelligemment en fonction de la popularité de l’utilisation.

![](../images/tutorials/create-schema/mixin-popularity.png)

Si vous sélectionnez un mixin dans la liste, il apparaît dans le rail de droite. Vous pouvez sélectionner plusieurs mixins si vous le souhaitez, en ajoutant chacun à la liste dans le rail de droite avant de confirmer. En outre, une icône s’affiche sur le côté droit du mixin actuellement sélectionné, ce qui vous permet de prévisualisation de la structure des champs fournis.

![](../images/tutorials/create-schema/preview-mixin-button.png)

Lors de la prévisualisation d&#39;un mixin, une description détaillée du schéma du mixin est fournie dans le rail droit. Vous pouvez également parcourir les champs du mixin dans la trame fournie. Lorsque vous sélectionnez différents champs, le rail de droite se met à jour pour afficher des détails sur le champ en question. Sélectionnez **[!UICONTROL Précédent]** lorsque vous avez terminé de prévisualiser pour revenir à la boîte de dialogue de sélection de mixin.

![](../images/tutorials/create-schema/preview-mixin.png)

Pour ce didacticiel, sélectionnez le mixin des détails **[!UICONTROL de la personne]** Profil, puis sélectionnez **[!UICONTROL Ajouter le mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Le canevas du schéma réapparaît. The **[!UICONTROL Mixins]** section now lists &quot;[!UICONTROL Profile person details]&quot; and the **[!UICONTROL Structure]** section includes the fields contributed by the mixin. Vous pouvez sélectionner le nom du mixin sous la section **[!UICONTROL Mélanges]** pour mettre en surbrillance les champs spécifiques qu’il contient dans la trame.

![](../images/tutorials/create-schema/person_details_structure.png)

This mixin contributes several fields under the top-level name `person` with the data type &quot;[!UICONTROL Person]&quot;. Ce groupe de champs décrit les informations sur un individu, notamment son nom, sa date de naissance et son genre.

>[!NOTE]
>
>Remember that fields may use scalar types (such as string, integer, array, or date), as well as any data type (a group of fields representing a common concept) defined within the [!DNL Schema Registry].

Notice that the `name` field has a data type of &quot;[!UICONTROL Full name]&quot;, meaning it too describes a common concept and contains name-related sub-fields such as first name, last name, courtesy title, and suffix.

Sélectionnez les différents champs de la zone de travail pour afficher les champs supplémentaires qui contribuent à la structure du schéma.

## Ajout d’un autre mixin {#mixin-2}

Vous pouvez maintenant répéter les mêmes étapes pour ajouter un autre mixin. When you view the **[!UICONTROL Add mixin]** dialog this time, notice that the &quot;[!UICONTROL Profile person details]&quot; mixin has been greyed out and the checkbox next to it cannot be selected. Cela vous évite de dupliquer accidentellement des mixins que vous avez déjà inclus dans le schéma actuel.

Pour ce didacticiel, sélectionnez le mixin &quot;[!DNL Profile personal details]&quot; dans la boîte de dialogue, puis sélectionnez **[!UICONTROL Ajouter le mixin]** pour l’ajouter au schéma.

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Une fois ajouté, le canevas réapparaît. &quot;[!UICONTROL Profile personal details]&quot; is now listed under **[!UICONTROL Mixins]** in the **[!UICONTROL Composition]** section, and fields for home address, mobile phone, and more have been added under **[!UICONTROL Structure]**.

Similar to the `name` field, the fields you just added represent multi-field concepts. For example, `homeAddress` has a data type of &quot;[!UICONTROL Postal address]&quot; and `mobilePhone` has a data type of &quot;[!UICONTROL Phone number]&quot;. Vous pouvez sélectionner chacun de ces champs pour les développer et afficher les champs supplémentaires inclus dans le type de données.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Définition d’un nouveau mixin {#define-mixin}

The &quot;[!UICONTROL Loyalty Members]&quot; schema is meant to capture data related to the members of a loyalty program, so it will require some specific loyalty-related fields. Il n’existe pas de mixins standard qui contiennent les champs nécessaires. Vous devrez donc définir un nouveau mixin.

Cette fois, lorsque vous ouvrez la boîte de dialogue **[!UICONTROL Ajouter un mixin]**, sélectionnez **[!UICONTROL Créer un mixin]**. Il vous sera alors demandé de fournir un **[!UICONTROL nom d’affichage]** et une **[!UICONTROL description]** pour votre mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Comme pour les noms de classe, le nom du mixin doit être court et simple, décrivant ce que le mixin va apporter au schéma. Ces noms sont également uniques. Vous ne pourrez donc pas réutiliser le nom et devrez donc veiller à ce qu’il soit suffisamment spécifique.

For this tutorial, name the new mixin &quot;[!UICONTROL Loyalty Details]&quot;.

Sélectionnez **[!UICONTROL Ajouter le mixin]** pour revenir au [!DNL Schema Editor]. &quot;[!UICONTROL Loyalty Details]&quot; should now appear under **[!UICONTROL Mixins]** on the left-side of the canvas, but there are no fields associated with it yet and therefore no new fields appear under **[!UICONTROL Structure]**.

## Ajout de champs au mixin {#mixin-fields}

Now that you have created the &quot;[!UICONTROL Loyalty Details]&quot; mixin, it is time to define the fields that the mixin will contribute to the schema.

To begin, select the mixin name in the **[!UICONTROL Mixins]** section. Once you do this, the mixin&#39;s properties appear on the right-hand side of the editor and an **[!UICONTROL Add field]** button appears next to the name of the schema under **[!UICONTROL Structure]**.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Select **[!UICONTROL Add field]** next to &quot;[!DNL Loyalty Members]&quot; to create a new node in the structure. This node (called `_tenantId` in this example) represents your IMS Organization&#39;s tenant ID, preceded by an underscore. La présence de l’identifiant du client indique que les champs que vous ajoutez sont contenus dans l’espace de noms de votre organisation.

En d’autres termes, les champs que vous ajoutez sont propres à votre organisation et seront enregistrés dans une zone spécifique accessible uniquement à votre organisation [!DNL Schema Registry] dans une zone spécifique. Les champs que vous définissez doivent toujours être ajoutés à votre espace de nommage locataire afin d’éviter les collisions avec des noms provenant d’autres classes standard, mixins, types de données et champs.

Inside that namespaced node is a &quot;[!UICONTROL New Field]&quot;. This is the beginning of the &quot;[!UICONTROL Loyalty Details]&quot; mixin.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Using the controls on the right-hand side of the editor, start by creating a `loyalty` field with type &quot;[!UICONTROL Object]&quot; that will be used to hold your loyalty-related fields. When finished, select **[!UICONTROL Apply]**.

![](../images/tutorials/create-schema/loyalty_object.png)

The changes are applied and the newly created `loyalty` object appears. Select **[!UICONTROL Add field]** next to the object to add additional loyalty-related fields. A &quot;[!UICONTROL New Field]&quot; appears and the **[!UICONTROL Field properties]** section is visible on the right-hand side of the canvas.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Chaque champ nécessite les informations suivantes :

* **[!UICONTROL Nom]du champ :** Le nom du champ, écrit dans le boîtier du chameau. Exemple : loyaltyLevel
* **[!UICONTROL Nom]d&#39;affichage :** Nom du champ, écrit en cas de titre. Exemple : Loyalty Level
* **[!UICONTROL Type]:** Type de données du champ. This includes basic scalar types and any data types defined in the [!DNL Schema Registry]. Examples: [!UICONTROL String], [!UICONTROL Integer], [!UICONTROL Boolean], [!UICONTROL Person], [!UICONTROL Address], [!UICONTROL Phone number], etc.
* **[!UICONTROL Description]:** Une description facultative du champ doit être incluse, écrite en cas de phrase, avec un maximum de 200 caractères.

The first field for the `Loyalty` object will be a string called `loyaltyId`. When setting the new field&#39;s type to &quot;[!UICONTROL String]&quot;, the **[!UICONTROL Field properties]** section becomes populated with several options for applying constraints, including **[!UICONTROL Default value]**, **[!UICONTROL Format]**, and **[!UICONTROL Maximum length]**.

![](../images/tutorials/create-schema/string_constraints.png)

Différentes options de contraintes sont disponibles selon le type de données sélectionné. Since `loyaltyId` will be an email address, select &quot;[!UICONTROL email]&quot; from the **[!UICONTROL Format]** dropdown menu. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer vos modifications.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Add more fields to the mixin {#mixin-fields-2}

Now that you have added the `loyaltyId` field, you can add additional fields to capture loyalty-related information such as:

* Points (entier)
* Membre depuis (date)

Each field is added by selecting **[!UICONTROL Add field]** on the `loyalty` object and filling in the required information.

Une fois terminé, l’objet Fidélité contient des champs pour l’identifiant de fidélité, les points et le membre depuis.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## ajouter un champ d’énumération au mixin {#enum}

When defining fields in the [!DNL Schema Editor], there are some additional options that you can apply to basic field types in order to provide further constraints on the data the field can contain. Les cas d’utilisation de ces contraintes sont expliqués dans le tableau suivant :

| Contrainte | Description |
| --- | --- |
| [!UICONTROL Obligatoire] | Indique que le champ est requis pour l’assimilation de données. Toute donnée chargée dans un ensemble de données basé sur ce schéma qui ne contient pas ce champ sera défaillante lors de l’ingestion. |
| [!UICONTROL Tableau] | Indique que le champ contient un tableau de valeurs, chacune avec le type de données spécifié. Par exemple, l’utilisation de cette contrainte sur un champ dont le type de données est &quot;[!UICONTROL String]&quot; indique que le champ contiendra un tableau de chaînes. |
| [!UICONTROL Enum] | Indique que ce champ doit contenir l’une des valeurs d’une liste énumérée de valeurs possibles. |
| [!UICONTROL Identité] | Indique que ce champ est un champ d’identité. Vous trouverez plus d’informations sur les champs d’identité [dans la suite de ce tutoriel](#identity-field). |
| [!UICONTROL Relation] | Bien que les relations de schéma puissent être déduites par l&#39;utilisation du schéma et [!DNL Real-time Customer Profile]de l&#39;union, cela ne s&#39;applique qu&#39;aux schémas qui partagent la même classe. La contrainte [!UICONTROL Relation] indique que ce champ fait référence à l&#39;identité Principale d&#39;un schéma en fonction d&#39;une classe différente, ce qui implique une relation entre les deux schémas. See the tutorial on [defining a relationship](./relationship-ui.md) for more information. |

Pour ce didacticiel, l’ [!DNL "loyalty"] objet du schéma nécessite un nouveau champ d’énumération qui décrit le &quot;niveau de fidélité&quot; d’un client, où la valeur ne peut être que l’une des quatre options possibles. To add this field to the schema, select **[!UICONTROL Add field]** beside the `loyalty` object and fill in the required fields for **[!UICONTROL Field name]** and **[!UICONTROL Display name]**. Pour **[!UICONTROL Type]**, sélectionnez &quot;[!UICONTROL Chaîne]&quot;.

![](../images/tutorials/create-schema/loyalty-level-type.png)

D’autres cases à cocher s’affichent pour le champ une fois son type sélectionné, notamment les cases **[!UICONTROL Tableau]**, **[!UICONTROL Enum]** et **[!UICONTROL Identité]**.

Select the **[!UICONTROL Enum]** checkbox to open the **[!UICONTROL Enum values]** section below. Ici, vous pouvez saisir la **[!UICONTROL valeur]** (en Camel Case) et le **[!UICONTROL libellé]** (nom facultatif et facile à lire écrit en Title Case) pour chaque niveau de fidélité acceptable.

Une fois toutes les propriétés de champ remplies, sélectionnez **[!UICONTROL Appliquer]** pour ajouter le champ &quot;[!DNL loyaltyLevel]&quot; à l’ `loyalty` objet.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

## Conversion d’un objet à plusieurs champs en un type de données {#datatype}

L’ `loyalty` objet contient désormais plusieurs champs spécifiques à la fidélité et représente une structure de données commune qui peut s’avérer utile dans d’autres schémas. Le [!DNL Schema Editor] permet d’appliquer facilement des objets réutilisables à plusieurs champs en convertissant la structure de ces objets en types de données.

Les types de données permettent l’utilisation cohérente de structures à champs multiples, avec plus de flexibilité que les mixins, car ils peuvent être utilisés n’importe où dans un schéma. Pour ce faire, définissez la valeur **[!UICONTROL Type]** du champ sur celle de tout type de données défini dans le [!DNL Schema Registry].

To convert the `loyalty` object to a data type, select the `loyalty` field under **[!UICONTROL Structure]**, then select **[!UICONTROL Convert to new data type]** on the right-hand side of the editor under **[!UICONTROL Field properties]**. Une fenêtre contextuelle verte s’affiche, confirmant que l’objet a bien été converti.

![](../images/tutorials/create-schema/convert-data-type.png)

Now, when you look under **[!UICONTROL Structure]**, you can see that the `loyalty` field has a data type of &quot;[!DNL Loyalty]&quot; and the fields have small lock icons beside them, indicating they are no longer individual fields but rather part of a multi-field data type.

![](../images/tutorials/create-schema/loyalty_data_type.png)

In a future schema, you could now assign a field the **[!UICONTROL Type]** of &quot;[!DNL Loyalty]&quot; and it would automatically include fields for ID, loyalty level, member since, and points.

## Rechercher et filtrer les champs de schéma

Votre schéma contient désormais plusieurs mixins en plus des champs fournis par sa classe de base. Lorsque vous travaillez avec des schémas plus volumineux, vous pouvez cocher les cases en regard des noms de mixin dans le rail de gauche pour filtrer les champs affichés uniquement ceux fournis par les mixins qui vous intéressent.

![](../images/tutorials/create-schema/filter-by-mixin.png)

Si vous recherchez un champ spécifique dans votre schéma, vous pouvez également utiliser la barre de recherche pour filtrer les champs affichés par nom, quel que soit le mixin sous lequel ils sont fournis.

![](../images/tutorials/create-schema/search.png)

>[!IMPORTANT]
>
>La fonction de recherche tient compte des filtres de mixin sélectionnés lors de l’affichage des champs correspondants. Si une requête de recherche n’affiche pas les résultats attendus, vous devrez peut-être vérifier par doublon que vous ne filtrez aucun mixin pertinent.

## Définition d’un champ de schéma comme champ d’identité {#identity-field}

La structure de données standard fournie par les schémas peut être exploitée pour identifier les données appartenant à la même personne sur plusieurs sources, ce qui permet d&#39;utiliser divers cas d&#39;utilisation en aval tels que la segmentation, le rapports, l&#39;analyse des données scientifiques, etc. Pour regrouper les données en fonction des identités individuelles, les champs clés doivent être marqués comme champs [!UICONTROL Identité] dans les schémas applicables.

[!DNL Experience Platform] facilite la désignation d&#39;un champ d&#39;identité grâce à l&#39;utilisation d&#39;une case à cocher **[!UICONTROL Identité]** dans le [!DNL Schema Editor]. Cependant, vous devez déterminer quel champ est le meilleur candidat à utiliser comme identité, en fonction de la nature de vos données.

For example, there may be thousands of loyalty program members belonging to the same &quot;loyalty level&quot;, but each member of the loyalty program has a unique `loyaltyId` (which in this instance is the individual member&#39;s email address). The fact that `loyaltyId` is a unique identifier for each member makes it a good candidate for an identity field, whereas `loyaltyLevel` is not.

>[!IMPORTANT]
>
>Les étapes décrites ci-dessous expliquent comment ajouter un descripteur d&#39;identité à un champ de schéma existant. Au lieu de définir des champs d&#39;identité dans la structure du schéma lui-même, vous pouvez également utiliser un `identityMap` champ pour contenir des informations d&#39;identité.
>
>Si vous prévoyez d&#39;utiliser `identityMap`, gardez à l&#39;esprit qu&#39;il remplacera toute identité Principale que vous ajouterez directement au schéma. Pour plus d&#39;informations, consultez la section sur `identityMap` les [bases du guide](../schema/composition.md#identityMap) de composition de schéma.

Dans la section **[!UICONTROL Structure]** de l’éditeur, sélectionnez le `loyaltyId` champ et la case à cocher **[!UICONTROL Identité]** s’affiche sous Propriétés **[!UICONTROL du]** champ. Check the box and the option to set this as the **[!UICONTROL Primary identity]** appears. Sélectionnez également cette zone.

>[!NOTE]
>
>Chaque schéma ne peut contenir qu’un seul champ d’identité principal. Une fois qu&#39;un champ de schéma a été défini comme identité Principale, vous recevrez un message d&#39;erreur si vous tentez par la suite de définir un autre champ d&#39;identité dans le schéma comme Principal.

Ensuite, vous devez fournir un espace de nommage **** d&#39;identité à partir de la liste d&#39;espaces de nommage prédéfinis dans la liste déroulante. Puisque `loyaltyId` est l’adresse électronique du client, sélectionnez &quot;[!UICONTROL Courriel]&quot; dans la liste déroulante. Sélectionnez **[!UICONTROL Appliquer]** pour confirmer les mises à jour apportées au `loyaltyId` champ.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Pour une liste des espaces de nommage standard et de leurs définitions, voir la [[!DNL Identity Service] documentation](../../identity-service/troubleshooting-guide.md#standard-namespaces).

Après l’application de la modification, l’icône `loyaltyId` affiche un symbole d’empreinte digitale, indiquant qu’il s’agit désormais d’un champ d’identité. En outre, le [!DNL Loyalty Details] mixin du rail gauche liste le champ d&#39;identité situé en dessous, ce qui vous permet de déterminer facilement quel mixin d&#39;un schéma fournit ce ou ces champs d&#39;identité de schéma.

![](../images/tutorials/create-schema/identity-applied.png)

Now all data ingested into the `loyaltyId` field will be used to help identify that individual and stitch together a single view of that customer. To learn more about working with identities in [!DNL Experience Platform], please review the [[!DNL Identity Service]](../../identity-service/home.md) documentation.

## Enable the schema for use in [!DNL Real-time Customer Profile] {#profile}

[[ !Profil client en temps réel DNL]](../../profile/home.md) utilise les données d&#39;identité [!DNL Experience Platform] pour fournir une vue holistique de chaque client individuel. Le service crée des profils robustes de 360° d&#39;attributs du client ainsi que des comptes horodatés de chaque interaction que les clients ont eue dans tout système intégré à [!DNL Experience Platform].

In order for a schema to be enabled for use with [!DNL Real-time Customer Profile], it must have a primary identity defined. Vous recevrez un message d&#39;erreur si vous tentez d&#39;activer un schéma sans définir au préalable une identité Principale.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

To enable the &quot;Loyalty Members&quot; schema for use in [!DNL Profile], begin by selecting &quot;[!DNL Loyalty Members]&quot; in the **[!UICONTROL Structure]** section of the editor.

Sur le côté droit de l’éditeur, des informations sur le schéma, y compris son nom d’affichage, sa description et son type, s’affichent. Outre ces informations, il existe un bouton de bascule **[!UICONTROL Profil]** .

![](../images/tutorials/create-schema/profile-toggle.png)

Select **[!UICONTROL Profile]** and a popover appears, asking you to confirm that you wish to enable the schema for [!DNL Profile].

<img src="../images/tutorials/create-schema/enable-profile.png" width="700" /><br>

>[!WARNING]
>
>Once a schema has been enabled for [!DNL Real-time Customer Profile] and saved, it cannot be disabled.

Sélectionnez **[!UICONTROL Activer]** pour confirmer votre choix. Vous pouvez sélectionner à nouveau la bascule **[!UICONTROL Profil]** pour désactiver le schéma si vous le souhaitez, mais une fois que le schéma a été enregistré alors qu&#39;il [!DNL Profile] est activé, il ne peut plus être désactivé.

## Étapes suivantes et ressources supplémentaires

Maintenant que vous avez fini de composer le schéma, vous pouvez voir le schéma complet dans la trame. Sélectionnez **[!UICONTROL Enregistrer]** et le schéma sera enregistré dans le [!DNL Schema Library]fichier, ce qui le rendra accessible par [!DNL Schema Registry]le.

Votre nouveau schéma peut désormais être utilisé pour importer des données dans [!DNL Platform]. Pour rappel, une fois que le schéma a été utilisé pour ingérer des données, seules des modifications additives peuvent être apportées. Reportez-vous aux [principes de base de la composition des schémas](../schema/composition.md) pour plus d’informations sur le contrôle de version des schémas.

Vous pouvez maintenant suivre le didacticiel sur la [définition d’une relation de schéma dans l’interface utilisateur](./relationship-ui.md) pour ajouter un nouveau champ de relation au schéma &quot;Membres fidèles&quot;.

The &quot;Loyalty Members&quot; schema is also available to be viewed and managed using the [!DNL Schema Registry] API. To begin working with the API, start by reading the [[!DNL Schema Registry API] developer guide](../api/getting-started.md).

### Ressources vidéo

>[!WARNING]
>
>L’ [!DNL Platform] interface utilisateur affichée dans les vidéos suivantes est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

La vidéo suivante montre comment créer un schéma simple dans l’ [!DNL Platform] interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

La vidéo ci-dessous est destinée à vous aider à mieux comprendre comment travailler avec des mixins et des classes.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Annexe

Les sections suivantes fournissent des informations complémentaires sur l&#39;utilisation de la [!DNL Schema Editor]méthode.

### Création d’une nouvelle classe {#create-new-class}

[!DNL Experience Platform] offre la possibilité de définir un schéma basé sur une classe propre à votre organisation.

Dans l’espace de travail **[!UICONTROL Schémas]** , sélectionnez **[!UICONTROL Créer un schéma]**, puis sélectionnez **[!UICONTROL Parcourir]** dans la liste déroulante.

![](../images/tutorials/create-schema/browse-classes.png)

Une boîte de dialogue s&#39;affiche, vous permettant de choisir parmi une liste de classes disponibles. Dans la partie supérieure de la boîte de dialogue, sélectionnez **[!UICONTROL Créer une classe]**. You can then give your new class a **[!UICONTROL Display name]** (a short, descriptive, unique, and user-friendly name for the class), a **[!UICONTROL Description]**, and a **[!UICONTROL Behavior]** (&quot;[!UICONTROL Record]&quot; or &quot;[!UICONTROL Time Series]&quot;) for the data the schema will define.

![](../images/tutorials/create-schema/create_new_class.png)

>[!IMPORTANT]
>
>Lors de la création d’un schéma qui met en œuvre une classe définie par votre organisation, n’oubliez pas que les mixins ne peuvent être utilisés qu’avec des classes compatibles. Since the class you defined is new, there are no compatible mixins listed in the **[!UICONTROL Add mixin]** dialog. Instead, you will need to select **[!UICONTROL Create new mixin]** and define a mixin for use with that class. La prochaine fois que vous composerez un schéma mettant en œuvre la nouvelle classe, le mixin que vous avez défini sera répertorié et pourra être utilisé.

### Modification de la classe d’un schéma {#change-class}

Vous pouvez modifier la classe d&#39;un schéma à tout moment pendant le processus de composition initial avant que le schéma n&#39;ait été enregistré.

>[!WARNING]
>
>Réassigner la classe à un schéma doit être fait avec une extrême prudence. Les mixins ne sont compatibles qu&#39;avec certaines classes. Par conséquent, modifier la classe réinitialise le canevas et les champs que vous avez ajoutés.

Pour réaffecter une classe, sélectionnez **[!UICONTROL Attribuer]** dans la partie gauche du canevas.

![](../images/tutorials/create-schema/assign_class_button.png)

A dialog appears that displays a list of all available classes, including any defined by your organization (the owner being &quot;[!UICONTROL Customer]&quot;) as well as standard classes defined by Adobe.

Sélectionnez une classe dans la liste pour afficher sa description sur le côté droit de la boîte de dialogue. You can also select **[!UICONTROL Preview class structure]** to see the fields and metadata associated with the class. Sélectionnez **[!UICONTROL Affecter une classe]** pour continuer.

![](../images/tutorials/create-schema/assign_class.png)

Une nouvelle boîte de dialogue s&#39;ouvre vous demandant de confirmer que vous souhaitez affecter une nouvelle classe. Sélectionnez **[!UICONTROL Attribuer]** pour confirmer.

![](../images/tutorials/create-schema/assign-confirm.png)

Après avoir confirmé le changement de classe, le canevas sera réinitialisé et tous les progrès de la composition seront perdus.
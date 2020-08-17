---
keywords: Experience Platform;home;popular topics;schema;Schema;create schema;enum;XDM individual profile;primary identity;primary idenity;enum datatype;schema design
solution: Experience Platform
title: Création d’un schéma à l’aide de l’éditeur de schémas
topic: tutorials
description: Ce tutoriel décrit les étapes de création d’un schéma à l’aide de l’éditeur de schémas d’Experience Platform.
translation-type: tm+mt
source-git-commit: bf99b08a1093a815687cc06372407949e170a0b3
workflow-type: tm+mt
source-wordcount: '3392'
ht-degree: 59%

---


# Créez un schéma à l’aide de la variable [!DNL Schema Editor]

The [!DNL Schema Registry] provides a user interface and RESTful API from which you can view and manage all resources in the Adobe Experience Platform [!DNL Schema Library]. The [!DNL Schema Library] contains resources made available to you by Adobe, Experience Platform partners, and vendors whose applications you use, as well as resources that you define and save to the [!DNL Schema Registry].

This tutorial covers the steps for creating a schema using the Schema Editor within [!DNL Experience Platform]. Si vous préférez composer un schéma à l’aide de l’API Schema Registry, veuillez commencer par lire le [guide de développement du registre des schémas](../api/getting-started.md) avant de vous lancer dans le tutoriel sur la [création d’un schéma à l’aide de l’API](create-schema-api.md).

Ce tutoriel comprend également des étapes pour [définir une nouvelle classe](#create-new-class) que vous pourrez ensuite utiliser pour composer un schéma.

## Prise en main

Ce tutoriel exige une bonne compréhension des différents aspects d’Adobe Experience Platform inhérents à l’utilisation de l’éditeur de schémas. Avant de commencer ce tutoriel, veuillez consulter la documentation relative aux concepts suivants :

* [!DNL Experience Data Model (XDM)](../home.md): Cadre normalisé selon lequel la plate-forme organise les données d’expérience client.
* [Principes de base de la composition des schémas](../schema/composition.md) : présentation des schémas XDM et de leurs blocs de création, notamment les classes, les mixins, les types de données et les champs.
* [!DNL Real-time Customer Profile](../../profile/home.md) : fournit un profil client en temps réel unifié basé sur des données agrégées issues de plusieurs sources.

Ce tutoriel nécessite d’avoir accès à [!DNL Experience Platform]. If you do not have access to an IMS Organization in [!DNL Experience Platform], please speak to your system administrator before proceeding.

## Exploration des schémas existants dans l’espace de travail des schémas {#browse}

The Schemas workspace within [!DNL Experience Platform] provides a visualization of the [!DNL Schema Library], allowing you to view and manage all of the schemas available to you, as well as compose new ones. L’espace de travail comprend également l’éditeur de schémas, le canevas sur lequel vous allez composer un schéma tout au long de ce tutoriel.

After logging into [!DNL Experience Platform], click **[!UICONTROL Schemas]** in the left-hand navigation and you will be taken to the Schemas workspace. You will see a list of schemas (a representation of the [!DNL Schema Library]) where you can view, manage, and customize all schemas available to you. La liste comprend le nom, le type, la classe et le comportement (enregistrement ou série chronologique) sur lesquels repose le schéma, ainsi que la date et l’heure de la dernière modification du schéma.

Cliquez sur l’icône de filtrage à côté de la barre de recherche afin d’utiliser les fonctionnalités de filtrage pour toutes les ressources du registre, y compris les classes, les mixins et les types de données.

![Affichage de la bibliothèque des schémas](../images/tutorials/create-schema/schemas_filter.png)

## Création et attribution d’un nom à un schéma {#create}

Pour commencer à composer un schéma, cliquez sur **[!UICONTROL Créer un schéma]** dans le coin supérieur droit de l’espace de travail des schémas.

![Bouton Créer un schéma](../images/tutorials/create-schema/create_schema_button.png)

L’*éditeur de schémas* s’affiche. C’est le canevas sur lequel vous allez composer votre schéma. Lorsque vous arrivez dans l’éditeur, un « Schéma sans titre » est automatiquement créé dans la section *Structure* du canevas pour que vous puissiez commencer à le personnaliser.

![Éditeur de schémas](../images/tutorials/create-schema/schema_editor.png)

Dans la partie droite de l’éditeur se trouvent les *propriétés du schéma* où vous pouvez donner un nom au schéma (en utilisant le champ **[!UICONTROL Nom d’affichage]**). Une fois qu’un nom est saisi, le canevas se met à jour pour tenir compte du nouveau nom du schéma.

![Canevas de schéma](../images/tutorials/create-schema/name_schema.png)

Plusieurs éléments importants doivent être pris en compte lors du choix d’un nom pour votre schéma :

* Le nom d’un schéma doit être court et descriptif afin qu’il puisse être facilement retrouvé par la suite dans la bibliothèque.
* Le nom d’un schéma doit être unique, ce qui signifie qu’il doit également être suffisamment précis pour ne pas être réutilisé à l’avenir. Par exemple, si votre organisation dispose de programmes de fidélité distincts pour différentes marques, nous vous conseillons de nommer votre schéma « Brand A Loyalty Members » pour faciliter la distinction avec d’autres schémas relatifs à la fidélité que vous pourriez définir ultérieurement.
* Vous pouvez éventuellement fournir des informations supplémentaires sur le schéma en utilisant le champ **[!UICONTROL Description]**.

Ce tutoriel compose un schéma pour ingérer les données relatives aux membres d’un programme de fidélité, c’est pourquoi le schéma est nommé « Loyalty Members ».

## Attribution d’une classe {#class}

Dans la partie gauche de l’éditeur se trouve la section *Composition*. Elle contient actuellement deux sous-sections : *[!UICONTROL Schéma]* et *[!UICONTROL Classe]*.

Maintenant que le schéma a un nom, il est temps d’attribuer la classe que le schéma va mettre en œuvre. Cliquez sur **[!UICONTROL Attribuer]** en regard de *[!UICONTROL Classe]*.

![](../images/tutorials/create-schema/assign_class_button.png)

La boîte de dialogue *[!UICONTROL Attribuer une classe]* s’affiche. Cette fenêtre affiche une liste de toutes les classes disponibles, y compris celles définies par votre organisation (le propriétaire étant « Client ») ainsi que les classes standard définies par Adobe.

Cliquez sur le nom de la classe pour afficher sa description. Vous pouvez également choisir l’option **[!UICONTROL Prévisualiser la structure de la classe]** pour voir les champs et les métadonnées associés à la classe.

This tutorial uses the [!DNL XDM Individual Profile] class. Cliquez sur le bouton radio en regard de la classe pour la sélectionner, puis cliquez sur **[!UICONTROL Attribuer une classe]**.

![Boîte de dialogue Attribuer une classe](../images/tutorials/create-schema/assign_class.png)

Le canevas réapparaît. The *[!UICONTROL Class]* section now contains the class you selected ([!DNL XDM Individual Profile]) and the fields contributed by the [!DNL XDM Individual Profile] class are now visible within the *[!UICONTROL Structure]* section.

![Classe XDM Individual Profile attribuée](../images/tutorials/create-schema/class_assigned_structure.png)

Les champs s’affichent au format « fieldName | Data Type ». Les étapes de définition des champs de schéma dans l’interface utilisateur sont expliquées dans la suite de ce tutoriel.

>[!NOTE]
>
>Vous pouvez [modifier la classe d’un schéma](#change-class) à tout moment au cours du processus de composition initial avant que le schéma ne soit enregistré, mais cela doit être fait avec la plus grande prudence. Les mixins ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialisera le canevas et tous les champs que vous avez ajoutés.

## Ajout d’un mixin {#mixin}

Maintenant qu’une classe a été attribuée, la section *Composition* contient une troisième sous-section : *[!UICONTROL Mixins]*.

Vous pouvez maintenant commencer à ajouter des champs à votre schéma grâce à l’ajout de mixins. Un mixin est un groupe d’un ou de plusieurs champs qui décrivent un concept particulier. Ce tutoriel utilise des mixins pour décrire les membres du programme de fidélité et recueillir des informations clés telles que le nom, la date d’anniversaire, le numéro de téléphone, l’adresse, etc.

Pour ajouter un mixin, cliquez sur **Ajouter** dans la sous-section *Mixins*.

![](../images/tutorials/create-schema/add_mixin_button.png)

La boîte de dialogue *[!UICONTROL Ajouter un mixin]* s’affiche. Mixins are only intended for use with specific classes, therefore the list of mixins shows only those compatible with the class you selected (in this case, the [!DNL XDM Individual Profile] class).

En sélectionnant le bouton radio à côté d’un mixin, vous aurez la possibilité de **[!UICONTROL prévisualiser la structure du mixin]**. Sélectionnez le mixin « Profile Person Details », puis cliquez sur **[!UICONTROL Ajouter un mixin]**.

![](../images/tutorials/create-schema/add_mixin_person_details.png)

Le canevas du schéma réapparaît. The *[!UICONTROL Mixins]* section now lists the &quot;[!UICONTROL Profile Person Details]&quot; mixin and the *[!UICONTROL Structure]* section includes the fields contributed by the mixin.

![](../images/tutorials/create-schema/person_details_structure.png)

Ce mixin met à disposition plusieurs champs sous le nom de premier niveau « person » avec le type de données « Person ». Ce groupe de champs décrit les informations sur un individu, notamment son nom, sa date de naissance et son genre.

>[!NOTE]
>
>Remember that fields may use scalar types (such as string, integer, array, or date) as their data type, as well as any &quot;data type&quot; (a group of fields representing a common concept) in the [!DNL Schema Registry].

Notice that the &quot;[!UICONTROL name]&quot; field has a data type of &quot;[!UICONTROL Person Name]&quot;, meaning it too describes a common concept and contains name-related sub-fields such as first name, last name, and full name.

Cliquez sur les différents champs dans le canevas pour voir les champs supplémentaires contribuant à la structure du schéma.

## Ajout d’un autre mixin {#mixin-2}

Vous pouvez maintenant répéter les mêmes étapes pour ajouter un autre mixin. When you view the *[!UICONTROL Add Mixin]* dialog this time, notice that the &quot;[!UICONTROL Profile Person Details]&quot; mixin has been greyed out and the radio button next to it cannot be selected. Cela vous évite de dupliquer accidentellement des mixins que vous avez déjà inclus dans le schéma actuel.

Vous pouvez maintenant ajouter &quot;[!DNL Profile Personal Details" mixin] à partir de la boîte de dialogue *[!UICONTROL Ajouter le mixin]* .

![](../images/tutorials/create-schema/add_mixin_personal_details.png)

Une fois ajouté, le canevas réapparaît. The &quot;[!UICONTROL Profile Personal Details]&quot; is now listed under *[!UICONTROL Mixins]* in the *[!UICONTROL Composition]* section, and fields for home address, mobile phone, and more have been added under *[!UICONTROL Structure]*.

Similar to the &quot;[!UICONTROL name]&quot; field, the fields you just added represent multi-field concepts. For example, &quot;[!UICONTROL homeAddress]&quot; has a data type of &quot;[!UICONTROL Address]&quot; and &quot;[!UICONTROL mobilePhone]&quot; has a data type of &quot;[!UICONTROL Phone Number]&quot;. Vous pouvez cliquer sur chacun de ces champs pour les développer et afficher les champs supplémentaires inclus dans le type de données.

![](../images/tutorials/create-schema/personal_details_structure.png)

## Définition d’un nouveau mixin {#define-mixin}

The &quot;[!UICONTROL Loyalty Members]&quot; schema is meant to capture data related to the members of a loyalty program, so it will require some specific loyalty-related fields. Il n’existe pas de mixins standard qui contiennent les champs nécessaires. Vous devrez donc définir un nouveau mixin.

Cette fois, lorsque vous ouvrez la boîte de dialogue *[!UICONTROL Ajouter un mixin]*, sélectionnez **[!UICONTROL Créer un mixin]**. Il vous sera alors demandé de fournir un **[!UICONTROL nom d’affichage]** et une **[!UICONTROL description]** pour votre mixin.

![](../images/tutorials/create-schema/mixin_create_new.png)

Comme pour les noms de classe, le nom du mixin doit être court et simple, décrivant ce que le mixin va apporter au schéma. Ces noms sont également uniques. Vous ne pourrez donc pas réutiliser le nom et devrez donc veiller à ce qu’il soit suffisamment spécifique.

For this tutorial, name the new mixin &quot;[!UICONTROL Loyalty Details]&quot;.

Cliquez sur **[!UICONTROL Ajouter un mixin]** pour revenir à l’éditeur de schémas. &quot;[!UICONTROL Loyalty Details]&quot; should now appear under *[!UICONTROL Mixins]* on the left-side of the canvas, but there are no fields associated with it yet and therefore no new fields appear under *[!UICONTROL Structure]*.

## Ajout de champs au mixin {#mixin-fields}

Now that you have created the &quot;[!UICONTROL Loyalty Details]&quot; mixin, it is time to define the fields that the mixin will contribute to the schema.

Pour commencer, cliquez sur le nom du mixin dans la section *[!UICONTROL Mixins]*. Une fois que vous avez effectué cette opération, la section *[!UICONTROL Propriétés du mixin]* apparaît sur le côté droit de l’éditeur et un bouton **[!UICONTROL Ajouter un champ]** s’affiche à côté du nom du schéma sous *[!UICONTROL Structure]*.

![](../images/tutorials/create-schema/loyalty_details_structure.png)

Click **[!UICONTROL Add Field]** next to &quot;[!UICONTROL Loyalty Members]&quot; to create a new node in the structure. Ce nœud (appelé « _tenantId » dans cet exemple) représente l’identifiant du client de votre organisation IMS, précédé d’un caractère de soulignement. La présence de l’identifiant du client indique que les champs que vous ajoutez sont contenus dans l’espace de noms de votre organisation.

In other words, the fields you are adding are unique to your organization and are going to be saved in the [!DNL Schema Registry] in a specific area accessible only to your IMS Org. Fields you define must always be added to your namespace to prevent collisions with names from other standard classes, mixins, data types, and fields.

Inside that namespaced node is a &quot;[!UICONTROL New Field]&quot;. This is the beginning of the &quot;[!UICONTROL Loyalty Details]&quot; mixin.

![](../images/tutorials/create-schema/new_field_loyalty.png)

Using *[!UICONTROL Field Properties]* on the right-hand side of the editor, start by creating a &quot;[!UICONTROL loyalty]&quot; field with type &quot;[!UICONTROL Object]&quot; that will be used to hold your loyalty-related fields. Lorsque vous avez terminé, cliquez sur **[!UICONTROL Appliquer]**.

![](../images/tutorials/create-schema/loyalty_object.png)

The changes are applied and the newly created &quot;[!UICONTROL loyalty]&quot; object appears. Cliquez sur **[!UICONTROL Ajouter un champ]** à côté de l’objet pour ajouter des champs supplémentaires liés à la fidélité. Un « Nouveau champ » apparaît et la section *[!UICONTROL Propriétés du champ]* est visible sur le côté droit du canevas.

![](../images/tutorials/create-schema/new_field_in_loyalty_object.png)

Chaque champ nécessite les informations suivantes :

* **[!UICONTROL Nom]du champ :** Le nom du champ, écrit dans le boîtier du chameau. Exemple : loyaltyLevel
* **[!UICONTROL Nom]d&#39;affichage :** Nom du champ, écrit en cas de titre. Exemple : Loyalty Level
* **[!UICONTROL Type]:** Type de données du champ. This includes basic scalar types and any data types defined in the [!DNL Schema Registry]. Exemples : string, integer, boolean, Person, Address, Phone Number, etc. (chaîne, entier, booléen, Personne, Adresse, Numéro de téléphone, etc.)
* **[!UICONTROL Description]:** Une description facultative du champ doit être incluse, écrite en cas de phrase. (200 caractères max.)

The first field for the Loyalty object will be a string called &quot;[!UICONTROL loyaltyId]&quot;. When setting the new field&#39;s type to &quot;[!UICONTROL String]&quot;, the *[!UICONTROL Field Properties]* window becomes populated with several options for applying constraints, including **[!UICONTROL Default Value]**, **[!UICONTROL Format]**, and **[!UICONTROL Maximum Length]**.

![](../images/tutorials/create-schema/string_constraints.png)

Différentes options de contraintes sont disponibles selon le type de données sélectionné. Since &quot;[!UICONTROL loyaltyId]&quot; will be an email address, select &quot;[!UICONTROL email]&quot; from the **[!UICONTROL Format]** dropdown menu. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer vos modifications.

![](../images/tutorials/create-schema/loyaltyId_field.png)

## Ajout de champs supplémentaires au mixin {#mixin-fields-2}

Now that you have added the &quot;[!UICONTROL loyaltyId]&quot; field, you can add additional fields to capture loyalty-related information such as:

* Points (nombre entier)
* Member Since (Membre depuis, date)

Chaque champ est ajouté en cliquant sur **[!UICONTROL Ajouter un champ]** sur l’objet Loyalty et en renseignant les informations requises.

Une fois cette étape terminée, l’objet Loyalty contiendra des champs pour : Loyalty ID, Points, et Member Since.

![](../images/tutorials/create-schema/loyalty_object_fields.png)

## Ajout d’un champ « enum » au mixin {#enum}

Lorsque vous définissez des champs dans l’éditeur de schémas, vous pouvez appliquer certaines options supplémentaires aux types de champs de base afin de limiter davantage les données que le champ peut contenir.

An example of this would be a &quot;[!UICONTROL Loyalty Level]&quot; field, where the value can only be one of four possible options. To add this field to the schema, click **[!UICONTROL Add Field]** beside the &quot;[!UICONTROL loyalty]&quot; object and fill in the required fields under *[!UICONTROL Field Properties]*.

Pour **[!UICONTROL Type]**, sélectionnez « String » et des cases à cocher supplémentaires s’afficheront pour **[!UICONTROL Tableau]**, **[!UICONTROL Énumération]**, et **[!UICONTROL Identité]**.

Cochez la case **[!UICONTROL Énumération]** pour ouvrir la section *[!UICONTROL Valeurs d’énumération]* ci-dessous. Ici, vous pouvez saisir la **[!UICONTROL valeur]** (en Camel Case) et le **[!UICONTROL libellé]** (nom facultatif et facile à lire écrit en Title Case) pour chaque niveau de fidélité acceptable.

When you have completed all field properties, click **[!UICONTROL Apply]** and the &quot;[!UICONTROL loyaltyLevel]&quot; field will be added to the &quot;loyalty&quot; object.

![](../images/tutorials/create-schema/loyalty_level_enum.png)

Vous trouverez ci-dessous davantage d’informations sur les contraintes supplémentaires disponibles :

* **[!UICONTROL Obligatoire]:** Indique que le champ est requis pour l’assimilation de données. Toute donnée chargée dans un ensemble de données basé sur ce schéma qui ne contient pas ce champ sera défaillante lors de l’ingestion.
* **[!UICONTROL Tableau]:** Indique que le champ contient un tableau de valeurs, chacune avec le type de données spécifié. Par exemple, si vous sélectionnez un type de données « String » et que vous cochez la case « Tableau », cela signifie que le champ contiendra un tableau de chaînes.
* **[!UICONTROL Enum]:** Indique que ce champ doit contenir l’une des valeurs d’une liste énumérée de valeurs possibles.
* **[!UICONTROL Identité]:** Indique que ce champ est un champ d’identité. Vous trouverez plus d’informations sur les champs d’identité [dans la suite de ce tutoriel](#identity-field).

## Conversion d’un objet à plusieurs champs en un type de données {#datatype}

After adding several loyalty-specific fields, the &quot;[!UICONTROL loyalty]&quot; object now contains a common data structure that could be useful in other schemas.

Si vous estimez qu’une structure à plusieurs champs peut être réutilisable et que vous souhaitez avoir la possibilité d’utiliser cette même structure de données ailleurs, l’éditeur de schémas vous permet de convertir cette structure en un type de données.

Les types de données permettent l’utilisation cohérente de structures à champs multiples, avec plus de flexibilité que les mixins, car ils peuvent être utilisés n’importe où dans un schéma. Pour ce faire, définissez le **[!UICONTROL type]** d’un champ dans un mixin par rapport à celui de tout type de données défini dans le registre.

To convert the &quot;[!UICONTROL loyalty]&quot; object to a data type, click on the &quot;loyalty&quot; field under *[!UICONTROL Structure]* and select **[!UICONTROL Convert to New Data Type]** on the right-hand-side of the editor under *[!UICONTROL Field Properties]*. A small green pop-up appears confirming &quot;[!UICONTROL Object Converted to Data Type]&quot;.

Now, when you look under *[!UICONTROL Structure]*, you can see that the &quot;[!UICONTROL loyalty]&quot; field has a data type of &quot;[!UICONTROL Loyalty]&quot; and the fields have small lock icons beside them indicating they are no longer individual fields, but rather part of a multi-field structure.

In a future schema, you could now assign a field the **[!UICONTROL Type]** of &quot;[!UICONTROL Loyalty]&quot; and it would automatically include Loyalty Level, Points, Member Since, and Loyalty ID fields.

![](../images/tutorials/create-schema/loyalty_data_type.png)

## Définition d’un champ de schéma comme champ d’identité {#identity-field}

Schemas are used for ingesting data into [!DNL Experience Platform], and that data is ultimately used to identify individuals and stitch together information coming from multiple sources. To help with this process, key fields can be marked as &quot;[!UICONTROL Identity]&quot; fields.

[!DNL Experience Platform] facilite la désignation d&#39;un champ d&#39;identité grâce à l&#39;utilisation d&#39;une case à cocher **[!UICONTROL Identité]** dans le [!DNL Schema Editor].

Par exemple, il peut y avoir des milliers de membres du programme de fidélité appartenant au même « level », mais chaque membre du programme de fidélité a un « loyaltyId » unique (qui, dans ce cas, est l’adresse électronique du membre individuel). Le fait que « loyaltyId » soit un identifiant unique pour chaque membre en fait un bon candidat pour un champ d’identité, contrairement à « level ».

In the *[!UICONTROL Structure]* section of the editor, click on the &quot;[!UICONTROL loyaltyId]&quot; field that you created and you will see the **[!UICONTROL Identity]** checkbox appear under *[!UICONTROL Field Properties]*. Cochez la case et vous aurez la possibilité de la définir comme **[!UICONTROL Identité principale]**. Cochez également cette case.

Ensuite, vous devez fournir un **[!UICONTROL espace de noms d’identité]**. There are several pre-defined namespaces, but since the &quot;[!UICONTROL loyaltyId]&quot; is the member&#39;s email address, select &quot;Email&quot; from the dropdown list. You can now click **[!UICONTROL Apply]** to confirm the updates to the &quot;[!UICONTROL loyaltyId]&quot; field.

Now all data ingested into the &quot;[!UICONTROL loyaltyId]&quot; field will be used to help identify that individual and stitch together a single view of that customer.

![](../images/tutorials/create-schema/loyaltyId_primary_identity.png)

>[!NOTE]
>
>Une fois qu’un champ du schéma a été défini comme identité principale, vous recevrez un message d’erreur si vous tentez par la suite de définir un autre champ du schéma comme identité principale. Chaque schéma ne peut contenir qu’un seul champ d’identité principal.

Pour en savoir plus sur l’utilisation des identités, consultez la documentation [!DNL Identity Service](../../identity-service/home.md).

<!-- ## Relationship

Schemas define a static view of a concept, but do not provide specific details on how data based on these schemas (datasets, etc) may relate to one another. Adobe Experience Platform allows you to describe these relationships through the **Relationship** checkbox in the schema editor. 

In order to define a relationship, click on the field and check the **Relationship** checkbox on the right-side of the canvas. 

![](../images/tutorials/create-schema/relationship.png)

More information about relationships and other schema metadata can be found in the [Schema Registry API Developer Guide](../schema_registry_developer_guide.md). -->

## Enable the schema for use in [!DNL Real-time Customer Profile] {#profile}

L’éditeur de schémas permet d’activer un schéma à utiliser avec [!DNL Real-time Customer Profile](../../profile/home.md). [!DNL Profile] fournit une vue globale de chaque client individuel en établissant un profil solide à 360° des attributs du client ainsi qu’un compte horodaté de chaque interaction que le client a eue avec tout système intégré à [!DNL Experience Platform].

In order for a schema to be enabled for use with [!DNL Real-time Customer Profile], it must have a primary identity defined. Vous recevrez un message d’erreur « Missing Primary Identity » (Identité primaire manquante) si vous essayez d’activer un schéma sans avoir défini au préalable une identité principale.

<img src="../images/tutorials/create-schema/missing_primary_identity.png" width="600" /><br>

To enable the &quot;Loyalty Members&quot; schema for use in [!DNL Profile], begin by clicking on &quot;Loyalty Members&quot; in the *Structure* section of the editor.

Dans la partie droite de l’éditeur, sous *Propriétés du schéma*, des informations sur le schéma sont affichées, notamment son nom d’affichage, sa description et son type. En plus de ces informations, il y a un bouton de basculement intitulé **[!UICONTROL Profile]**.

![](../images/tutorials/create-schema/unified_profile_toggle.png)

Click **[!UICONTROL Profile]** and a pop-up appears, asking you to confirm that you wish to enable the schema for [!DNL Profile].

![](../images/tutorials/create-schema/enable_unified_profile.png)

>[!NOTE]
>
>Once a schema has been enabled for [!DNL Real-time Customer Profile] and saved, it cannot be disabled.

## Étapes suivantes et ressources supplémentaires

Now that you have finished composing a &quot;[!UICONTROL Loyalty Members]&quot; schema, you can see the complete schema in the *Structure* section of the editor. Click **[!UICONTROL Save]** and the schema will be saved to the [!DNL Schema Library], making it accessible by the [!DNL Schema Registry].

Votre nouveau schéma peut désormais être utilisé pour ingérer des données dans [!DNL Platform]. Pour rappel, une fois que le schéma a été utilisé pour ingérer des données, seules des modifications additives peuvent être apportées. Reportez-vous aux [principes de base de la composition des schémas](../schema/composition.md) pour plus d’informations sur le contrôle de version des schémas.

The &quot;[!UICONTROL Loyalty Members]&quot; schema is also available to be viewed and managed using the [!DNL Schema Registry] API. Pour commencer à utiliser l’API, consultez d’abord le [guide de développement de l’API Schema Registry](../api/getting-started.md).

>[!WARNING]
>
>L’ [!DNL Platform] interface utilisateur illustrée dans les vidéos suivantes est obsolète. Reportez-vous à la documentation ci-dessus pour obtenir les dernières captures d&#39;écran et fonctionnalités de l&#39;interface utilisateur.

La vidéo suivante montre comment créer un schéma simple dans l’ [!DNL Platform] interface utilisateur.

>[!VIDEO](https://video.tv.adobe.com/v/27012?quality=12&learn=on)

La vidéo ci-dessous est destinée à vous aider à mieux comprendre comment travailler avec des mixins et des classes.

>[!VIDEO](https://video.tv.adobe.com/v/27013?quality=12&learn=on)

## Annexe

Les informations suivantes viennent compléter le tutoriel de l’éditeur de schémas.

### Création d’une nouvelle classe {#create-new-class}

[!DNL Experience Platform] offre la possibilité de définir un schéma basé sur une classe propre à votre organisation.

Ouvrez la boîte de dialogue *[!UICONTROL Attribuer une classe]* en cliquant sur **[!UICONTROL Attribuer]** dans la section *[!UICONTROL Classe]* de l’éditeur de schémas. Within the dialog, select **C[!UICONTROL reate New Class]**.

You can then give your new class a **[!UICONTROL Display Name]** (a short, descriptive, unique, and user-friendly name for the class), a **[!UICONTROL Description]**, and a **[!UICONTROL Behavior]** (&quot;[!UICONTROL Record]&quot; or &quot;[!UICONTROL Time Series]&quot;) for the data the schema will define.

![Détails sur la nouvelle classe](../images/tutorials/create-schema/create_new_class.png)

>[!NOTE]
>
>Lors de la création d’un schéma qui met en œuvre une classe définie par votre organisation, n’oubliez pas que les mixins ne peuvent être utilisés qu’avec des classes compatibles. Comme la classe que vous avez définie est nouvelle, aucun mixin compatible n’est répertorié dans la boîte de dialogue *Ajouter un mixin*. Vous devez plutôt sélectionner **[!UICONTROL Créer un mixin]** et définir un mixin à utiliser avec cette classe. La prochaine fois que vous composerez un schéma mettant en œuvre la nouvelle classe, le mixin que vous avez défini sera répertorié et pourra être utilisé.

### Modification de la classe d’un schéma {#change-class}

À tout moment au cours du processus initial de composition du schéma, avant que le schéma ne soit enregistré, vous pouvez modifier la classe sur laquelle repose le schéma.

>[!WARNING]
>
>Réfléchissez bien avant de modifier la classe. Les mixins ne sont compatibles qu’avec certaines classes. Par conséquent, la modification de la classe réinitialise le canevas et supprime tous les champs que vous avez ajoutés à ce stade.

Pour modifier la classe, cliquez sur **[!UICONTROL Attribuer]** à côté de *[!UICONTROL Classe]* dans la section *[!UICONTROL Composition]* de l’éditeur.

Lorsque la boîte de dialogue *[!UICONTROL Attribuer une classe]* s’ouvre, vous pouvez sélectionner une nouvelle classe dans la liste disponible. Cliquez sur **[!UICONTROL Attribuer une classe]** et une nouvelle boîte de dialogue s’ouvre, vous demandant de confirmer que vous souhaitez attribuer une nouvelle classe.

![Modifier la classe](../images/tutorials/create-schema/assign_new_class_warning.png)

Si vous confirmez la modification de la classe, le canevas sera réinitialisé et toute la progression de la composition sera perdue.
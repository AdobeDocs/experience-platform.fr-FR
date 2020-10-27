---
keywords: Experience Platform;home;popular topics;ui;UI;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema editor;Schema Editor;schema;Schema;schemas;Schemas;create;relationship;Relationship;reference;Reference;
solution: Experience Platform
title: Définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas
description: Ce document fournit un didacticiel pour la définition d'une relation entre deux schémas à l'aide de l'éditeur de Schémas dans l'interface utilisateur de l'Experience Platform.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 34%

---


# Define a relationship between two schemas using the [!DNL Schema Editor]

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

Bien que les relations de schéma puissent être déduites par l&#39;utilisation du schéma et [!DNL Real-time Customer Profile]de l&#39;union, cela ne s&#39;applique qu&#39;aux schémas qui partagent la même classe. Pour établir une relation entre deux schémas appartenant à des classes différentes, un champ de relation dédié doit être ajouté à un schéma source, qui fait référence à l&#39;identité d&#39;un schéma de destination.

Ce document fournit un didacticiel pour la définition d’une relation entre deux schémas à l’aide de l’éditeur de Schémas dans l’ [!DNL Experience Platform] interface utilisateur. Les étapes de la définition des relations de schémas à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).

## Prise en main

This tutorial requires a working understanding of [!DNL XDM System] and the Schema Editor in the [!DNL Experience Platform] UI. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM en Experience Platform](../home.md): Présentation de XDM et de sa mise en oeuvre dans [!DNL Experience Platform].
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Créez un schéma à l’aide des [!DNL Schema Editor]](create-schema-ui.md)éléments suivants : Didacticiel sur les bases de l&#39;utilisation de la [!DNL Schema Editor]méthode.

## Définition d’un schéma source et de destination

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. For demonstration purposes, this tutorial creates a relationship between members of an organization&#39;s loyalty program (defined in a &quot;[!DNL Loyalty Members]&quot; schema) and their favorite hotel (defined in a &quot;[!DNL Hotels]&quot; schema).

>[!IMPORTANT]
>
>Pour établir une relation, les deux schémas doivent avoir défini des identités Principales et être autorisés à [!DNL Real-time Customer Profile]établir une relation. Reportez-vous à la section relative à l’ [activation d’un schéma pour une utilisation en Profil](./create-schema-ui.md#profile) dans le didacticiel de création de schéma si vous avez besoin de conseils sur la manière de configurer vos schémas en conséquence.

Les relations de schéma sont représentées par un champ dédié dans un schéma **** source qui fait référence à un autre champ dans un schéma **de** destination. In the steps that follow, &quot;[!DNL Loyalty Members]&quot; will be the source schema, while &quot;[!DNL Hotels]&quot; will act as the destination schema.

À titre de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant de définir une relation.

### [!DNL Loyalty Members] schema

The source schema &quot;[!DNL Loyalty Members]&quot; is based on the [!DNL XDM Individual Profile] class, and is the schema that was constructed in the tutorial for [creating a schema in the UI](create-schema-ui.md). It includes a `loyalty` object under its `_tenantId` namespace, which includes several loyalty-specific fields. One of these fields, `loyaltyId`, serves as the primary identity for the schema under the [!UICONTROL Email] namespace. Comme vous pouvez le voir sous **[!UICONTROL Propriétés du schéma]**, ce schéma a été activé pour une utilisation dans [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/loyalty-members.png)

### [!DNL Hotels] schema

Le schéma de destination &quot;[!DNL Hotels]&quot; est basé sur une classe &quot;[!DNL Hotels]&quot; personnalisée et contient des champs qui décrivent un hôtel. The `hotelId` field serves as the primary identity for the schema under a custom `hotelId` namespace. Tout comme le [!DNL Loyalty Members] schéma, ce schéma a également été activé pour [!DNL Real-time Customer Profile]le.

![](../images/tutorials/relationship/hotels.png)

## Création d’une relation mixin

>[!NOTE]
>
>Cette étape n’est requise que si votre schéma source ne dispose pas d’un champ de type chaîne dédié à utiliser comme référence au schéma de destination. Si ce champ est déjà défini dans votre schéma source, passez à l’étape suivante de la [définition d’un champ de relation](#relationship-field).

Pour définir une relation entre deux schémas, le schéma source doit disposer d’un champ dédié à utiliser comme référence au schéma de destination. Vous pouvez ajouter ce champ au schéma source en créant un nouveau mixin.

Start by selecting **[!UICONTROL Add]** in the **[!UICONTROL Mixins]** section.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

La boîte de dialogue [!UICONTROL Ajouter un mixin] s’affiche. From here, select **[!UICONTROL Create new mixin]**. Dans les champs de texte qui s’affichent, saisissez le nom d’affichage et la description du nouveau mixin. Select **[!UICONTROL Add mixin]** when finished.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

The canvas reappears with &quot;[!DNL Favorite Hotel]&quot; appearing in the **[!UICONTROL Mixins]** section. Select the mixin name, then select **[!UICONTROL Add field]** next to the root-level `Loyalty Members` field.

![](../images/tutorials/relationship/loyalty-add-field.png)

A new field appears in the canvas under the `_tenantId` namespace. Under **[!UICONTROL Field properties]**, provide a field name and display name for the field, and set its type to &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

When finished, select **[!UICONTROL Apply]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

The updated `favoriteHotel` field appears in the canvas. Select **[!UICONTROL Save]** to finalize your changes to the schema.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définition d’un champ de relation pour le schéma source {#relationship-field}

Une fois que le champ de référence dédié de votre schéma source est défini, vous pouvez le désigner comme champ de relation.

Select the `favoriteHotel` field in the canvas, then scroll down under **[!UICONTROL Field properties]** until the **[!UICONTROL Relationship]** checkbox appears. Cochez la case pour afficher les paramètres requis pour la configuration d’un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Select the dropdown for **[!UICONTROL Reference schema]** and select the destination schema for the relationship (&quot;[!DNL Hotels]&quot; in this example). If the destination schema is enabled for [!DNL Profile], the **[!UICONTROL Reference identity namespace]** field is automatically set to the namespace of the destination schema&#39;s primary identity. Si aucune identité principale n’est définie pour le schéma, vous devez sélectionner manuellement l’espace de noms que vous prévoyez d’utiliser dans le menu déroulant. Select **[!UICONTROL Apply]** when finished.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

The `favoriteHotel` field is now highlighted as a relationship in the canvas, displaying the name and reference identity namespace of the destination schema. Select **[!UICONTROL Save]** to save your changes and complete the workflow.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

By following this tutorial, you have successfully created a one-to-one relationship between two schemas using the [!DNL Schema Editor]. Les étapes de la définition des relations à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).
---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Définition d’une relation entre deux schémas à l’aide de l’éditeur de schémas
topic: tutorials
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 60%

---


# Define a relationship between two schemas using the [!DNL Schema Editor]

Comprendre les relations entre vos clients et leurs interactions avec votre marque sur divers canaux est un aspect important d’Adobe Experience Platform. Defining these relationships within the structure of your [!DNL Experience Data Model] (XDM) schemas allows you to gain complex insights into your customer data.

This document provides a tutorial for defining a one-to-one relationship between two schemas defined by your organization using the [!DNL Schema Editor] in the [!DNL Experience Platform] user interface. Les étapes de la définition des relations de schémas à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).

## Prise en main

Ce didacticiel nécessite une bonne compréhension de [!DNL XDM System] l’interface utilisateur et de son [!DNL Schema Editor] [!DNL Experience Platform] contenu. Avant de commencer ce tutoriel, consultez la documentation suivante :

* [Système XDM dans Experience Platform](../home.md) : présentation de XDM et de sa mise en œuvre dans Experience Platform.
* [Principes de base de composition des schémas](../schema/composition.md) : une présentation des blocs de création de schémas XDM.
* [Créez un schéma à l’aide de l’éditeur](create-schema-ui.md)de Schéma : Didacticiel sur les bases de l&#39;utilisation de la [!DNL Schema Editor]méthode.

## Définition d’un schéma source et de destination

Vous devez avoir déjà créé les deux schémas qui seront définis dans la relation. For demonstration purposes, this tutorial creates a relationship between members of an organization&#39;s loyalty program (defined in a &quot;[!UICONTROL Loyalty Members]&quot; schema) and their favorite hotels (defined in a &quot;Hotels&quot; schema).

Les relations de schémas sont représentées par un **[!UICONTROL schéma source]** disposant d’un champ qui fait référence à un autre champ dans un **[!UICONTROL schéma de destination]**. In the steps that follow, &quot;[!UICONTROL Loyalty Members]&quot; will be the source schema, while &quot;Hotels&quot; will act as the destination schema.

À titre de référence, les sections suivantes décrivent la structure de chaque schéma utilisé dans ce tutoriel avant de définir une relation.

### [!UICONTROL Schéma Loyalty Members]

The source schema &quot;[!UICONTROL Loyalty Members]&quot; is the schema that was constructed in the tutorial for [creating a schema in the UI](create-schema-ui.md). It includes a &quot;[!UICONTROL loyalty]&quot; object under its &quot;[!UICONTROL \_tenantId]&quot; namespace, which includes several loyalty-specific fields. One of these fields, &quot;[!UICONTROL loyaltyId]&quot;, serves as the primary identity for the schema under the &quot;[!UICONTROL Email]&quot; namespace. Comme vous pouvez le voir sous _Propriétés du schéma_, ce schéma a été activé pour une utilisation dans [!DNL Real-time Customer Profile](../../profile/home.md).

![](../images/tutorials/relationship/loyalty-members.png)

### Schéma Hotels

The destination schema &quot;[!UICONTROL Hotels]&quot; contains fields that describe a hotel, include its address, brand, number of rooms, and star rating. The &quot;[!UICONTROL hotelId]&quot; field serves as the primary identity for the schema under the &quot;ECID&quot; namespace. Unlike &quot;[!UICONTROL Loyalty Members]&quot;, this schema has not been enabled for [!DNL Real-time Customer Profile].

![](../images/tutorials/relationship/hotels.png)

## Création d’une relation mixin

>[!NOTE]
>
>Cette étape n’est nécessaire que si votre schéma source ne dispose pas d’un champ de type chaîne dédié à utiliser comme référence à un autre schéma. Si ce champ est déjà défini dans votre schéma source, passez à l’étape suivante de la [définition d’un champ de relation](#relationship-field).

Pour définir une relation entre deux schémas, le schéma source doit disposer d’un champ dédié à utiliser comme référence au schéma de destination. Vous pouvez ajouter ce champ au schéma source en créant un nouveau mixin.

Commencez par cliquer sur **[!UICONTROL Ajouter]** dans la section _Mixins_.

![](../images/tutorials/relationship/loyalty-add-mixin.png)

La boîte de dialogue [!UICONTROL _Ajouter un mixin _]s’affiche. À partir de là, cliquez sur**[!UICONTROL  Créer un nouveau mixin ]**. Dans les champs de texte qui s’affichent, saisissez le nom d’affichage et la description du nouveau mixin. Cliquez sur**[!UICONTROL  Ajouter un mixin ]**lorsque vous avez terminé.

<img src="../images/tutorials/relationship/loyalty-create-new-mixin.png" width="750"><br>

The canvas reappears with &quot;[!UICONTROL Loyalty Relationship]&quot; appearing in the _Mixins_ section. Click the mixin name, then click **[!UICONTROL Add Field]** next to the root-level &quot;[!UICONTROL Loyalty Members]&quot; field.

![](../images/tutorials/relationship/loyalty-add-field.png)

A new field appears in the canvas under the &quot;[!UICONTROL \_tenantId]&quot; namespace. Under [!UICONTROL _Field Properties _], provide a field name and display name for the field, and set its type to &quot;[!UICONTROL String]&quot;.

![](../images/tutorials/relationship/relationship-field-details.png)

Lorsque vous avez terminé, cliquez sur **[!UICONTROL Appliquer]**.

![](../images/tutorials/relationship/relationship-field-apply.png)

The updated &quot;[!UICONTROL loyaltyRelationship]&quot; field appears in the canvas. Cliquez sur **[!UICONTROL Enregistrer]** pour finaliser les modifications apportées au schéma.

![](../images/tutorials/relationship/relationship-field-save.png)

## Définition d’un champ de relation pour le schéma source {#relationship-field}

Une fois que le champ de référence dédié de votre schéma source est défini, vous pouvez le désigner comme champ de relation.

Cliquez sur le champ de référence dans le canevas, puis faites défiler la liste sous _[!UICONTROL Propriétés du champ]_jusqu’à ce que la case à cocher**[!UICONTROL  Relation ]**apparaisse. Cochez la case pour afficher les paramètres requis pour la configuration d’un champ de relation.

![](../images/tutorials/relationship/relationship-checkbox.png)

Click the dropdown for **[!UICONTROL Reference Schema]** and select the destination schema for the relationship (&quot;[!UICONTROL Hotels]&quot; in this example). Si le schéma de destination est activé pour l’union, le champ **[!UICONTROL Espace de noms d’identité de référence]** est automatiquement défini sur l’espace de noms de l’identité principale du schéma de destination. Si aucune identité principale n’est définie pour le schéma, vous devez sélectionner manuellement l’espace de noms que vous prévoyez d’utiliser dans le menu déroulant. Cliquez sur **[!UICONTROL Appliquer]** lorsque vous avez terminé.

![](../images/tutorials/relationship/reference-schema-id-namespace.png)

Le champ apparaît sous la forme d’une relation dans le canevas, affichant le nom et l’espace de noms d’identité de référence du schéma de destination. Cliquez sur **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et terminer le processus.

![](../images/tutorials/relationship/relationship-save.png)

## Étapes suivantes

By following this tutorial, you have successfully created a one-to-one relationship between two schemas using the [!DNL Schema Editor]. Les étapes de la définition des relations à l’aide de l’API sont décrites dans le tutoriel sur la [définition d’une relation à l’aide de l’API Schema Registry](relationship-api.md).
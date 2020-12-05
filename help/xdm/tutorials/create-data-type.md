---
keywords: Experience Platform;home;popular topics;ui;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;create;data type;data types;
solution: Experience Platform
title: Création et modification de types de données à l'aide de l'interface utilisateur du registre de Schéma
topic: tutorial
type: Tutorial
description: Ce didacticiel utilise l’interface utilisateur de l’Experience Platform pour vous guider dans les étapes de composition d’un type de données personnalisé.
translation-type: tm+mt
source-git-commit: 9008b49e1eb5e32b0f4cda7049bf873c689f6442
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---


# Création et modification de types de données à l’aide de l’interface utilisateur Experience Platform

Dans le modèle de données d’expérience (XDM), les types de données sont utilisés comme champs de type référence dans les classes ou les mixins de la même manière que les champs littéraux de base, la différence majeure étant que les types de données peuvent définir plusieurs sous-champs. Bien que semblables aux mixins en ce qu&#39;ils permettent l&#39;utilisation cohérente d&#39;une structure à champs multiples, les types de données sont plus flexibles parce qu&#39;ils peuvent être inclus n&#39;importe où dans la structure de schéma alors que les mixins ne peuvent être ajoutés qu&#39;au niveau racine.

Adobe Experience Platform fournit de nombreux types de données standard qui peuvent être utilisés pour couvrir un large éventail de cas d’utilisation courants de la gestion de l’expérience. Cependant, vous pouvez également définir vos propres types de données personnalisées afin de répondre à vos besoins spécifiques.

Ce didacticiel décrit les étapes de création et de modification des types de données personnalisées dans l’interface utilisateur de la plate-forme.

## Conditions préalables 

Ce didacticiel nécessite une bonne compréhension de XDM System. Reportez-vous à la présentation [de](../home.md) XDM pour une présentation du rôle de XDM dans l&#39;écosystème Experience Platform, ainsi qu&#39;aux [bases de la composition](../schema/composition.md) des schémas pour savoir comment les types de données contribuent aux schémas XDM.

Bien que ce didacticiel ne soit pas obligatoire, il est recommandé de suivre également le didacticiel sur la [composition d’un schéma dans l’interface utilisateur](./-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités du [!DNL Schema Editor].

## Ouvrez [!DNL Schema Editor] un type de données.

Dans l’interface utilisateur de la plateforme, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail des [!UICONTROL Schémas] , puis sélectionnez l’onglet Types **** de données. Une liste des types de données disponibles s’affiche, y compris ceux définis par l’Adobe et ceux créés par votre organisation.

![](../images/tutorials/create-datatype/data-types-tab.png)

Vous disposez de deux options :

* [Créer un nouveau type de données](#create)
* [Sélectionner un type de données existant à modifier](#edit)

### Create a new data type {#create}

Dans l’onglet Types **[!UICONTROL de]** données, sélectionnez **[!UICONTROL Créer un type]** de données.

![](../images/tutorials/create-datatype/create.png)

Le [!DNL Schema Editor] apparaît, indiquant la structure actuelle du nouveau type de données dans la trame. Sur le côté droit de l’éditeur, vous pouvez fournir un nom d’affichage et une description facultative pour le type de données. Veillez à fournir un nom unique et concis pour votre type de données, tel qu’il sera identifié lors de son ajout à un schéma.

Ce didacticiel crée un type de données qui décrit une propriété de restaurant, de sorte que le type de données se voit attribuer un nom d&#39;affichage &quot;Restaurant&quot;.

![](../images/tutorials/create-datatype/data-type-properties.png)

Accédez à la section [](#add-fields) suivante pour ajouter des champs au type de données au début.

### Modification d’un type de données existant

Seuls les types de données personnalisés définis par votre organisation peuvent être modifiés. Pour réduire la liste affichée, sélectionnez l’icône de filtre (Icône![de](../images/tutorials/create-datatype/filter.png)filtre) afin de révéler les contrôles de filtrage selon le [!UICONTROL propriétaire]. Sélectionnez **[!UICONTROL Client]** pour afficher uniquement les types de données personnalisés appartenant à votre organisation.

Sélectionnez le type de données à modifier dans la liste pour ouvrir le rail de droite, en indiquant les détails du type de données. Sélectionnez le nom du type de données dans le rail de droite pour ouvrir sa structure dans le [!DNL Schema Editor].

![](../images/tutorials/create-datatype/edit.png)

## Ajouter les champs au type de données {#add-fields}

Pour début d’ajouter des champs au type de données, sélectionnez l’icône **plus (+)** en regard du champ de niveau racine dans le canevas. Un nouveau champ apparaît ci-dessous et le rail droit est mis à jour pour afficher les commandes du nouveau champ.

![](../images/tutorials/create-datatype/new-field.png)

Utilisez les commandes de rail droit pour fournir un nom **[!UICONTROL de]** champ, un nom **** d’affichage et un **[!UICONTROL type]** pour le champ. Notez que le type d’un champ peut être un type scalaire de base (par exemple une chaîne, un entier ou une valeur booléenne), ou peut représenter un autre type de données à champs multiples défini par un Adobe ou votre organisation.

Le type de données Restaurant requiert un champ de chaîne pour représenter le nom du restaurant. Par conséquent, le nom [!UICONTROL du] champ est défini comme &quot;nom&quot; et le [!UICONTROL type] comme [!UICONTROL chaîne]. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer les modifications au champ.

![](../images/tutorials/create-datatype/name-field.png)

Continuez à suivre la même procédure pour ajouter des champs supplémentaires, en commençant par sélectionner l’icône **plus (+)** en regard du champ de niveau racine et en fournissant les détails de configuration dans le rail de droite.

Le type de données du restaurant comporte désormais des champs supplémentaires pour la marque, la capacité de stockage et l’espace au sol.

![](../images/tutorials/create-datatype/more-fields.png)

Outre les champs de base, vous pouvez également imbriquer d’autres types de données dans votre type de données personnalisé. Par exemple, le type de données Restaurant requiert un champ qui représente l’adresse physique de la propriété. Dans ce scénario, vous pouvez ajouter un nouveau champ &quot;adresse&quot; auquel est affecté le type de données standard &quot;[!UICONTROL Adresse]postale&quot;.

![](../images/tutorials/create-datatype/address-field.png)

Cela montre à quel point les types de données peuvent être flexibles en termes de description de vos données : les types de données peuvent utiliser des champs qui sont également des types de données, qui peuvent eux-mêmes contenir d’autres types de données, etc. Cela vous permet d’abstraire et de réutiliser des modèles de données courants dans vos schémas XDM, ce qui facilite la représentation de structures de données complexes.

Une fois que vous avez terminé d’ajouter des champs au type de données, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et ajouter le type de données au [!DNL Schema Library].

## Ajouter le type de données à un mixin

Une fois que vous avez créé un type de données, vous pouvez le début dans vos schémas. Les schémas XDM étant composés d&#39;une classe et de zéro ou plusieurs mixins, les champs fournis par un type de données ne peuvent pas être ajoutés directement à un schéma. Ils doivent être inclus dans une classe ou un mixin.

>[!NOTE]
>
>Cette section porte sur l’ajout d’un type de données à un mixin, car il s’agit du modèle le plus courant pour les types de données personnalisés. Cependant, vous pouvez également appliquer les mêmes étapes pour ajouter votre type de données à une classe.

Vous pouvez ajouter le type de données à un mixin existant ou créer entièrement un mixin. Dans les deux cas, vous devez ouvrir le [!DNL Schema Editor] schéma auquel vous prévoyez d’ajouter le nouveau type de données, soit en sélectionnant un schéma existant dans l’onglet **[!UICONTROL Parcourir]** , soit en créant un nouveau schéma entièrement.

Une fois le schéma ouvert dans le [!DNL Schema Editor]menu, sélectionnez le mixin auquel vous souhaitez ajouter le type de données dans le rail de gauche. Si le schéma ne dispose pas d&#39;un mixin approprié, suivez les étapes pour [créer un mixin](./create-schema-ui.md#define-mixin) à ajouter au schéma à la place, et assurez-vous que le mixin est sélectionné dans le rail de gauche.

![](../images/tutorials/create-datatype/mixin-selected.png)

Sélectionnez l’icône **plus (+)** en regard du nom du schéma pour ajouter un nouveau champ au mixin sélectionné. Lors de la sélection de la propriété **[!UICONTROL Type]** pour le champ, le nom du type de données créé précédemment est désormais disponible dans la liste déroulante. Vous pouvez début de saisir le nom du type de données pour faciliter sa localisation.

![](../images/tutorials/create-datatype/add-data-type.png)

Sélectionnez votre type de données dans la liste, puis sélectionnez **[!UICONTROL Appliquer]**. Le champ de schéma est mis à jour dans la trame pour afficher les sous-champs structurés fournis par le type de données. Si vous enregistrez le schéma en sélectionnant **[!UICONTROL Enregistrer]**, le mixin est également enregistré, ce qui vous permet de réutiliser le mixin dans d’autres schémas appartenant à la même classe.

![](../images/tutorials/create-datatype/data-type-added.png)

>[!NOTE]
>
>Les mixins ne sont compatibles qu&#39;avec une seule classe. Si vous souhaitez utiliser votre type de données dans des schémas supplémentaires basés sur différentes classes, vous devez suivre les étapes ci-dessus pour ajouter le type de données à d&#39;autres mixins destinés à étendre ces classes.

## Étapes suivantes

Ce didacticiel explique comment créer et modifier des types de données et comment les ajouter à des mixins à l’aide de la [!DNL Schema Editor]. Pour en savoir plus sur l’utilisation des types de données dans l’interface utilisateur, y compris sur la conversion d’un objet à champs multiples en type de données, consultez le didacticiel [sur la création de](./create-schema-ui.md#datatype)schémas.

Pour savoir comment créer un type de données à l&#39;aide de l&#39;API de Schéma Registry, consultez le guide [des points de terminaison des types de](../api/data-types.md#create)données.
---
keywords: Experience Platform;accueil;rubriques populaires;ui;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre des schémas;schéma;schéma;schémas;schémas;créer;type de données;types de données;types de données;schéma;schéma
solution: Experience Platform
title: Création et modification de types de données à l’aide de l’interface utilisateur
topic-legacy: tutorial
type: Tutorial
description: Découvrez comment créer et modifier des types de données dans l’interface utilisateur de l’Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 14128b247b003a54cb0d91167bb46fccf16ed799
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# Création et modification de types de données à l’aide de l’interface utilisateur

Dans le modèle de données d’expérience (XDM), les types de données sont des champs réutilisables qui contiennent plusieurs sous-champs. Bien que semblables aux groupes de champs de schéma dans le sens où ils permettent l’utilisation cohérente d’une structure à plusieurs champs, les types de données sont plus flexibles car ils peuvent être inclus n’importe où dans la structure de schéma alors que les groupes de champs ne peuvent être ajoutés qu’au niveau racine.

Adobe Experience Platform fournit de nombreux types de données standard qui peuvent être utilisés pour couvrir un large éventail de cas d’utilisation courants de la gestion de l’expérience. Cependant, vous pouvez également définir vos propres types de données personnalisés afin de répondre à vos besoins professionnels uniques.

Ce tutoriel décrit les étapes de création et de modification des types de données personnalisés dans l’interface utilisateur de Platform.

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et les [bases de la composition des schémas](../../schema/composition.md) pour la manière dont les types de données contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) afin de vous familiariser avec les différentes fonctionnalités de [!DNL Schema Editor].

## Ouvrez le [!DNL Schema Editor] pour un type de données.

Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Schémas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Schémas], puis sélectionnez l’onglet **[!UICONTROL Types de données]**. Une liste des types de données disponibles s’affiche, y compris ceux définis par Adobe et ceux créés par votre organisation.

![](../../images/ui/resources/data-types/data-types-tab.png)

Vous disposez de deux options :

- [Création d’un type de données](#create)
- [Sélectionner un type de données existant à modifier](#edit)

### Création d’un type de données {#create}

Dans l’onglet **[!UICONTROL Types de données]**, sélectionnez **[!UICONTROL Créer un type de données]**.

![](../../images/ui/resources/data-types/create.png)

[!DNL Schema Editor] s’affiche, indiquant la structure actuelle du nouveau type de données dans la zone de travail. Dans la partie droite de l’éditeur, vous pouvez indiquer un nom d’affichage et une description facultative du type de données. Veillez à fournir un nom unique et concis pour votre type de données, car c’est ainsi qu’il sera identifié lors de son ajout à un schéma.

Ce tutoriel crée un type de données qui décrit une propriété &quot;restaurant&quot;, de sorte que le type de données se voit attribuer un nom d’affichage &quot;Restaurant&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

À partir de là, vous pouvez passer à la [section suivante](#add-fields) pour commencer à ajouter des champs au nouveau type de données.

### Modification d’un type de données existant

>[!NOTE]
>
>Une fois qu’un type de données existant est utilisé dans un schéma qui a été activé pour une utilisation dans Real-time Customer Profile, seules des modifications non destructives peuvent être apportées par la suite à ce type de données. Pour plus d’informations, consultez les [règles de l’évolution du schéma](../../schema/composition.md#evolution) .

Seuls les types de données personnalisés définis par votre organisation peuvent être modifiés. Pour réduire la liste affichée, sélectionnez l’icône de filtre (![Icône Filtrer](../../images/ui/resources/data-types/filter.png)) afin d’afficher les contrôles pour le filtrage en fonction de [!UICONTROL Propriétaire]. Sélectionnez **[!UICONTROL Client]** pour afficher uniquement les types de données personnalisés appartenant à votre organisation.

Sélectionnez le type de données à modifier dans la liste pour ouvrir le rail de droite, en affichant les détails du type de données. Sélectionnez le nom du type de données dans le rail de droite pour ouvrir sa structure dans la balise [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Ajouter des champs au type de données {#add-fields}

Pour commencer à ajouter des champs au type de données, sélectionnez l’icône **plus (+)** en regard du champ de niveau racine dans la zone de travail. Un nouveau champ s’affiche en dessous et le rail de droite se met à jour pour afficher les commandes du nouveau champ.

![](../../images/ui/resources/data-types/new-field.png)

Utilisez les commandes du rail de droite pour configurer les détails du nouveau champ. Consultez le guide sur la [définition des champs dans l’interface utilisateur](../fields/overview.md#define) pour obtenir des instructions spécifiques sur la configuration et l’ajout du champ au type de données.

Le type de données Restaurant nécessite un champ de chaîne pour représenter le nom du restaurant. Par conséquent, le [!UICONTROL nom du champ] est défini comme &quot;name&quot; et le [!UICONTROL type] est défini comme &quot;[!UICONTROL chaîne]&quot;. Sélectionnez **[!UICONTROL Appliquer]** pour appliquer les modifications au champ.

![](../../images/ui/resources/data-types/name-field.png)

Continuez à ajouter d’autres champs au type de données selon vos besoins. L’exemple de type de données Restaurant comporte désormais des champs supplémentaires pour la marque, la capacité de sièges et l’espace de plancher.

![](../../images/ui/resources/data-types/more-fields.png)

Outre les champs de base, vous pouvez imbriquer des types de données supplémentaires dans votre type de données personnalisé. Par exemple, le type de données Restaurant nécessite un champ qui représente l’adresse physique de la propriété. Dans ce scénario, vous pouvez ajouter un nouveau champ &quot;adresse&quot; auquel est affecté le type de données standard &quot;[!UICONTROL Adresse postale]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Cela montre à quel point les types de données peuvent être flexibles pour décrire vos données : Les types de données peuvent utiliser des champs qui sont également des types de données, qui peuvent eux-mêmes contenir d’autres types de données, etc. Vous pouvez ainsi abstraire et réutiliser des modèles de données courants dans vos schémas XDM, ce qui facilite la représentation de structures de données complexes.

Une fois que vous avez terminé d’ajouter des champs au type de données, sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer vos modifications et ajouter le type de données au [!DNL Schema Library].

## Ajouter le type de données à une classe ou à un groupe de champs

Une fois que vous avez créé un type de données, vous pouvez commencer à l’utiliser dans vos schémas. Les schémas XDM étant composés d’une classe et de zéro ou plusieurs groupes de champs, les champs fournis par un type de données ne peuvent pas être ajoutés directement à un schéma. Ils doivent être inclus dans une classe ou un groupe de champs.

Commencez par suivre la procédure d’[ajout d’un champ à une classe](./classes.md#add-fields) ou [ajout d’un champ à un groupe de champs](./field-groups.md#add-fields). Lorsque vous choisissez **[!UICONTROL Type]** pour le nouveau champ, sélectionnez le nom de votre type de données dans le menu déroulant.

## Conversion d’un objet à plusieurs champs en un type de données {#convert}

Lorsque vous créez un champ de type objet avec plusieurs sous-champs dans la balise [!DNL Schema Editor], vous pouvez convertir ce champ en un type de données afin d’utiliser la même structure de champ dans une autre classe ou groupe de champs.

Pour convertir un champ de type objet en type de données, sélectionnez le champ dans la zone de travail. Avant de convertir le champ, assurez-vous que le **[!UICONTROL nom d’affichage]** est descriptif des données que l’objet contiendra, car il deviendra le nom du type de données. Lorsque vous êtes prêt à convertir le champ, sélectionnez **[!UICONTROL Convertir en nouveau type de données]** dans le rail de droite.

![](../../images/ui/resources/data-types/convert-object.png)

Le canevas met à jour le type de données du champ de &quot;[!UICONTROL Objet]&quot; vers le nouveau type de données. Les sous-champs comportent également de petites icônes de verrouillage, indiquant qu’ils ne sont plus des champs individuels, mais qu’ils font partie d’un type de données à champs multiples. Cette structure peut désormais être réutilisée dans d’autres classes et groupes de champs en sélectionnant ce type de données dans la liste déroulante **[!UICONTROL Type]** lors de la définition d’un nouveau champ.

![](../../images/ui/resources/data-types/converted.png)

## Étapes suivantes

Ce guide explique comment créer et modifier des types de données à l’aide de l’interface utilisateur de Platform. Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

Pour savoir comment gérer les types de données à l’aide de l’API [!DNL Schema Registry], consultez le [guide de point de terminaison des types de données](../../api/data-types.md).

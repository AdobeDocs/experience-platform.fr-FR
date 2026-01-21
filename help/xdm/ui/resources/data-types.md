---
keywords: Experience Platform;accueil;rubriques les plus consultées;iu;XDM;système XDM;modèle de données d’expérience;modèle de données d’expérience;modèle de données d’expérience;modèle de données;modèle de données;registre de schémas;registre de schémas;schéma;schémas;schémas;créer;type de données;types de données;
solution: Experience Platform
title: Créer et modifier des types de données à l’aide de l’interface utilisateur
type: Tutorial
description: Découvrez comment créer et modifier des types de données dans l’interface utilisateur Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 7%

---

# Créer et modifier des types de données à l’aide de l’interface d’utilisation {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Filtre de type de données standard ou personnalisé"
>abstract="La liste des types de données disponibles est préfiltrée en fonction de la manière dont ils ont été créés. Sélectionnez le bouton radio pour choisir entre les options Standard et Personnalisé. L’option Standard affiche les entités créées par Adobe et l’option Personnalisé affiche les entités créées au sein de votre organisation. Consultez la documentation pour en savoir plus sur la création et la modification des types de données."

Dans le modèle de données d’expérience (XDM), les types de données sont des champs réutilisables qui contiennent plusieurs sous-champs. Bien qu’ils soient similaires aux groupes de champs de schéma en ce qu’ils permettent l’utilisation cohérente d’une structure à champs multiples, les types de données sont plus flexibles, car ils peuvent être inclus n’importe où dans la structure du schéma, tandis que les groupes de champs ne peuvent être ajoutés qu’au niveau racine.

Adobe Experience Platform fournit de nombreux types de données standard qui peuvent être utilisés pour couvrir un large éventail de cas d’utilisation courants de la gestion de l’expérience. Cependant, vous pouvez également définir vos propres types de données personnalisés afin de répondre aux besoins spécifiques de votre entreprise.

>[!NOTE]
>
>Si un champ est défini comme un type de données spécifique, vous ne pouvez pas créer le même champ avec un type de données différent dans un autre schéma. Cette contrainte s’applique à l’ensemble du client de votre organisation.

Ce tutoriel décrit les étapes à suivre pour créer et modifier des types de données personnalisés dans l’interface utilisateur d’Experience Platform.

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une introduction au rôle de XDM dans l’écosystème Experience Platform et aux [principes de base de la composition des schémas](../../schema/composition.md) pour savoir comment les types de données contribuent aux schémas XDM.

Bien que cela ne soit pas obligatoire pour ce guide, il est recommandé de suivre également le tutoriel sur [la composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités de l’[!DNL Schema Editor].

## Ouvrir le [!DNL Schema Editor] pour un type de données {#data-type}

Dans l’interface utilisateur d’Experience Platform, sélectionnez **[!UICONTROL Schemas]** dans le volet de navigation de gauche pour ouvrir l’espace de travail [!UICONTROL Schemas], puis sélectionnez l’onglet **[!UICONTROL Data types]** . Une liste des types de données disponibles s’affiche. La liste des types de données est automatiquement filtrée en fonction de leur création. Le paramètre par défaut affiche les types de données définis par Adobe. Vous pouvez également filtrer la liste pour afficher celles créées par votre organisation.

![Espace de travail [!UICONTROL Schemas] avec [!UICONTROL Schemas] dans le volet de navigation de gauche et [!UICONTROL Data types] mis en surbrillance.](../../images/ui/resources/data-types/data-types-tab.png)

À partir de là, vous disposez des options suivantes :

- [Créer un nouveau type de données](#create)
- [Filtrer les types de données](#filter)
- [Sélectionner un type de données existant à modifier](#edit)

### Créer un nouveau type de données {#create}

Dans l’onglet **[!UICONTROL Data types]** , sélectionnez **[!UICONTROL Create data type]**.

![Onglet [!UICONTROL Schemas] de l’espace de travail [!UICONTROL Data types] avec le [!UICONTROL Create data type] en surbrillance.](../../images/ui/resources/data-types/create.png)

La [!DNL Schema Editor] s’affiche, affichant la structure actuelle du nouveau type de données dans la zone de travail. Dans la partie droite de l’éditeur, vous pouvez fournir un nom d’affichage et une description facultative du type de données. Veillez à fournir un nom unique et concis pour votre type de données, car c’est ainsi qu’il sera identifié lors de son ajout à un schéma.

Ce tutoriel crée un type de données qui décrit une propriété de restaurant. Le nom d’affichage « Restaurant » est donc attribué au type de données.

![](../../images/ui/resources/data-types/data-type-properties.png)

À partir de là, vous pouvez passer à la [section suivante](#add-fields) pour commencer à ajouter des champs au nouveau type de données.

### Filtrer les types de données {#filter}

La liste des types de données disponibles est préfiltrée en fonction de la manière dont ils ont été créés. Sélectionnez le bouton radio pour choisir entre les options [!UICONTROL Standard] et [!UICONTROL Custom]. L’option [!UICONTROL Standard] affiche les entités créées par Adobe et l’option [!UICONTROL Custom] affiche les entités créées au sein de votre organisation.

![Onglet [!UICONTROL Data types] de l’espace de travail [!UICONTROL Schemas] avec [!UICONTROL Standard] et [!UICONTROL Custom] en surbrillance.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Modifier un type de données existant {#edit}

>[!NOTE]
>
>Une fois qu’un type de données existant est utilisé dans un schéma qui a été activé pour une utilisation dans le profil client en temps réel, seules des modifications non destructives peuvent être apportées à ce type de données par la suite. Pour plus d’informations, consultez la section [règles d’évolution des schémas](../../schema/composition.md#evolution) .

Seuls les types de données personnalisés définis par votre organisation peuvent être modifiés. Sélectionnez **[!UICONTROL Custom]** pour afficher uniquement les types de données personnalisés détenus par votre organisation.

Sélectionnez le type de données à modifier dans la liste pour ouvrir le rail de droite, qui affiche les détails du type de données. Dans le panneau des détails, vous pouvez également télécharger un exemple de fichier, copier la structure JSON ou ajouter le type de données à un package.

Sélectionnez le nom du type de données dans le rail de droite pour ouvrir sa structure dans le [!DNL Schema Editor].

![Onglet [!UICONTROL Data types] de l’espace de travail [!UICONTROL Schemas], avec un type de données, [!UICONTROL Custom] et le type de données [!UICONTROL Name] mis en surbrillance.](../../images/ui/resources/data-types/edit.png)

## Ajouter des champs au type de données {#add-fields}

Pour commencer à ajouter des champs au type de données, sélectionnez l’icône **plus (+)** à côté du champ de niveau racine dans la zone de travail. Un nouveau champ s’affiche sous et le rail de droite se met à jour pour afficher les commandes du nouveau champ.

![](../../images/ui/resources/data-types/new-field.png)

Utilisez les commandes du rail de droite pour configurer les détails du nouveau champ. Consultez le guide sur la [définition de champs dans l’interface utilisateur](../fields/overview.md#define) pour obtenir des instructions spécifiques sur la configuration et l’ajout du champ au type de données.

Le type de données Restaurant nécessite un champ de chaîne pour représenter le nom du restaurant. Par conséquent, le [!UICONTROL Field name] est défini sur « nom » et le [!UICONTROL Type] est défini sur « [!UICONTROL String] ». Sélectionnez **[!UICONTROL Apply]** pour appliquer les modifications au champ.

![](../../images/ui/resources/data-types/name-field.png)

Continuez à ajouter d’autres champs au type de données selon vos besoins. L’exemple de type de données Restaurant comporte désormais des champs supplémentaires pour la marque, la capacité de la salle et l’espace au sol.

![](../../images/ui/resources/data-types/more-fields.png)

Outre les champs de base, vous pouvez également imbriquer des types de données supplémentaires dans votre type de données personnalisé. Par exemple, le type de données Restaurant nécessite un champ qui représente l’adresse physique de la propriété. Dans ce scénario, vous pouvez ajouter un nouveau champ « adresse » auquel est affecté le type de données standard « [!UICONTROL Postal address] ».

![](../../images/ui/resources/data-types/address-field.png)

Cela montre à quel point les types de données peuvent être flexibles pour décrire vos données : les types de données peuvent utiliser des champs qui sont également des types de données, qui peuvent eux-mêmes contenir d’autres types de données, etc. Vous pouvez ainsi abstraire et réutiliser des modèles de données courants dans vos schémas XDM, ce qui facilite la représentation de structures de données complexes.

Une fois que vous avez terminé d’ajouter des champs au type de données, sélectionnez **[!UICONTROL Save]** pour enregistrer vos modifications et ajouter le type de données au [!DNL Schema Library].

## Ajouter le type de données à un schéma {#add-data-type}

Une fois que vous avez créé un type de données, vous pouvez commencer à l’utiliser dans vos schémas. Étant donné que les schémas XDM sont composés d’une classe et de zéro ou plusieurs groupes de champs, les champs fournis par un type de données ne peuvent pas être ajoutés directement à un schéma. Au lieu de cela, ils doivent être inclus dans une classe ou un groupe de champs.

Commencez par suivre les étapes liées à [l’ajout d’un champ à une classe](./classes.md#add-fields) ou [l’ajout d’un champ à un groupe de champs](./field-groups.md#add-fields). Vous pouvez également commencer [à ajouter directement un champ à un schéma](./schemas.md#add-individual-fields) et choisir la classe ou le groupe de champs parent à partir de là. Lorsque vous choisissez la **[!UICONTROL Type]** du nouveau champ, sélectionnez le nom de votre type de données dans le menu déroulant.

## Conversion d’un objet à plusieurs champs en un type de données {#convert}

Lorsque vous créez un champ de type objet avec plusieurs sous-champs dans le [!DNL Schema Editor], vous pouvez convertir ce champ en un type de données afin d’utiliser la même structure de champ dans une classe ou un groupe de champs différent.

Pour convertir un champ de type objet en un type de données, sélectionnez le champ dans la zone de travail. Avant de convertir le champ, assurez-vous que le **[!UICONTROL Display name]** est descriptif des données que l’objet contiendra, car il deviendra le nom du type de données. Lorsque vous êtes prêt à convertir le champ, sélectionnez **[!UICONTROL Convert to new data type]** dans le rail de droite.

![](../../images/ui/resources/data-types/convert-object.png)

La zone de travail met à jour le type de données du champ de « [!UICONTROL Object] » vers le nouveau type de données. Cette structure peut désormais être réutilisée dans d’autres classes et groupes de champs en sélectionnant ce type de données dans la liste déroulante **[!UICONTROL Type]** lors de la définition d’un nouveau champ.

![](../../images/ui/resources/data-types/converted.png)

## Étapes suivantes {#next-steps}

Ce guide explique comment créer et modifier des types de données à l’aide de l’interface utilisateur d’Experience Platform. Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schemas], consultez la présentation de l’espace de travail [[!UICONTROL Schemas]](../overview.md).

Pour savoir comment gérer les types de données à l’aide de l’API [!DNL Schema Registry], consultez le guide de point d’entrée [types de données](../../api/data-types.md).

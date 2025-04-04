---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;interface utilisateur;espace de travail;champ;
solution: Experience Platform
title: Définir des champs XDM dans l’interface utilisateur
description: Découvrez comment définir des champs XDM dans l’interface utilisateur Experience Platform.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 1%

---

# Définir des champs XDM dans l’interface utilisateur

L’[!DNL Schema Editor] de l’interface utilisateur de Adobe Experience Platform vous permet de définir vos propres champs dans les classes et groupes de champs de schéma du modèle de données d’expérience (XDM) personnalisé. Ce guide décrit les étapes de définition des champs XDM dans l’interface utilisateur, y compris les options de configuration disponibles pour chaque type de champ.

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une introduction au rôle de XDM dans l’écosystème Experience Platform et aux [principes de base de la composition des schémas](../../schema/composition.md) afin de découvrir comment les classes et les groupes de champs contribuent aux champs des schémas XDM.

Bien que cela ne soit pas obligatoire pour ce guide, il est recommandé de suivre également le tutoriel sur [la composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités de l’[!DNL Schema Editor].

## Sélectionner une ressource à laquelle ajouter des champs {#select-resource}

Pour définir de nouveaux champs XDM dans l’interface utilisateur, vous devez d’abord ouvrir un schéma dans le [!DNL Schema Editor] . Selon les schémas actuellement disponibles dans le [!DNL Schema Library], vous pouvez choisir de [créer un schéma](../resources/schemas.md#create) ou [sélectionner un schéma existant à modifier](../resources/schemas.md#edit).

Une fois le [!DNL Schema Editor] ouvert, les commandes permettant d’ajouter des champs s’affichent dans la zone de travail. Ces commandes s’affichent en regard du nom du schéma, ainsi que des champs de type objet qui ont été définis sous la classe ou le groupe de champs sélectionné.

![Éditeur de schémas avec les icônes d’ajout mises en surbrillance.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Si vous tentez d’ajouter un champ à un objet fourni par un groupe de champs standard, ce groupe de champs est converti en groupe de champs personnalisés et le groupe de champs d’origine n’est plus disponible. Pour plus d’informations, consultez la section sur [l’ajout de champs à des groupes de champs standard](../resources/schemas.md#custom-fields-for-standard-groups) dans le guide de l’interface utilisateur des schémas .

Pour ajouter un nouveau champ à la ressource, sélectionnez l’icône **plus (+)** en regard du nom du schéma dans la zone de travail, ou en regard du champ de type d’objet sous lequel vous souhaitez définir le champ.

![L’éditeur de schémas avec une icône d’ajout mise en surbrillance.](../../images/ui/fields/overview/plus-icon.png)

Selon que vous ajoutez directement un champ à un schéma ou à sa classe et à ses groupes de champs constitutifs, les étapes requises pour ajouter le champ varient. Le reste de ce document se concentre sur la configuration des propriétés d’un champ, quel que soit l’emplacement de ce champ dans le schéma. Pour plus d’informations sur les différentes manières dont les champs peuvent être ajoutés à un schéma, reportez-vous aux sections suivantes du guide de l’interface utilisateur des schémas :

* [Ajouter des champs à des groupes de champs](../resources/schemas.md#add-fields)
* [Ajout direct de champs à un schéma](../resources/schemas.md#add-individual-fields)

## Définition des propriétés d’un champ {#define}

Après avoir sélectionné l’icône **plus (+)** un espace réservé **[!UICONTROL Champ sans titre]** s’affiche dans la zone de travail.

![L’éditeur de schémas avec un nouveau champ sans titre mis en surbrillance.](../../images/ui/fields/overview/new-field.png)

Dans le rail de droite sous **[!UICONTROL Propriétés du champ]**, vous pouvez configurer les détails du nouveau champ. Les informations suivantes sont requises pour chaque champ :

| Propriété du champ | Description |
| --- | --- |
| [!UICONTROL Nom du champ] | Nom unique et descriptif pour le champ. Notez que le nom du champ ne peut pas être modifié une fois le schéma enregistré. Cette valeur est utilisée pour identifier et référencer le champ dans le code et dans d’autres applications en aval<br><br>Le nom doit idéalement être écrit en CamelCase. Il peut contenir des caractères alphanumériques ou des traits de soulignement, mais il **peut pas** commencer par un trait de soulignement.<ul><li>**Correct** : `fieldName`</li><li>**Acceptable :** `field_name2`, `fieldName_3`</li><li>**Incorrect** : `_fieldName`</li></ul> |
| [!UICONTROL Nom d’affichage] | Nom d’affichage du champ. Il s’agit du nom qui sera utilisé pour représenter le champ dans la zone de travail de l’éditeur de schémas. Le nom du champ peut être remplacé par le nom d’affichage à l’aide du bouton [bascule du nom d’affichage](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Type] | Type de données que le champ contiendra. Dans ce menu déroulant, vous pouvez sélectionner l’un des [types scalaires standard](../../schema/field-constraints.md) pris en charge par XDM, ou l’un des [types de données](../resources/data-types.md) à champs multiples précédemment définis dans le [!DNL Schema Registry].<br>Remarque : si vous sélectionnez le type de données Mappage, la propriété [!UICONTROL Type de valeur de mappage] s’affiche.<br><br>Vous pouvez également sélectionner **[!UICONTROL Recherche avancée de type]** pour rechercher et filtrer les types de données existants et localiser plus facilement le type souhaité. |
| [!UICONTROL Mapper le type de valeur] | Cette valeur est requise si vous sélectionnez [!UICONTROL Mapper] comme type de données pour le champ. Les valeurs disponibles pour le mappage sont [!UICONTROL Chaîne] et [!UICONTROL Entier]. Sélectionnez une valeur dans la liste déroulante des options disponibles.<br>Pour en savoir plus sur les [propriétés de champ spécifiques à un type](#type-specific-properties), consultez la présentation de la définition des champs . |

{style="table-layout:auto"}

Vous pouvez également choisir de fournir une description et des notes pour chaque champ. Utilisez le champ **[!UICONTROL Description]** pour ajouter du contexte et décrire les fonctionnalités du type de données de mappage. Cela contribue à la facilité de maintenance et à la lisibilité de la mise en œuvre. Vous pouvez également ajouter des notes pour compléter la description initiale. Cela devrait offrir des informations plus granulaires et plus spécifiques pour aider les développeurs à comprendre, à gérer et à utiliser la carte efficacement dans le contexte de la base de code. |


>[!NOTE]
>
>Selon le **[!UICONTROL Type]** que vous avez sélectionné pour le champ, des commandes de configuration supplémentaires peuvent apparaître dans le rail de droite. Pour plus d’informations sur ces commandes, consultez la section sur les [propriétés de champ spécifiques à un type](#type-specific-properties).
>
>Le rail de droite fournit également des cases à cocher pour désigner des types de champs spéciaux. Pour plus d’informations, consultez la section sur les [types de champs spéciaux](#special).

Une fois le champ configuré, sélectionnez **[!UICONTROL Appliquer]**.

![La section [!UICONTROL Propriétés du champ] de l’éditeur de schémas est mise en surbrillance.](../../images/ui/fields/overview/field-details.png)

La zone de travail se met à jour pour afficher le champ nouvellement ajouté, situé dans un objet dont l’espace de noms est associé à votre identifiant de client unique (illustré comme `_tenantId` dans l’exemple ci-dessous). Tous les champs personnalisés ajoutés à un schéma sont automatiquement placés dans cet espace de noms afin d’éviter tout conflit avec d’autres champs des classes et groupes de champs fournis par Adobe. Le rail de droite répertorie désormais le chemin d’accès au champ en plus de ses autres propriétés.

![Un nouveau champ dans le diagramme de schéma et son chemin d’accès correspondant dans la section [!UICONTROL Propriétés du champ] sont mis en surbrillance.](../../images/ui/fields/overview/field-added.png)

Vous pouvez continuer à suivre les étapes ci-dessus pour ajouter d’autres champs au schéma. Une fois le schéma enregistré, sa classe de base et ses groupes de champs sont également enregistrés si des modifications y ont été apportées.

>[!NOTE]
>
>Toute modification apportée aux groupes de champs ou à la classe d’un schéma est répercutée dans tous les autres schémas qui les utilisent.

## Propriétés de champ spécifiques au type {#type-specific-properties}

Lors de la définition d’un nouveau champ, des options de configuration supplémentaires peuvent apparaître dans le rail de droite selon le **[!UICONTROL Type]** que vous choisissez pour le champ. Le tableau suivant décrit ces propriétés de champ supplémentaires, ainsi que leurs types compatibles :

| Propriété du champ | Types compatibles | Description |
| --- | --- | --- |
| [!UICONTROL Mapper le type de valeur] | [!UICONTROL Carte] | La propriété [!UICONTROL Type de valeur de mappage] n’apparaît dans l’interface utilisateur que si vous sélectionnez la valeur de mappage dans les options déroulantes [!UICONTROL Type]. Vous pouvez choisir entre les types de valeur Chaîne et Entier pour le mappage.<br>![ L’éditeur de schémas avec les champs de type Type et Valeur map mis en surbrillance.](../../images/ui/fields/overview/map-type.png " L’éditeur de schémas avec les champs de type Type et Valeur map mis en surbrillance."){width="100" zoomable="yes"}<br>Remarque : tous les types de données de mappage créés par le biais de l’API qui ne sont pas de type String ou Integer s’affichent sous la forme d’un type de données « [!UICONTROL Complex] ». Vous ne pouvez pas créer de types de données « [!UICONTROL Complexes] » via l’interface utilisateur. |
| [!UICONTROL Motif] | [!UICONTROL Chaîne] | Une [expression régulière](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) à laquelle la valeur de ce champ doit se conformer pour être acceptée lors de l’ingestion. |
| [!UICONTROL Format] | [!UICONTROL Chaîne] | Effectuez une sélection dans une liste de formats prédéfinis pour les chaînes auxquelles la valeur doit se conformer. Les formats disponibles sont les suivants : <ul><li>[[!UICONTROL date-heure]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL nom d’hôte]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL modèle-url]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL pointeur-json]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Longueur minimale] | [!UICONTROL Chaîne] | Nombre minimum de caractères que la chaîne doit contenir pour que la valeur soit acceptée lors de l’ingestion. |
| [!UICONTROL Longueur maximale] | [!UICONTROL Chaîne] | Nombre maximal de caractères que la chaîne doit contenir pour que la valeur soit acceptée lors de l’ingestion. |
| [!UICONTROL Valeur minimale] | [!UICONTROL Double] | Valeur minimale pour que le doublon soit accepté lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l’utilisation de cette contrainte, la contrainte « [!UICONTROL Valeur minimale exclusive] » doit rester vide. |
| [!UICONTROL Valeur maximale] | [!UICONTROL Double] | Valeur maximale de Double à accepter lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l’utilisation de cette contrainte, la contrainte « [!UICONTROL Valeur maximale exclusive] » doit rester vide. |
| [!UICONTROL Valeur minimale exclusive] | [!UICONTROL Double] | Valeur maximale de Double à accepter lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, elle est rejetée. Lors de l’utilisation de cette contrainte, la contrainte « [!UICONTROL Valeur minimale] » (non exclusive) doit rester vide. |
| [!UICONTROL Valeur maximale exclusive] | [!UICONTROL Double] | Valeur maximale de Double à accepter lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, elle est rejetée. Lors de l’utilisation de cette contrainte, la contrainte « [!UICONTROL Valeur maximale] » (non exclusive) doit rester vide. |

{style="table-layout:auto"}

## Types de champs spéciaux {#special}

Le rail de droite propose plusieurs cases à cocher pour désigner des rôles spéciaux pour le champ sélectionné. Les cas d’utilisation de certaines de ces options impliquent des considérations importantes concernant votre stratégie de modélisation des données et la manière dont vous avez l’intention d’utiliser les services Experience Platform en aval.

Pour en savoir plus sur ces types spéciaux, consultez la documentation suivante :

* [Carte](./map.md)
* [[!UICONTROL Obligatoire]](./required.md)
* [[!UICONTROL Tableau]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identité]](./identity.md) (disponible uniquement pour les champs de chaîne)
* [[!UICONTROL Relation]](./relationship.md) (disponible uniquement pour les champs de chaîne)

Bien que techniquement il ne s’agisse pas d’un type de champ spécial, il est également recommandé de consulter le guide sur la [définition de champs de type objet](./object.md) pour en savoir plus sur la définition de sous-champs imbriqués dans vos structures de schéma.

## Étapes suivantes

Ce guide présente un aperçu de la définition des champs XDM dans l’interface utilisateur. N’oubliez pas que les champs ne peuvent être ajoutés aux schémas que par le biais de classes et de groupes de champs. Pour en savoir plus sur la gestion de ces ressources dans l’interface utilisateur, consultez les guides sur la création et la modification de [classes](../resources/classes.md) et de [groupes de champs](../resources/field-groups.md).

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la présentation de l’espace de travail [[!UICONTROL Schémas]](../overview.md).

---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;champ;
solution: Experience Platform
title: Définition des champs XDM dans l’interface utilisateur
description: Découvrez comment définir des champs XDM dans l’interface utilisateur de l’Experience Platform.
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 89519918aa830dc09365fa80449099229dc475d5
workflow-type: tm+mt
source-wordcount: '1734'
ht-degree: 1%

---

# Définition des champs XDM dans l’interface utilisateur

L’ [!DNL Schema Editor] de l’interface utilisateur de Adobe Experience Platform vous permet de définir vos propres champs dans les classes XDM (Experience Data Model) personnalisées et les groupes de champs de schéma. Ce guide décrit les étapes de définition des champs XDM dans l’interface utilisateur, y compris les options de configuration disponibles pour chaque type de champ.

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et aux [ principes de base de la composition des schémas](../../schema/composition.md) pour apprendre comment les classes et les groupes de champs contribuent aux champs des schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les différentes fonctionnalités de [!DNL Schema Editor].

## Sélectionner une ressource à laquelle ajouter des champs {#select-resource}

Pour définir de nouveaux champs XDM dans l’interface utilisateur, vous devez d’abord ouvrir un schéma dans le [!DNL Schema Editor]. En fonction des schémas actuellement disponibles dans [!DNL Schema Library], vous pouvez choisir de [créer un nouveau schéma](../resources/schemas.md#create) ou de [sélectionner un schéma existant à modifier](../resources/schemas.md#edit).

Une fois que vous avez ouvert l’élément [!DNL Schema Editor], les commandes permettant d’ajouter des champs s’affichent dans la zone de travail. Ces commandes s’affichent en regard du nom du schéma, ainsi que des champs de type objet qui ont été définis sous la classe ou le groupe de champs sélectionné.

![ L’éditeur de schémas avec les icônes d’ajout surlignées.](../../images/ui/fields/overview/select-resource.png)

>[!WARNING]
>
>Si vous tentez d’ajouter un champ à un objet fourni par un groupe de champs standard, ce groupe sera converti en groupe de champs personnalisé et le groupe de champs d’origine ne sera plus disponible. Pour plus d’informations, consultez la section sur l’ [ajout de champs aux groupes de champs standard](../resources/schemas.md#custom-fields-for-standard-groups) dans le guide de l’interface utilisateur des schémas.

Pour ajouter un nouveau champ à la ressource, sélectionnez l’icône **plus (+)** en regard du nom du schéma dans la zone de travail ou en regard du champ de type objet sous lequel vous souhaitez définir le champ.

![ L’éditeur de schémas avec une icône d’ajout mise en surbrillance.](../../images/ui/fields/overview/plus-icon.png)

Selon que vous ajoutez directement un champ à un schéma ou à sa classe constituante et à ses groupes de champs, les étapes requises pour ajouter le champ varient. Le reste de ce document se concentre sur la configuration des propriétés d’un champ, quel que soit l’endroit où ce champ apparaît dans le schéma. Pour plus d’informations sur les différentes manières d’ajouter des champs à un schéma, reportez-vous aux sections suivantes du guide de l’interface utilisateur des schémas :

* [Ajouter des champs aux groupes de champs](../resources/schemas.md#add-fields)
* [Ajout direct de champs à un schéma](../resources/schemas.md#add-individual-fields)

## Définition des propriétés d’un champ {#define}

Après avoir sélectionné l’icône **plus (+)** , un espace réservé **[!UICONTROL Champ sans titre]** s’affiche dans la zone de travail.

![L’éditeur de schémas avec un nouveau champ sans titre en surbrillance.](../../images/ui/fields/overview/new-field.png)

Dans le rail de droite sous **[!UICONTROL Propriétés du champ]**, vous pouvez configurer les détails du nouveau champ. Les informations suivantes sont requises pour chaque champ :

| Propriété du champ | Description |
| --- | --- |
| [!UICONTROL Nom du champ] | Nom descriptif et unique du champ. Notez que le nom du champ ne peut pas être modifié une fois le schéma enregistré. Cette valeur est utilisée pour identifier et référencer le champ dans le code et dans d’autres applications en aval<br><br>Le nom doit idéalement être écrit en CamelCase. Il peut contenir des caractères alphanumériques, des tirets ou des traits de soulignement, mais **ne peut pas commencer par un trait de soulignement.**<ul><li>**Correct** : `fieldName`</li><li>**Acceptable :** `field_name2`, `Field-Name`, `field-name_3`</li><li>**Incorrect** : `_fieldName`</li></ul> |
| [!UICONTROL Nom d’affichage] | Nom d’affichage du champ. Il s’agit du nom qui sera utilisé pour représenter le champ dans le canevas de l’éditeur de schémas. Le nom du champ peut être remplacé par le nom d’affichage à l’aide du bouton [bascule du nom d’affichage](../resources/schemas.md#display-name-toggle). |
| [!UICONTROL Type] | Le type de données que le champ contiendra. Dans ce menu déroulant, vous pouvez sélectionner l’un des [types scalaires standard](../../schema/field-constraints.md) pris en charge par XDM, ou l’un des [types de données](../resources/data-types.md) à plusieurs champs précédemment définis dans [!DNL Schema Registry].<br>Remarque : Si vous sélectionnez le type de données Map , la propriété [!UICONTROL Type de valeur Map] s’affiche.<br><br>Vous pouvez également sélectionner **[!UICONTROL Recherche de type avancé]** pour rechercher et filtrer les types de données existants et localiser plus facilement le type souhaité. |
| [!UICONTROL Type de valeur de carte] | Cette valeur est requise si vous sélectionnez [!UICONTROL Map] comme type de données pour le champ. Les valeurs disponibles pour la carte sont [!UICONTROL String] et [!UICONTROL Integer]. Sélectionnez une valeur dans la liste déroulante des options disponibles.<br>Pour en savoir plus sur les [propriétés de champ spécifiques au type](#type-specific-properties), consultez la présentation de la définition des champs. |

{style="table-layout:auto"}

Vous pouvez également choisir de fournir une description et des notes pour chaque champ. Utilisez le champ **[!UICONTROL Description]** pour ajouter du contexte et décrire la fonctionnalité du type de données de carte. Cela contribue à la maintenabilité et à la lisibilité de la mise en oeuvre. Vous pouvez également ajouter des notes pour compléter la description initiale. Cela devrait offrir des informations plus granulaires et spécifiques pour aider les développeurs à comprendre, gérer et utiliser efficacement la carte dans le contexte du code base. |


>[!NOTE]
>
>Selon le **[!UICONTROL Type]** que vous avez sélectionné pour le champ, d’autres contrôles de configuration peuvent apparaître dans le rail de droite. Pour plus d’informations sur ces contrôles, consultez la section sur les [propriétés de champ spécifiques au type](#type-specific-properties) .
>
>Le rail de droite contient également des cases à cocher pour désigner les types de champ spéciaux. Pour plus d’informations, consultez la section sur les [types de champ spéciaux](#special) .

Une fois que vous avez terminé de configurer le champ, sélectionnez **[!UICONTROL Apply]**.

![La section [!UICONTROL Propriétés du champ] de l’éditeur de schémas est mise en surbrillance.](../../images/ui/fields/overview/field-details.png)

Le canevas se met à jour pour afficher le champ nouvellement ajouté, situé dans un espace de noms d’objet associé à votre identifiant de tenant unique (illustré par `_tenantId` dans l’exemple ci-dessous). Tous les champs personnalisés ajoutés à un schéma sont automatiquement placés dans cet espace de noms afin d’éviter tout conflit avec d’autres champs provenant de classes et de groupes de champs fournis par l’Adobe. Le rail de droite répertorie désormais le chemin d’accès du champ en plus de ses autres propriétés.

![Un nouveau champ dans le schéma et son chemin d’accès correspondant dans la section [!UICONTROL Propriétés du champ] est mis en surbrillance.](../../images/ui/fields/overview/field-added.png)

Vous pouvez continuer à suivre les étapes ci-dessus pour ajouter d’autres champs au schéma. Une fois le schéma enregistré, sa classe de base et ses groupes de champs sont également enregistrés si des modifications leur ont été apportées.

>[!NOTE]
>
>Toutes les modifications que vous apportez aux groupes de champs ou à la classe d’un schéma seront répercutées dans tous les autres schémas qui les utilisent.

## Propriétés de champ spécifiques à un type {#type-specific-properties}

Lors de la définition d’un nouveau champ, d’autres options de configuration peuvent s’afficher dans le rail de droite en fonction du **[!UICONTROL type]** que vous avez choisi pour le champ. Le tableau suivant décrit ces propriétés de champ supplémentaires, ainsi que leurs types compatibles :

| Propriété du champ | Types compatibles | Description |
| --- | --- | --- |
| [!UICONTROL Type de valeur de carte] | [!UICONTROL Carte] | La propriété [!UICONTROL Type de valeur de carte] apparaît uniquement dans l’interface utilisateur si vous sélectionnez la valeur de carte dans les options de liste déroulante [!UICONTROL Type]. Vous pouvez choisir entre les types de valeurs Chaîne et Entier pour la carte.<br>![L’éditeur de schémas avec les champs Type et Type de valeur de mappage mis en surbrillance.](../../images/ui/fields/overview/map-type.png "L’éditeur de schémas avec les champs Type et Type de valeur de mappage mis en surbrillance."){width="100" zoomable="yes"}<br>Remarque : tous les types de données de mappage créés par le biais de l’API qui ne sont pas de type Chaîne ou Entier sont affichés sous la forme d’un type de données &#39;[!UICONTROL Complex]&#39;. Vous ne pouvez pas créer de types de données &#39;[!UICONTROL Complex]&#39; via l’interface utilisateur. |
| [!UICONTROL Valeur par défaut] | [!UICONTROL Chaîne], [!UICONTROL Double], [!UICONTROL Long], [!UICONTROL Entier], [!UICONTROL Court], [!UICONTROL Octet], [!UICONTROL Booléen] | Valeur par défaut attribuée à ce champ si aucune autre valeur n’est fournie pendant l’ingestion. Cette valeur doit être conforme au type sélectionné du champ.<br><br>Les valeurs par défaut ne sont pas enregistrées dans le jeu de données au moment de l’ingestion, car elles peuvent changer au fil du temps. Les valeurs par défaut définies dans le schéma sont déduites par les services et applications Platform en aval lorsqu’ils lisent les données du jeu de données. Par exemple, lors de l’interrogation des données à l’aide de Query Service, si l’attribut a une valeur NULL, mais que la valeur par défaut est `5` au niveau du schéma, il est prévu que Query Service renvoie `5` au lieu de NULL. Notez que ce comportement n’est actuellement pas uniforme pour tous les services AEP. |
| [!UICONTROL Modèle] | [!UICONTROL Chaîne] | Une [expression régulière](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) à laquelle la valeur de ce champ doit être conforme pour être acceptée lors de l’ingestion. |
| [!UICONTROL Format] | [!UICONTROL Chaîne] | Effectuez une sélection dans une liste de formats prédéfinis pour les chaînes auxquelles la valeur doit se conformer. Les formats disponibles sont les suivants : <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-reference]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Longueur minimale] | [!UICONTROL Chaîne] | Nombre minimum de caractères que doit contenir la chaîne pour que la valeur soit acceptée lors de l’ingestion. |
| [!UICONTROL Longueur maximale] | [!UICONTROL Chaîne] | Nombre maximal de caractères que doit contenir la chaîne pour que la valeur soit acceptée lors de l’ingestion. |
| [!UICONTROL Valeur minimale] | [!UICONTROL Double] | Valeur minimale à accepter lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur minimale exclusive]&quot; doit être laissée vide. |
| [!UICONTROL Valeur maximale] | [!UICONTROL Double] | Valeur maximale que la Double doit être acceptée lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur maximale exclusive]&quot; doit être laissée vide. |
| [!UICONTROL Valeur minimale exclusive] | [!UICONTROL Double] | Valeur maximale que la Double doit être acceptée lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est rejetée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Minimum value]&quot; (non exclusive) doit être laissée vide. |
| [!UICONTROL Valeur maximale exclusive] | [!UICONTROL Double] | Valeur maximale que la Double doit être acceptée lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est rejetée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Maximum value]&quot; (non exclusive) doit être laissée vide. |

{style="table-layout:auto"}

## Types de champ spéciaux {#special}

Le rail de droite comporte plusieurs cases à cocher pour la désignation des rôles spéciaux pour le champ sélectionné. Les cas d’utilisation de certaines de ces options impliquent des considérations importantes concernant votre stratégie de modélisation des données et la manière dont vous envisagez d’utiliser les services Platform en aval.

Pour en savoir plus sur ces types spéciaux, consultez la documentation suivante :

* [Carte](./map.md)
* [[!UICONTROL Obligatoire]](./required.md)
* [[!UICONTROL Tableau]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identité]](./identity.md) (Disponible uniquement pour les champs de chaîne)
* [[!UICONTROL Relationship]](./relationship.md) (Disponible uniquement pour les champs de chaîne)

Bien que techniquement non un type de champ spécial, il est également recommandé de consulter le guide sur la [définition des champs de type objet](./object.md) pour en savoir plus sur la définition de sous-champs imbriqués dans vos structures de schéma.

## Étapes suivantes

Ce guide fournit un aperçu de la définition des champs XDM dans l’interface utilisateur. N’oubliez pas que les champs ne peuvent être ajoutés qu’aux schémas par l’utilisation de classes et de groupes de champs. Pour en savoir plus sur la gestion de ces ressources dans l’interface utilisateur, consultez les guides sur la création et la modification des [classes](../resources/classes.md) et des [groupes de champs](../resources/field-groups.md).

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

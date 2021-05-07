---
keywords: Experience Platform;accueil;rubriques populaires;api;API;XDM;XDM system;experience data model;ui;workspace;field;
solution: Experience Platform
title: Définition de champs XDM dans l’interface utilisateur
description: Découvrez comment définir des champs XDM dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '1325'
ht-degree: 4%

---

# Définition des champs XDM dans l’interface utilisateur

Le [!DNL Schema Editor] de l’interface utilisateur Adobe Experience Platform vous permet de définir vos propres champs dans les classes de modèle de données d’expérience (XDM) personnalisées et les groupes de champs de schéma. Ce guide décrit les étapes de définition des champs XDM dans l’interface utilisateur, y compris les options de configuration disponibles pour chaque type de champ.

## Conditions préalables  

Ce guide nécessite une bonne compréhension de XDM System. Pour une présentation du rôle de XDM au sein de l&#39;écosystème Experience Platform, voir [Présentation de XDM](../../home.md) et les [bases de la composition des schémas](../../schema/composition.md) pour savoir comment les classes et les groupes de champs contribuent aux schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur [la composition d&#39;un schéma dans l&#39;interface utilisateur](../../tutorials/create-schema-ui.md) pour vous familiariser avec les diverses fonctionnalités du [!DNL Schema Editor].

## Sélectionnez une ressource à laquelle ajouter des champs à {#select-resource}

Pour définir de nouveaux champs XDM dans l&#39;interface utilisateur, vous devez d&#39;abord ouvrir un schéma dans [!DNL Schema Editor]. Selon les schémas actuellement disponibles dans [!DNL Schema Library], vous pouvez choisir de [créer un nouveau schéma](../resources/schemas.md#create) ou [sélectionner un schéma existant à modifier](../resources/schemas.md#edit).

Une fois que [!DNL Schema Editor] est ouvert, utilisez le rail de gauche pour sélectionner la classe ou le groupe de champs pour lesquels vous souhaitez définir des champs. Si la ressource est une ressource personnalisée définie par votre organisation, les contrôles permettant d’ajouter ou de modifier des champs s’affichent dans la trame. Ces contrôles s&#39;affichent en regard du nom du schéma, ainsi que des champs de type objet définis sous la classe ou le groupe de champs sélectionné.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Si la classe ou le groupe de champs que vous sélectionnez est une ressource principale fournie par Adobe, il ne peut pas être modifié et les contrôles affichés ci-dessus n&#39;apparaîtront donc pas. Si le schéma auquel vous souhaitez ajouter des champs est basé sur une classe XDM de base et ne contient aucun groupe de champs personnalisé, vous pouvez [créer un nouveau groupe de champs](../resources/field-groups.md#create) à ajouter au schéma.

Pour ajouter un nouveau champ à la ressource, sélectionnez l&#39;icône **plus (+)** en regard du nom du schéma dans le canevas ou en regard du champ de type d&#39;objet sous lequel vous souhaitez définir le champ.

![](../../images/ui/fields/overview/plus-icon.png)

## Définir un champ pour une ressource {#define}

Après avoir sélectionné l&#39;icône **plus (+)**, un **[!UICONTROL nouveau champ]** apparaît dans le canevas, situé dans un objet de niveau racine qui porte l&#39;espace de noms de votre ID de client unique (comme `_tenantId` dans l&#39;exemple ci-dessous). Tous les champs ajoutés à un schéma par le biais de classes personnalisées et de groupes de champs sont automatiquement placés dans cet espace de nommage afin d’éviter les conflits avec d’autres champs provenant de classes et de groupes de champs fournis par l’Adobe.

![](../../images/ui/fields/overview/new-field.png)

Dans le rail de droite sous **[!UICONTROL Propriétés de champ]**, vous pouvez configurer les détails des nouveaux champs. Les informations suivantes sont requises pour chaque champ :

| Propriété de champ | Description |
| --- | --- |
| [!UICONTROL Nom du champ] | Nom unique et descriptif du champ. Notez que le nom du champ ne peut pas être modifié une fois le schéma enregistré.<br><br>Le nom devrait idéalement être écrit en cave à chameau. Il peut contenir des caractères alphanumériques, des tirets ou des traits de soulignement, mais **ne peut pas** début avec un trait de soulignement.<ul><li>**Correct** :  `fieldName`</li><li>**Acceptable:** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Incorrect** :  `_fieldName`</li></ul> |
| [!UICONTROL Nom d’affichage] | Nom convivial du champ. |
| [!UICONTROL Type] | Type de données que le champ contiendra. Dans ce menu déroulant, vous pouvez sélectionner l&#39;un des [types scalaires standard](../../schema/field-constraints.md) pris en charge par XDM, ou l&#39;un des types de données [à champs multiples ](../resources/data-types.md) qui ont été précédemment définis dans [!DNL Schema Registry].<br><br>Vous pouvez également sélectionner  **[!UICONTROL Recherche de type]** avancé pour rechercher et filtrer les types de données existants et identifier plus facilement le type souhaité. |

Vous pouvez également fournir au champ une **[!UICONTROL Description]** lisible par l&#39;utilisateur afin de fournir un contexte plus précis quant au cas d&#39;utilisation prévu pour le champ.

>[!NOTE]
>
>Selon le **[!UICONTROL type]** que vous avez sélectionné pour le champ, d&#39;autres contrôles de configuration peuvent apparaître dans le rail de droite. Pour plus d’informations sur ces contrôles, voir la section [propriétés de champ spécifiques au type](#type-specific-properties).
>
>Le rail droit fournit également des cases à cocher pour la désignation de types de champs spéciaux. Pour plus d&#39;informations, consultez la section sur les [types de champs spéciaux](#special).

Une fois le champ configuré, sélectionnez **[!UICONTROL Appliquer]**.

![](../../images/ui/fields/overview/field-details.png)

Le canevas se met à jour pour afficher le nom et le type du champ. Le rail droit liste désormais le chemin d’accès du champ en plus de ses autres propriétés.

![](../../images/ui/fields/overview/field-added.png)

Vous pouvez continuer à suivre les étapes ci-dessus pour ajouter d’autres champs au schéma. Une fois le schéma enregistré, sa classe de base et ses groupes de champs sont également enregistrés si des modifications ont été apportées.

>[!NOTE]
>
>Toute modification apportée aux groupes de champs ou à la classe d&#39;un schéma sera répercutée dans tous les autres schémas qui les utilisent.

## Propriétés de champ spécifiques au type {#type-specific-properties}

Lors de la définition d’un nouveau champ, d’autres options de configuration peuvent s’afficher dans le rail de droite selon le **[!UICONTROL Type]** que vous avez choisi pour le champ. Le tableau suivant présente les propriétés de champs supplémentaires ainsi que leurs types compatibles :

| Propriété de champ | Types compatibles | Description |
| --- | --- | --- |
| [!UICONTROL Valeur par défaut] | [!UICONTROL Chaîne],  [!UICONTROL Doublon],  [!UICONTROL Long],  [!UICONTROL Entier], Short, , Octet, Booléen][!UICONTROL  | Valeur par défaut qui sera affectée à ce champ si aucune autre valeur n’est fournie lors de l’assimilation. Cette valeur doit être conforme au type sélectionné dans le champ. |
| [!UICONTROL Modèle] | [!UICONTROL Chaîne] | Expression [régulière](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) à laquelle la valeur de ce champ doit se conformer pour être acceptée lors de l&#39;assimilation. |
| [!UICONTROL Format] | [!UICONTROL Chaîne] | Effectuez une sélection dans une liste de formats prédéfinis pour les chaînes auxquelles la valeur doit se conformer. Les formats disponibles sont les suivants : <ul><li>[[!UICONTROL date-heure]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL uri-référence]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointeur]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Longueur minimale] | [!UICONTROL Chaîne] | Nombre minimum de caractères que doit contenir la chaîne pour que la valeur soit acceptée lors de l’assimilation. |
| [!UICONTROL Longueur maximale] | [!UICONTROL Chaîne] | Nombre maximal de caractères que doit contenir la chaîne pour que la valeur soit acceptée lors de l’assimilation. |
| [!UICONTROL Valeur minimale] | [!UICONTROL Double] | Valeur minimale pour que le Doublon soit accepté lors de l&#39;assimilation. Si la valeur assimilée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l&#39;utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur minimale exclusive]&quot; doit rester vide. |
| [!UICONTROL Valeur maximale] | [!UICONTROL Doublon] | Valeur maximale pour le Doublon à accepter lors de l’assimilation. Si la valeur assimilée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l&#39;utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur maximale exclusive]&quot; doit rester vide. |
| [!UICONTROL Valeur minimale exclusive] | [!UICONTROL Doublon] | Valeur maximale pour le Doublon à accepter lors de l’assimilation. Si la valeur assimilée correspond exactement à celle saisie ici, elle est rejetée. Lors de l&#39;utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur minimale]&quot; (non exclusive) doit rester vide. |
| [!UICONTROL Valeur maximale exclusive] | [!UICONTROL Doublon] | Valeur maximale pour le Doublon à accepter lors de l’assimilation. Si la valeur assimilée correspond exactement à celle saisie ici, elle est rejetée. Lors de l&#39;utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur maximale]&quot; (non exclusive) doit rester vide. |

## Types de champ spéciaux {#special}

Le rail droit fournit plusieurs cases à cocher pour la désignation de rôles spéciaux pour le champ sélectionné. Les cas d’utilisation de certaines de ces options impliquent des considérations importantes concernant votre stratégie de modélisation des données et la manière dont vous envisagez d’utiliser les services de plateforme en aval.

Pour en savoir plus sur ces types spéciaux, consultez la documentation suivante :

* [[!UICONTROL Obligatoire]](./required.md)
* [[!UICONTROL Tableau]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identité]](./identity.md)  (disponible uniquement pour les champs de chaîne)
* [[!UICONTROL Relation]](./relationship.md)  (disponible uniquement pour les champs de chaîne)

Bien que techniquement non un type de champ spécial, il est également recommandé de consulter le guide sur la [définition de champs de type objet](./object.md) pour en savoir plus sur la définition de sous-champs imbriqués si votre schéma se structure.

## Étapes suivantes

Ce guide fournit un aperçu de la manière de définir les champs XDM dans l’interface utilisateur. N&#39;oubliez pas que les champs ne peuvent être ajoutés aux schémas qu&#39;à l&#39;aide de classes et de groupes de champs. Pour en savoir plus sur la gestion de ces ressources dans l’interface utilisateur, consultez les guides sur la création et la modification de [classes](../resources/classes.md) et de [groupes de champs](../resources/field-groups.md).

Pour plus d&#39;informations sur les fonctionnalités de l&#39;espace de travail [!UICONTROL Schémas], consultez la présentation de l&#39;espace de travail [[!UICONTROL Schémas]](../overview.md).

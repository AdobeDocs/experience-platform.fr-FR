---
keywords: Experience Platform;accueil;rubriques les plus consultées;api;API;XDM;système XDM;modèle de données d’expérience;modèle de données;ui;espace de travail;champ;
solution: Experience Platform
title: Définition des champs XDM dans l’interface utilisateur
description: Découvrez comment définir des champs XDM dans l’interface utilisateur de l’Experience Platform.
topic-legacy: user guide
exl-id: 2adb03d4-581b-420e-81f8-e251cf3d9fb9
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 5%

---

# Définition des champs XDM dans l’interface utilisateur

La balise [!DNL Schema Editor] de l’interface utilisateur de Adobe Experience Platform vous permet de définir vos propres champs dans les classes XDM (Experience Data Model) personnalisées et les groupes de champs de schéma. Ce guide décrit les étapes de définition des champs XDM dans l’interface utilisateur, y compris les options de configuration disponibles pour chaque type de champ.

## Conditions préalables

Ce guide nécessite une compréhension pratique du système XDM. Reportez-vous à la [présentation de XDM](../../home.md) pour une présentation du rôle de XDM dans l’écosystème Experience Platform et les [bases de la composition des schémas](../../schema/composition.md) pour découvrir comment les classes et les groupes de champs contribuent aux champs des schémas XDM.

Bien que ce guide ne soit pas obligatoire, il est recommandé de suivre également le tutoriel sur la [composition d’un schéma dans l’interface utilisateur](../../tutorials/create-schema-ui.md) afin de vous familiariser avec les différentes fonctionnalités de [!DNL Schema Editor].

## Sélectionner une ressource à laquelle ajouter des champs {#select-resource}

Pour définir de nouveaux champs XDM dans l’interface utilisateur, vous devez d’abord ouvrir un schéma dans [!DNL Schema Editor]. Selon les schémas actuellement disponibles dans la balise [!DNL Schema Library], vous pouvez choisir de [créer un nouveau schéma](../resources/schemas.md#create) ou [sélectionner un schéma existant à modifier](../resources/schemas.md#edit).

Une fois [!DNL Schema Editor] ouvert, utilisez le rail de gauche pour sélectionner la classe ou le groupe de champs pour lequel vous souhaitez définir des champs. Si la ressource est une ressource personnalisée définie par votre organisation, les contrôles permettant d’ajouter ou de modifier des champs s’affichent dans la zone de travail. Ces commandes s’affichent en regard du nom du schéma, ainsi que des champs de type objet qui ont été définis sous la classe ou le groupe de champs sélectionné.

![](../../images/ui/fields/overview/select-resource.png)

>[!NOTE]
>
>Si la classe ou le groupe de champs que vous sélectionnez est une ressource principale fournie par Adobe, il ne peut pas être modifié et les contrôles affichés ci-dessus n’apparaîtront donc pas. Si le schéma auquel vous souhaitez ajouter des champs est basé sur une classe XDM principale et ne contient aucun groupe de champs personnalisé, vous pouvez [créer un nouveau groupe de champs](../resources/field-groups.md#create) à ajouter au schéma à la place.

Pour ajouter un nouveau champ à la ressource, sélectionnez l’icône **plus (+)** en regard du nom du schéma dans la zone de travail ou en regard du champ de type objet sous lequel vous souhaitez définir le champ.

![](../../images/ui/fields/overview/plus-icon.png)

## Définition d’un champ pour une ressource {#define}

Après avoir sélectionné l’icône **plus (+)**, un **[!UICONTROL Nouveau champ]** s’affiche dans la zone de travail, située dans un objet de niveau racine et dont l’espace de noms correspond à votre identifiant de client unique (illustré par `_tenantId` dans l’exemple ci-dessous). Tous les champs ajoutés à un schéma par le biais de classes personnalisées et de groupes de champs sont automatiquement placés dans cet espace de noms afin d’éviter tout conflit avec d’autres champs provenant de classes et de groupes de champs fournis par l’Adobe.

![](../../images/ui/fields/overview/new-field.png)

Dans le rail de droite sous **[!UICONTROL Propriétés du champ]**, vous pouvez configurer les détails des nouveaux champs. Les informations suivantes sont requises pour chaque champ :

| Propriété du champ | Description |
| --- | --- |
| [!UICONTROL Nom du champ] | Nom explicite unique du champ. Notez que le nom du champ ne peut pas être modifié une fois le schéma enregistré.<br><br>Le nom doit idéalement être écrit en CamelCase. Il peut contenir des caractères alphanumériques, des tirets ou des traits de soulignement, mais **ne peut pas** commencer par un trait de soulignement.<ul><li>**Correct** :  `fieldName`</li><li>**Acceptable :** `field_name2`,  `Field-Name`,  `field-name_3`</li><li>**Incorrect** :  `_fieldName`</li></ul> |
| [!UICONTROL Nom d’affichage] | Nom convivial du champ. |
| [!UICONTROL Type] | Le type de données que le champ contiendra. Dans ce menu déroulant, vous pouvez sélectionner l’un des [types scalaires standard](../../schema/field-constraints.md) pris en charge par XDM, ou l’un des [types de données ](../resources/data-types.md) à plusieurs champs précédemment définis dans la balise [!DNL Schema Registry].<br><br>Vous pouvez également sélectionner  **[!UICONTROL Recherche de type]** avancé pour rechercher et filtrer les types de données existants et localiser plus facilement le type souhaité. |

{style=&quot;table-layout:auto&quot;}

Vous pouvez également fournir au champ une **[!UICONTROL description]** lisible par l’utilisateur facultatif afin de fournir plus de contexte sur le cas d’utilisation prévu du champ.

>[!NOTE]
>
>Selon le **[!UICONTROL type]** que vous avez sélectionné pour le champ, d’autres contrôles de configuration peuvent apparaître dans le rail de droite. Pour plus d’informations sur ces contrôles, consultez la section [Propriétés de champ spécifiques au type](#type-specific-properties) .
>
>Le rail de droite contient également des cases à cocher pour désigner les types de champ spéciaux. Pour plus d’informations, reportez-vous à la section [Types de champs spéciaux](#special) .

Une fois que vous avez terminé de configurer le champ, sélectionnez **[!UICONTROL Appliquer]**.

![](../../images/ui/fields/overview/field-details.png)

Le canevas se met à jour pour afficher le nom et le type du champ. Le rail de droite répertorie désormais le chemin d’accès du champ en plus de ses autres propriétés.

![](../../images/ui/fields/overview/field-added.png)

Vous pouvez continuer à suivre les étapes ci-dessus pour ajouter d’autres champs au schéma. Une fois le schéma enregistré, sa classe de base et ses groupes de champs sont également enregistrés si des modifications leur ont été apportées.

>[!NOTE]
>
>Toutes les modifications que vous apportez aux groupes de champs ou à la classe d’un schéma seront répercutées dans tous les autres schémas qui les utilisent.

## Propriétés de champ spécifiques au type {#type-specific-properties}

Lors de la définition d&#39;un nouveau champ, d&#39;autres options de configuration peuvent apparaître dans le rail de droite selon le **[!UICONTROL Type]** que vous avez choisi pour le champ. Le tableau suivant décrit ces propriétés de champ supplémentaires, ainsi que leurs types compatibles :

| Propriété du champ | Types compatibles | Description |
| --- | --- | --- |
| [!UICONTROL Valeur par défaut] | [!UICONTROL Chaîne],  [!UICONTROL Double],  [!UICONTROL Long],  [!UICONTROL Entier],  [!UICONTROL Court],  [!UICONTROL Octet],  [!UICONTROL Booléen] | Une valeur par défaut qui sera affectée à ce champ si aucune autre valeur n’est fournie pendant l’ingestion. Cette valeur doit être conforme au type sélectionné du champ. |
| [!UICONTROL Modèle] | [!UICONTROL Chaîne] | [expression régulière](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) à laquelle la valeur de ce champ doit être conforme pour être acceptée lors de l’ingestion. |
| [!UICONTROL Format] | [!UICONTROL Chaîne] | Effectuez une sélection dans une liste de formats prédéfinis pour les chaînes auxquelles la valeur doit se conformer. Les formats disponibles sont les suivants : <ul><li>[[!UICONTROL date-time]](https://tools.ietf.org/html/rfc3339)</li><li>[[!UICONTROL email]](https://tools.ietf.org/html/rfc2822)</li><li>[[!UICONTROL hostname]](https://tools.ietf.org/html/rfc1123#page-13)</li><li>[[!UICONTROL ipv4]](https://tools.ietf.org/html/rfc791)</li><li>[[!UICONTROL ipv6]](https://tools.ietf.org/html/rfc2460)</li><li>[[!UICONTROL uri]](https://tools.ietf.org/html/rfc3986)</li><li>[[!UICONTROL référence uri]](https://tools.ietf.org/html/rfc3986#section-4.1)</li><li>[[!UICONTROL url-template]](https://tools.ietf.org/html/rfc6570)</li><li>[[!UICONTROL json-pointer]](https://tools.ietf.org/html/rfc6901)</li></ul> |
| [!UICONTROL Longueur minimale] | [!UICONTROL Chaîne] | Nombre minimum de caractères que doit contenir la chaîne pour que la valeur soit acceptée lors de l’ingestion. |
| [!UICONTROL Longueur maximale] | [!UICONTROL Chaîne] | Nombre maximal de caractères que doit contenir la chaîne pour que la valeur soit acceptée lors de l’ingestion. |
| [!UICONTROL Valeur minimale] | [!UICONTROL Double] | Valeur minimale à accepter lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur minimale exclusive]&quot; doit rester vide. |
| [!UICONTROL Valeur maximale] | [!UICONTROL Double] | Valeur maximale que la Double doit être acceptée lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est acceptée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur maximale exclusive]&quot; doit rester vide. |
| [!UICONTROL Valeur minimale exclusive] | [!UICONTROL Double] | Valeur maximale que la Double doit être acceptée lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est rejetée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Valeur minimale]&quot; (non exclusive) doit rester vide. |
| [!UICONTROL Valeur maximale exclusive] | [!UICONTROL Double] | Valeur maximale que la Double doit être acceptée lors de l’ingestion. Si la valeur ingérée correspond exactement à celle saisie ici, la valeur est rejetée. Lors de l’utilisation de cette contrainte, la contrainte &quot;[!UICONTROL Maximum value]&quot; (non exclusive) doit rester vide. |

{style=&quot;table-layout:auto&quot;}

## Types de champ spéciaux {#special}

Le rail de droite comporte plusieurs cases à cocher pour la désignation des rôles spéciaux pour le champ sélectionné. Les cas d’utilisation de certaines de ces options impliquent des considérations importantes concernant votre stratégie de modélisation des données et la manière dont vous envisagez d’utiliser les services Platform en aval.

Pour en savoir plus sur ces types spéciaux, consultez la documentation suivante :

* [[!UICONTROL Obligatoire]](./required.md)
* [[!UICONTROL Tableau]](./array.md)
* [[!UICONTROL Enum]](./enum.md)
* [[!UICONTROL Identité]](./identity.md)  (disponible uniquement pour les champs de chaîne)
* [[!UICONTROL Relation]](./relationship.md)  (disponible uniquement pour les champs de chaîne)

Bien que techniquement non un type de champ spécial, il est également recommandé de consulter le guide sur la [définition des champs de type objet](./object.md) pour en savoir plus sur la définition de sous-champs imbriqués dans vos structures de schéma.

## Étapes suivantes

Ce guide fournit un aperçu de la définition des champs XDM dans l’interface utilisateur. N’oubliez pas que les champs ne peuvent être ajoutés qu’aux schémas par l’utilisation de classes et de groupes de champs. Pour en savoir plus sur la gestion de ces ressources dans l’interface utilisateur, consultez les guides sur la création et la modification des [classes](../resources/classes.md) et des [groupes de champs](../resources/field-groups.md).

Pour plus d’informations sur les fonctionnalités de l’espace de travail [!UICONTROL Schémas], consultez la [[!UICONTROL présentation des schémas] de l’espace de travail](../overview.md).

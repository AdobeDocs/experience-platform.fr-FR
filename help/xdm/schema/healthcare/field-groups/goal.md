---
title: Groupe de champs de schéma d’objectif
description: Découvrez le groupe de champs Schéma d’objectif .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 87715274-cc9d-41da-9ca7-1634903b4e8f
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 6%

---

# [!UICONTROL Groupe de champs de schéma Objectif]

[!UICONTROL Objectif] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) et le [[!DNL Provider class]](../../../classes/provider.md). Il fournit un champ de type d’objet unique `healthcareGoal` qui décrit le ou les objectifs prévus pour un patient, un groupe ou un service de prise en charge de l’organisation.

![Structure de groupe de champs](../../../images/healthcare/field-groups/goal/goal.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL État de l’accomplissement] | `achievementStatus` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Décrit la progression, ou l’absence de progression, vers l’objectif par rapport à la cible. |
| [!UICONTROL Adresses] | `addresses` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | Les conditions et autres éléments du dossier de l’intégrité qui sont destinés à être traités par l’objectif. |
| [!UICONTROL Catégorie] | `category` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Indique une catégorie dans laquelle l’objectif appartient, telle que l’alimentation ou le comportement. |
| [!UICONTROL Description] | `description` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Code ou texte décrivant l’objectif. |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../data-types/identifier.md) | Les identifiants d’entreprise affectés à cet objectif par l’performeur ou d’autres systèmes qui restent constants à mesure que la ressource est mise à jour et propagée d’un serveur à l’autre. |
| [!UICONTROL Remarque] | `note` | Tableau de [[!UICONTROL Annotation]](../data-types/annotation.md) | Commentaires concernant l’objectif. |
| [!UICONTROL Résultat] | `outcome` | Tableau de [[!UICONTROL référence codeable]](../data-types/codeable-reference.md) | Identifie le changement (ou l’absence de changement) lorsque l’état de l’objectif est évalué. |
| [!UICONTROL Priorité] | `priority` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Identifie le niveau d’importance convenu d’un commun accord pour atteindre ou maintenir l’objectif. |
| [!UICONTROL Source] | `source` | [[!UICONTROL Référence]](../data-types/reference.md) | Indique la source de l’objectif, comme le patient ou le praticien. |
| [!UICONTROL Commencer un concept codeable] | `startCodeableConcept` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | L’événement au bout duquel l’objectif doit être persuadé. |
| [!UICONTROL  Objet |]`subject` | [[!UICONTROL Référence]](../data-types/reference.md) | Identifie le patient, le groupe ou l’organisation pour qui l’objectif est établi. |
| [!UICONTROL Target] | `target` | Tableau d’objets | Indique la chronologie d’étapes spécifiques dans l’objectif. Pour plus d’informations, consultez la [section ci-dessous](#target) . |
| [!UICONTROL Continu] | `continous` | Booléen | Indique si, après avoir atteint l’objectif, l’activité en cours est nécessaire pour maintenir l’objectif. |
| [!UICONTROL État du cycle de vie] | `lifecycleStatus` | Chaîne | État du cycle de vie de l’objectif. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `proposed` </li> <li> `planned` </li> <li> `accepted` </li> <li> `active` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `cancelled` </li> <li> `entered-in-error` </li> <li> `rejected` </li> |
| [!UICONTROL Date de début] | `startDate` | Date | Date à laquelle l’objectif doit commencer à être poursuivi. |
| [!UICONTROL Date d’état] | `statusDate` | Date | Identifie le moment où l’état a été créé. |
| [!UICONTROL Raison de l’état] | `statusReason` | Chaîne | Capture la raison de l’état actuel. |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/goal.example.1.json)

## `target` {#target}

`target` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure cible](../../../images/healthcare/field-groups/goal/target.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Concept de code de détail] | `detailCodeableConcept` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Le code cible à atteindre pour signifier la réalisation de l’objectif. |
| [!UICONTROL Quantité détaillée] | `detailQuantity` | [[!UICONTROL Quantity]](../data-types/quantity.md) | La quantité cible à atteindre pour signifier la réalisation de l’objectif. |
| [!UICONTROL Plage de détails] | `detailRange` | [[!UICONTROL Plage]](../data-types/range.md) | La plage cible à atteindre pour signifier la réalisation de l’objectif. |
| [!UICONTROL Ratio des détails] | `detailRatio` | [[!UICONTROL Ratio]](../data-types/ratio.md) | Le ratio cible à atteindre pour indiquer la réalisation de l’objectif. |
| [!UICONTROL Mesure] | `measure` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Le paramètre dont la valeur fait l’objet d’un suivi. |
| [!UICONTROL Valeur booléenne détaillée] | `detailBoolean` | Booléen | Indique l’exécution de l’objectif. |
| [!UICONTROL Entier de détails] | `detailInteger` | Nombre entier | Nombre cible à atteindre pour signifier l’accomplissement de l’objectif. |
| [!UICONTROL Chaîne de détail] | `detailString` | Chaîne | La valeur cible à atteindre pour signifier la réalisation de l’objectif. |
| [!UICONTROL Date d’échéance] | `dueDate` | Date | Date à laquelle la cible doit être atteinte. |

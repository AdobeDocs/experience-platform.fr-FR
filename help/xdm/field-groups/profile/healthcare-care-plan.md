---
title: Groupe de champs du schéma du plan d’assistance
description: Découvrez le groupe de champs Plan d’assistance .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 4%

---

# Groupe de champs de schéma [!UICONTROL Care Plan]

[!UICONTROL Care Plan] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Il fournit un champ de type objet unique `healthcareCarePlan` qui capture un plan de santé pour un patient ou un groupe.

![Structure de groupe de champs](../../images/field-groups/healthcare-care-plan/care-plan.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Activité] | `activity` | Tableau d’objets | Identifie une action qui a eu lieu ou qui est prévue dans le cadre du plan. Pour plus d’informations, consultez la [section ci-dessous](#activity) . |
| [!UICONTROL Adresses] | `addresses` | Tableau de [[!UICONTROL référence codeable]](../../data-types/healthcare/codeable-reference.md) | Identifie les conditions ou les préoccupations que le plan de soins gère. |
| [!UICONTROL Basé Sur] | `basedOn` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Ressource de demande de niveau supérieur qui est satisfaite en tout ou en partie par ce plan de soins. |
| [!UICONTROL Équipe de soin] | `careTeam` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Identifie toutes les personnes et toutes les organisations qui sont censées être impliquées dans les soins prévus par ce plan. |
| [!UICONTROL Catégorie] | `category` | Tableau de [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Identifie le type de plan qui permet de différencier plusieurs plans co-existants. |
| [!UICONTROL Contributeur] | `contributor` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Identifie la ou les personnes, l’organisation ou l’appareil qui ont fourni le contenu du plan de prise en charge. |
| [!UICONTROL Gardien] | `custodian` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Lorsqu&#39;il est rempli, le gardien est responsable du plan de soins et lui est attribué. |
| [!UICONTROL Rencontre] | `encounter` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | La rencontre au cours de laquelle le plan de soins a été créé. |
| [!UICONTROL Objectif] | `goal` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Le(s) but(s) de l&#39;exécution du plan. |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../../data-types/healthcare/identifier.md) | Les identifiants commerciaux attribués à ce plan de prise en charge par l’performeur ou d’autres systèmes qui restent constants à mesure que la ressource est mise à jour et propagée d’un serveur à l’autre. |
| [!UICONTROL Remarque] | `note` | Tableau de [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Remarques générales sur le plan de soins qui ne sont pas couvertes dans d’autres attributs. |
| [!UICONTROL Partie De] | `partOf` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Le plan de soins plus vaste dans lequel ce plan de soins particulier est un élément ou une étape. |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../../data-types/healthcare/period.md) | Indique le moment où le plan a pris effet (ou est prévu) et le moment où il se termine. |
| [!UICONTROL Remplace] | `replaces` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Plan de soins terminé ou terminé dont la fonction est reprise par ce plan. |
| [!UICONTROL Objet] | `subject` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Identifie le patient ou le groupe dont les soins prévus sont décrits par le plan. |
| [!UICONTROL Supporting Info] | `supportingInfo` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Identifie certaines parties du dossier du patient qui ont influencé la formation du plan. Il peut s’agir de comorbidités, de procédures récentes, de limitations ou d’évaluations récentes. |
| [!UICONTROL Créé] | `created` | DateTime | Représente la date de création de ce plan de prise en charge dans le système, qui est souvent une date générée par le système. |
| [!UICONTROL Description] | `description` | Chaîne | Description de la portée et de la nature du plan. |
| [!UICONTROL Instancie Canonical] | `instantiatesCanonical` | Tableau de chaînes | L’URL pointant vers un protocole, une directive, un questionnaire ou toute autre définition définis par la FHIR et qui est respectée en tout ou en partie par ce plan. |
| [!UICONTROL Instancie Uri] | `instantiatesUri` | Tableau de chaînes | URL pointant vers un protocole, une directive, un questionnaire ou une autre définition gérés de l’extérieur et entièrement ou en partie par ce plan, représenté sous la forme d’une URI. |
| [!UICONTROL Intent] | `intent` | Chaîne | L&#39;intention du plan de soins. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `option` </li> <li> `directive` </li> |
| [!UICONTROL Statut] | `status` | Chaîne | État du plan de soins. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `draft` </li> <li> `active` </li> <li> `on-hold` </li> <li> `revoked` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `unknown` </li> |
| [!UICONTROL Titre] | `title` | Chaîne | Nom du plan de soins. |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/careplan.schema.json)

## `activity` {#activity}

`activity` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure d’activité](../../images/field-groups/healthcare-care-plan/activity.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Activité réalisée] | `performedActivity` | Tableau de [[!UICONTROL référence codeable]](../../data-types/healthcare/codeable-reference.md) | Les résultats de l’activité, tels qu’un rendez-vous ou une procédure. |
| [!UICONTROL Référence des activités planifiées] | `plannedActivityReference` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Détails de l’activité proposée. |
| [!UICONTROL Progression] | `progress` | Tableau de [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Remarques sur l’adhésion, l’état ou la progression de l’activité. |

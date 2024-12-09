---
title: Planification d’un groupe de champs de schéma
description: Découvrez le groupe de champs Schéma de planification .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 5%

---

# Groupe de champs de schéma [!UICONTROL Schedule]

[!UICONTROL Schedule] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) et le [[!DNL Provider class]](../../classes/provider.md). Il fournit un champ de type objet unique `healthcareSchedule` qui est un conteneur pour les créneaux horaires qui peuvent être disponibles pour les rendez-vous de réservation.

![Structure de groupe de champs](../../images/field-groups/schedule.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Acteur] | `actor` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Les emplacements qui référencent ce planning fournissant les détails de disponibilité de ces ressources référencées. |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../../data-types/healthcare/identifier.md) | Identifiants externes pour le planning. |
| [!UICONTROL Planification de l’horizon] | `planningHorizon` | [[!UICONTROL Période]](../../data-types/healthcare/period.md) | La période pendant laquelle les créneaux qui font référence à ce planning couvrent, même s’il n’en existe aucun. |
| [!UICONTROL Catégorie de service] | `serviceCategory` | Tableau de [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Une classification large du service qui doit être exécuté pendant la nomination. |
| [!UICONTROL Type de service] | `serviceType` | Tableau de [[!UICONTROL référence codeable]](../../data-types/healthcare/codeable-reference.md) | Service spécifique à effectuer lors de la nomination. |
| [!UICONTROL Spécialité] | `specialty` | Tableau de [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | La spécialité du praticien qui serait requis pour exécuter le service demandé au moment de la nomination. |
| [!UICONTROL Actif] | `active` | Booléen | Indique si l’enregistrement de planification est en cours d’utilisation. |
| [!UICONTROL Commentaire] | `comment` | Chaîne | Commentaires sur la disponibilité dans le but de décrire toute information étendue, comme des contraintes personnalisées sur les emplacements. |
| [!UICONTROL Nom] | `name` | Chaîne | La description du planning telle qu’elle sera présentée au consommateur lors de la recherche. |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)

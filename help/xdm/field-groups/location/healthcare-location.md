---
title: Groupe de champs de schéma d’emplacement
description: Découvrez le groupe de champs Schéma d’emplacement .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Groupe de champs de schéma [!UICONTROL Location]

[!UICONTROL Location] est un groupe de champs de schéma standard pour la [[!DNL Location] classe](../../classes/location.md). Il fournit un champ unique de type objet `healthcareLocation` qui capture les détails et les informations de position d’un emplacement.

![Structure de groupe de champs](../../images/field-groups/location.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | [[!UICONTROL Adresse]](../../data-types/healthcare/address.md) | Adresse de l’emplacement physique. |
| [!UICONTROL Caractéristique] | `characteristic` | Tableau de [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Collection des caractéristiques de l’emplacement. |
| [!UICONTROL Contact] | `contact` | Tableau des [[!UICONTROL coordonnées étendues]](../../data-types/healthcare/extended-contact-detail.md) | Les coordonnées de l’emplacement. |
| [!UICONTROL Point d’entrée] | `endpoint` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Points d’entrée techniques permettant d’accéder aux services d’exploitation de l’emplacement. |
| [!UICONTROL Form] (Formulaire) | `form` | [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Forme physique de l’emplacement. |
| [!UICONTROL Heures d’opération] | `hoursOfOperation` | Tableau de [[!UICONTROL Disponibilité]](../../data-types/healthcare/availability.md) | Quels jours et heures cet emplacement est généralement ouvert (y compris les exceptions). |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../../data-types/healthcare/identifier.md) | Code ou numéro unique identifiant l’emplacement. |
| [!UICONTROL Gestion de l’organisation] | `managingOrganization` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | L’organisation responsable de la mise en service et de la maintenance. |
| [!UICONTROL État opérationnel] | `operationalStatus` | [[!UICONTROL Coding]](../../data-types/healthcare/coding.md) | État opérationnel de l’emplacement. |
| [!UICONTROL Partie De L’Emplacement] | `partOf` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | L’emplacement dans lequel cet emplacement fait partie. |
| [!UICONTROL Position] | `position` | Objet | La situation géographique absolue. Contient trois propriétés au format double : <li>`longitude` : longitude avec référence WGS84</li> <li>`latitude` : Latitude avec référence WGS84.</li> <li>`altitude` : altitude avec la référence WGS84.</li> |
| [!UICONTROL Type] | `type` | Tableau de [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Type de fonction exécutée à l’emplacement. |
| [!UICONTROL Service virtuel] | `virtualService` | Tableau de [[!UICONTROL Virtual Service Detail]](../../data-types/healthcare/virtual-service-detail.md) | Détails de la connexion d’un service virtuel. |
| [!UICONTROL Alias] | `alias` | Tableau de chaînes | Liste des noms alternatifs dont l’emplacement est ou était connu sous le nom. |
| [!UICONTROL Description] | `description` | Chaîne | Informations supplémentaires pour identifier l’emplacement au-delà de son nom. |
| [!UICONTROL Mode] | `mode` | Chaîne | Mode de l’emplacement. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL Nom] | `name` | Chaîne | Nom de l’emplacement. |
| [!UICONTROL Statut] | `status` | Chaîne | État de l’emplacement. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)

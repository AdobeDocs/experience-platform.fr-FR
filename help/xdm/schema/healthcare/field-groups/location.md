---
title: Groupe de champs de schéma d’emplacement
description: Découvrez le groupe de champs de schéma d’emplacement.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 99831093-89da-4329-be29-c130c1d48f63
TQID: https://experienceleague.adobe.com/Qn4L1lvNPbzC-YMfprA5fs0YXQlHGUrHLc5x9EFxuPw
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 341
ht-degree: 6%

---

# Groupe de champs de schéma [!UICONTROL Location]

[!UICONTROL Location] est un groupe de champs de schéma standard pour la [[!DNL Location] class](../classes/location.md). Il fournit un `healthcareLocation` de champ de type objet unique qui capture les détails et les informations de position d’un emplacement.

![Structure du groupe de champs](../../../images/healthcare/field-groups/location.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Adresse] | `address` | [[!UICONTROL Adresse]](../data-types/address.md) | Adresse de l’emplacement physique. |
| [!UICONTROL Caractéristique] | `characteristic` | Tableau de [[!UICONTROL concept codable]](../data-types/codeable-concept.md) | Ensemble des caractéristiques de l’emplacement. |
| [!UICONTROL  Contact ] | `contact` | Tableau de [[!UICONTROL détails de contact étendus]](../data-types/extended-contact-detail.md) | Coordonnées du lieu. |
| [!UICONTROL Point d’entrée] | `endpoint` | Tableau de [[!UICONTROL référence]](../data-types/reference.md) | Points d’entrée techniques permettant d’accéder aux services d’exploitation pour l’emplacement. |
| [!UICONTROL Formulaire] | `form` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Forme physique de l’emplacement. |
| [!UICONTROL Heures d’ouverture] | `hoursOfOperation` | Tableau de [[!UICONTROL disponibilité]](../data-types/availability.md) | Les jours et heures d’ouverture standard de cet emplacement (y compris les exceptions). |
| [!UICONTROL Identifiant] | `identifier` | Tableau d’[[!UICONTROL identifiant]](../data-types/identifier.md) | Code ou numéro unique identifiant l’emplacement. |
| [!UICONTROL Organisation de gestion] | `managingOrganization` | [[!UICONTROL Référence]](../data-types/reference.md) | Organisation responsable de l’approvisionnement et de la maintenance. |
| [!UICONTROL État opérationnel] | `operationalStatus` | [[!UICONTROL Codage]](../data-types/coding.md) | Statut opérationnel de l’emplacement. |
| [!UICONTROL Partie Du Lieu] | `partOf` | [[!UICONTROL Référence]](../data-types/reference.md) | Emplacement dont fait partie cet emplacement. |
| [!UICONTROL Position] | `position` | Objet | La situation géographique absolue. Contient trois propriétés au format Double : <li>`longitude` : Longitude avec référence WGS84</li> <li>`latitude` : Latitude avec référence WGS84.</li> <li>`altitude` : Altitude avec référence WGS84.</li> |
| [!UICONTROL Type] | `type` | Tableau de [[!UICONTROL concept codable]](../data-types/codeable-concept.md) | Type de fonction exécutée à l’emplacement. |
| [!UICONTROL Service virtuel] | `virtualService` | Tableau de [[!UICONTROL détails du service virtuel]](../data-types/virtual-service-detail.md) | Détails de connexion d’un service virtuel. |
| [!UICONTROL Alias] | `alias` | Tableau de chaînes | Liste d’autres noms sous lesquels l’emplacement est ou était connu. |
| [!UICONTROL Description] | `description` | Chaîne | Informations supplémentaires pour identifier l’emplacement au-delà de son nom. |
| [!UICONTROL Mode] | `mode` | Chaîne | Mode de l’emplacement. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `instance` </li> <li> `kind` </li> |
| [!UICONTROL Nom] | `name` | Chaîne | Nom de l’emplacement. |
| [!UICONTROL Statut] | `status` | Chaîne | Statut de l’emplacement. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `active` </li> <li> `inactive` </li> <li> `suspended` </li> |

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/location.schema.json)

---
title: Planifier le groupe de champs de schéma
description: En savoir plus sur le groupe de champs de schéma Planifier .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: fcabef50-203c-4239-81b4-210aaf5b26ca
TQID: https://experienceleague.adobe.com/kk3TEg11OZvNbZAov9800dyB0MvMbudv10XvElNtdaE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 259
ht-degree: 5%

---

# [!UICONTROL Planifier] groupe de champs de schéma

[!UICONTROL Planification] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) et le [[!DNL Provider class]](../../../classes/provider.md). Il fournit un seul champ de type objet `healthcareSchedule` qui est un conteneur pour les créneaux horaires qui peuvent être disponibles pour la réservation de rendez-vous.

![Structure du groupe de champs](../../../images/healthcare/field-groups/schedule.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Acteur ] | `actor` | Tableau de [[!UICONTROL référence]](../data-types/reference.md) | Emplacements qui font référence à cette planification et qui fournissent les détails de disponibilité à ces ressources référencées. |
| [!UICONTROL Identifiant] | `identifier` | Tableau d’[[!UICONTROL identifiant]](../data-types/identifier.md) | Identifiants externes du planning. |
| [!UICONTROL Horizon de planification] | `planningHorizon` | [[!UICONTROL Période]](../data-types/period.md) | Période couverte par les créneaux horaires qui font référence à cette planification, même s&#39;il n&#39;en existe aucun. |
| [!UICONTROL Catégorie de services] | `serviceCategory` | Tableau de [[!UICONTROL concept codable]](../data-types/codeable-concept.md) | Une catégorisation large du service qui doit être effectué pendant la nomination. |
| [!UICONTROL Type de service] | `serviceType` | Tableau de [[!UICONTROL référence codable]](../data-types/codeable-reference.md) | Service spécifique à effectuer pendant le rendez-vous. |
| [!UICONTROL Spécialité] | `specialty` | Tableau de [[!UICONTROL concept codable]](../data-types/codeable-concept.md) | La spécialité du praticien qui serait nécessaire pour effectuer le service demandé dans le rendez-vous. |
| [!UICONTROL Actif] | `active` | Booléen | Indique si l&#39;enregistrement du planning est en cours d&#39;utilisation. |
| [!UICONTROL Commentaire] | `comment` | Chaîne | Commentaires sur la disponibilité dans le but de décrire toute information étendue, telle que les contraintes personnalisées sur les emplacements. |
| [!UICONTROL Nom] | `name` | Chaîne | Description du planning tel qu’il serait présenté à un client lors de la recherche. |

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)

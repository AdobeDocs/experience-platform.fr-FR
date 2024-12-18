---
title: Modèle De Données Des Soins De Santé V2
description: Découvrez quelques cas d’utilisation courants des soins de santé et les bonnes classes, les groupes de champs associés et les types de données à utiliser.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a796b58b-b36f-4277-870b-0d3939af8061
source-git-commit: cb39966de77846758c16153f78fcf521f6a421e3
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 4%

---

# [!UICONTROL Healthcare] Data Model V2

## Groupes et classes de champs {#field-groups}

Le tableau suivant décrit les classes et les groupes de champs de schéma recommandés pour plusieurs cas d’utilisation courants des services de santé.

| Cas d’utilisation | Groupes de champs et classes compatibles |
| --- | --- |
| **Créer/mettre à jour un patient** : lorsqu&#39;un patient arrive à la réception de l&#39;hôpital, un dossier patient est établi, y compris les détails démographiques tels qu&#39;un identifiant (facultatif), le nom du patient, sa date de naissance, son sexe et son adresse. Il s’agit d’un composant essentiel de l’informatique des soins de santé. | <ul><li>**[Profils individuels XDM](../../classes/individual-profile.md)** :<ul><li>[Patient](./field-groups/patient.md)</li></ul></li></ul> |
| **Vaccination** : Faciliter le processus de vaccination, gérer les dossiers de vaccination des patients et intégrer les DME aux systèmes de gestion des vaccins. | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)** :<ul><li>[Immunisation](./field-groups/immunization.md)</li></ul></li><li>**[Profil individuel XDM](../../classes/individual-profile.md)** :<ul><li>[Distribution de médicaments](./field-groups/medication-dispense.md)</li><li>[Demande de médicaments](./field-groups/medication-request.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Emplacement](./classes/location.md)** :<ul><li>[Emplacement](./field-groups/location.md)</li></ul><li>**[Médicaments](../../classes/medication.md)** :<ul><li>[Médicaments](./field-groups/medication.md)</li><li>[Distribution de médicaments](./field-groups/medication-dispense.md)</li><li>[Demande de médicaments](./field-groups/medication-request.md)</li></ul></li><li>**[Fournisseur](../../classes/provider.md)** :<ul><li>[Distribution de médicaments](./field-groups/medication-dispense.md)</li><li>[Demande de médicaments](./field-groups/medication-request.md)</li></ul></li></ul> |
| **Observance post-traitement** : inciter les patients et les soignants à compléter leurs plans de traitement et à réduire les taux de transfert de fonds. | <ul><li>**[Profil individuel XDM](../../classes/individual-profile.md)** :<ul><li>[Plan de soins](./field-groups/care-plan.md)</li><li>[Objectif](./field-groups/goal.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Emplacement](./classes/location.md)** :<ul><li>[Emplacement](./field-groups/location.md)</li></ul><li>**[Fournisseur](../../classes/provider.md)** :<ul><li>[Objectif](./field-groups/goal.md)</li></ul></li></ul> |
| **Expérience client pour l’assurance** : améliorez l’acquisition numérique et les expériences des consommateurs qui achètent une assurance. Par exemple : <li> Comprendre le comportement des consommateurs pour envoyer des e-mails promotionnels ou des annonces tierces ciblées aux personnes qui accèdent à des pages contenant des informations générales (telles que les plans, les noms/niveaux de plan, Medicaid ou les programmes de bien-être)</li><li> Envoyer des informations sur la santé cardiaque liées aux vaccins pour sensibiliser la marque ou demander de programmer des vaccins aux personnes qui recherchent des informations sur la santé cardiaque et les vaccins. </li> | <ul><li>**[Profil individuel XDM](../../classes/individual-profile.md)** :<ul><li>[Compte](./field-groups/account.md)</li><li>[Distribution de médicaments](./field-groups/medication-dispense.md)</li><li>[Demande de médicaments](./field-groups/medication-request.md)</li><li>[Patient](./field-groups/patient.md)</li></ul></li><li>**[Emplacement](./classes/location.md)** :<ul><li>[Emplacement](./field-groups/location.md)</li></ul><li>**[Médicaments](../../classes/medication.md)** :<ul><li>[Médicaments](./field-groups/medication.md)</li><li>[Distribution de médicaments](./field-groups/medication-dispense.md)</li><li>[Demande de médicaments](./field-groups/medication-request.md)</li></ul></li><li>**[Fournisseur](../../classes/provider.md)** :<ul><li>[Compte](./field-groups/account.md)</li><li>[Distribution de médicaments](./field-groups/medication-dispense.md)</li><li>[Demande de médicaments](./field-groups/medication-request.md)</li></ul><li>**[Planifier](../../classes/plan.md)** :<ul><li>[Objectif](./field-groups/coverage.md)</li></ul></li></ul> |
| **Expérience améliorée du fournisseur** : utilisation des données des fournisseurs du système EMR pour suggérer d’autres fournisseurs en fonction de la disponibilité du rendez-vous, du lieu et de la spécialité. <br> <br>Amélioration des recherches de fournisseurs pour afficher les résultats avec la disponibilité souhaitée, vérification que le fournisseur sélectionné fait partie du réseau payeur et fourniture d&#39;estimations de coûts. | <ul><li>**[Profils individuels XDM](../../classes/individual-profile.md)** :<ul><li>[Rendez-vous](./field-groups/appointment.md)</li><li>[Organisation](./field-groups/organization.md)</li><li>[Patient](./field-groups/patient.md)</li><li>[Praticien](./field-groups/practioner.md)</li><li>[Planning](./field-groups/schedule.md)</li></ul></li><li>**[Emplacement](./classes/location.md)** :<ul><li>[Emplacement](./field-groups/location.md)</li></ul><li>**[Fournisseur](../../classes/provider.md)** :<ul><li>[Rendez-vous](./field-groups/appointment.md)</li><li>[Organisation](./field-groups/organization.md)</li><li>[Praticien](./field-groups/practioner.md)</li><li>[Planning](./field-groups/schedule.md)</li></ul></li></ul> |

{style="table-layout:auto"}

## Types de données {#data-types}

Le tableau suivant décrit les types de données créés conformément aux spécifications [!DNL HL7 FHIR Release 5].

| Nom | Description |
| --- | --- |
| [[!UICONTROL Adresse]](./data-types/address.md) | Décrit une adresse exprimée à l’aide de conventions postales (par opposition au GPS ou à d’autres formats de définition d’emplacement). |
| [[!UICONTROL Annotation]](./data-types/annotation.md) | Nœud de texte avec attribution à l’auteur. |
| [[!UICONTROL Disponibilité]](./data-types/availability.md) | Données de disponibilité d&#39;un article. |
| [[!UICONTROL Concept codable]](./data-types/codeable-concept.md) | Référence d’une ressource à une autre. |
| [[!UICONTROL Référence codable]](./data-types/codeable-reference.md) | Référence à une ressource ou à un concept. |
| [[!UICONTROL Codage]](./data-types/coding.md) | Référence à un code défini par un système terminologique. |
| [[!UICONTROL  Point de contact ]](./data-types/contact-point.md) | Coordonnées d’une personne. |
| [[!UICONTROL Posologie]](./data-types/dosage.md) | Comment le médicament est/a été pris ou doit être pris. |
| [[!UICONTROL Durée]](./data-types/duration.md) | Une durée. |
| [[!UICONTROL Détails de contact étendus]](./data-types/extended-contact-detail.md) | Informations sur le contact étendu. |
| [[!UICONTROL Nom Humain]](./data-types/human-name.md) | Informations sur le nom d’un être humain ou d’une autre entité vivante. |
| [[!UICONTROL Identifiant]](./data-types/identifier.md) | Identifiant destiné au calcul. |
| [[!UICONTROL Argent]](./data-types/money.md) | Une quantité d&#39;utilité économique dans une monnaie reconnue. |
| [[!UICONTROL Période]](./data-types/period.md) | Période définie par une date/heure de début et de fin. |
| [[!UICONTROL  Personne ]](./data-types/person.md) | Informations sur un enregistrement de personne générique. |
| [[!UICONTROL Quantité]](./data-types/quantity.md) | Une quantité mesurée ou mesurable. |
| [[!UICONTROL Plage]](./data-types/range.md) | Ensemble de valeurs liées par des valeurs faibles et élevées. |
| [[!UICONTROL Rapport]](./data-types/ratio.md) | Rapport de deux valeurs [[!UICONTROL Quantité]](./data-types/quantity.md) via un numérateur et un dénominateur. |
| [[!UICONTROL Référence]](./data-types/reference.md) | Référence d’une ressource à une autre. |
| [[!UICONTROL Répéter]](./data-types/repeat.md) | Ensemble de règles qui décrit le moment où un événement est planifié. |
| [[!UICONTROL Quantité simple]](./data-types/simple-quantity.md) | Une quantité mesurée ou mesurable. |
| [[!UICONTROL Planning]](./data-types/timing.md) | Informations sur un événement pouvant se produire plusieurs fois. |
| [[!UICONTROL Détails du service virtuel]](./data-types/virtual-service-detail.md) | Détails de contact du service virtuel. |


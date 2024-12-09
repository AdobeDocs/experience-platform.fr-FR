---
title: Modèle de données HealthCare V2
description: Découvrez certains cas d’utilisation courants des soins de santé, ainsi que les meilleures classes, groupes de champs associés et types de données à utiliser.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 872dfce238bfed9bb3eccc0b4589d418db76d1d4
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 16%

---

# [!UICONTROL Healthcare] Data Model V2

## Groupes de champs et classes {#field-groups}

Le tableau suivant décrit les classes recommandées et les groupes de champs de schéma pour plusieurs cas d’utilisation de la santé courants.

<table>
  <thead>
    <tr>
      <th>Cas d’utilisation</th>
      <th>Groupes de champs</th>
      <th>Classes compatibles</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Créer/mettre à jour le patient</strong> : lorsqu’un patient arrive à la réception de l’hôpital, un dossier de patient est établi, y compris des détails démographiques comme un identifiant (facultatif), le nom du patient, sa date de naissance, son sexe et son adresse. Il s’agit là d’une composante essentielle de l’informatique des soins de santé.</td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="6"><strong>Vaccination</strong> : Faciliter le processus de vaccination, gérer les dossiers d'immunisation des patients et intégrer les DME aux systèmes de gestion des vaccins.</td>
      <td><a href="../../field-groups/event/healthcare-immunization.md">Vaccination</a></td>
      <td>
        <li><a href="../../classes/experienceevent.md">Événement d’expérience XDM</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Emplacement</a></td>
      <td>
        <li><a href="../../classes/location.md">Emplacement</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-v2.md">Médicaments</a></td>
      <td>
        <li><a href="../../classes/medication.md">Médicaments</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-dispense.md">Dépense de médicaments</a></td>
      <td>
        <li><a href="../../classes/medication.md">Médicaments</a></li>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-request.md">Demande de médicament</a></td>
      <td>
        <li><a href="../../classes/medication.md">Médicaments</a></li>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="4"><strong>Respect des post-soins</strong> : motiver les patients et les prestataires à compléter leurs plans de traitement et à réduire les taux de transferts.</td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Emplacement</a></td>
      <td>
        <li><a href="../../classes/location.md">Emplacement</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-care-plan.md">Plan de prise en charge</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-goal.md">Objectif</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="7"><strong>Expérience client pour l’assurance</strong> : améliorez l’acquisition numérique et les expériences client pour les achats d’assurance. Par exemple : 
        <li> Comprendre le comportement des consommateurs lorsqu’ils envoient des emails promotionnels ou des annonces tierces ciblées à des personnes qui accèdent à des pages contenant des informations générales (comme les plans, les noms/niveaux des plans, Medicaid ou les programmes de bien-être)
        </li> 
        <li> Envoi d'informations relatives au vaccin sur la santé cardiaque afin de créer une prise de conscience de la marque ou de demandes de planification de vaccins aux personnes qui recherchent des informations sur la santé cardiaque et le vaccin.
        </li>
      </td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/plan/healthcare-coverage.md">Couverture</a></td>
      <td>
        <li><a href="../../classes/plan.md">Plan</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-account.md">Compte</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Emplacement</a></td>
      <td>
        <li><a href="../../classes/location.md">Emplacement</a></li>
      </td>
    </tr>
      <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-v2.md">Médicaments</a></td>
      <td>
        <li><a href="../../classes/medication.md">Médicaments</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-dispense.md">Dépense de médicaments</a></td>
      <td>
        <li><a href="../../classes/medication.md">Médicaments</a></li>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/medication/healthcare-medication-request.md">Demande de médicament</a></td>
      <td>
        <li><a href="../../classes/medication.md">Médicaments</a></li>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td rowspan="5"><strong>Amélioration de l’expérience du fournisseur</strong> : utilisation des données du fournisseur du système EMR pour suggérer d’autres fournisseurs en fonction de la disponibilité, de l’emplacement et de la spécialité du rendez-vous. <br> <br>Amélioration des recherches de fournisseurs pour afficher les résultats avec la disponibilité souhaitée, vérification que le fournisseur sélectionné fait partie du réseau payeur et établissement d’estimations de coûts.
      </td>
      <td><a href="../../field-groups/profile/healthcare-patient.md">Patient</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/location/healthcare-location.md">Emplacement</a></td>
      <td>
        <li><a href="../../classes/location.md">Emplacement</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-organization.md">Organisation</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-practioner.md">Professionnel ou professionnelle</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
    <tr>
      <td><a href="../../field-groups/profile/healthcare-schedule.md">Planning</a></td>
      <td>
        <li><a href="../../classes/individual-profile.md">XDM Individual Profile</a></li>
        <li><a href="../../classes/provider.md">Prestataire</a></li>
      </td>
    </tr>
  </tbody>
</table>

## Types de données {#data-types}

Le tableau suivant décrit les types de données créés conformément aux spécifications [!DNL HL7 FHIR Release 5].

| Nom | Description |
| --- | --- |
| [[!UICONTROL Adresse]](../../data-types/healthcare/address.md) | Décrit une adresse exprimée à l&#39;aide de conventions postales (par opposition au GPS ou à d&#39;autres formats de définition de localisation). |
| [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Noeud de texte avec attribution à l’auteur. |
| [[!UICONTROL Disponibilité]](../../data-types/healthcare/availability.md) | Données de disponibilité d’un élément. |
| [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Référence d’une ressource à une autre. |
| [[!UICONTROL Référence codeable]](../../data-types/healthcare/codeable-reference.md) | Référence à une ressource ou à un concept. |
| [[!UICONTROL Coding]](../../data-types/healthcare/coding.md) | Référence à un code défini par un système terminologique. |
| [[!UICONTROL Point de contact]](../../data-types/healthcare/contact-point.md) | Coordonnées d’une personne. |
| [[!UICONTROL Dosage]](../../data-types/healthcare/dosage.md) | Comment le médicament est-il pris ou doit-il être pris ? |
| [[!UICONTROL Durée]](../../data-types/healthcare/duration.md) | Une durée. |
| [[!UICONTROL  {Extended Contact Details]](../../data-types/healthcare/extended-contact-detail.md) | les informations d’un contact étendu. |
| [[!UICONTROL Nom de l’homme]](../../data-types/healthcare/human-name.md) | Informations sur le nom d’un être humain ou d’une autre entité vivante. |
| [[!UICONTROL Identifiant]](../../data-types/healthcare/identifier.md) | Identifiant destiné au calcul. |
| [[!UICONTROL Money]](../../data-types/healthcare/money.md) | Une quantité d&#39;utilité économique dans une monnaie reconnue. |
| [[!UICONTROL Période]](../../data-types/healthcare/period.md) | Une période définie par une date/heure de début et de fin. |
| [[!UICONTROL Personne]](../../data-types/healthcare/person.md) | Informations sur un enregistrement de personne générique. |
| [[!UICONTROL Quantity]](../../data-types/healthcare/quantity.md) | Montant mesuré ou mesurable. |
| [[!UICONTROL Plage]](../../data-types/healthcare/range.md) | Ensemble de valeurs liées par des valeurs élevées et faibles. |
| [[!UICONTROL Ratio]](../../data-types/healthcare/ratio.md) | Un ratio de deux valeurs [[!UICONTROL Quantity]](../../data-types/healthcare/quantity.md) via un numérateur et un dénominateur. |
| [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Référence d’une ressource à une autre. |
| [[!UICONTROL Répéter]](../../data-types/healthcare/repeat.md) | Ensemble de règles qui décrivent le moment où un événement est planifié. |
| [[!UICONTROL Quantité simple]](../../data-types/healthcare/simple-quantity.md) | Montant mesuré ou mesurable. |
| [[!UICONTROL Minutage]](../../data-types/healthcare/timing.md) | Informations sur un événement qui peut se produire plusieurs fois. |
| [[!UICONTROL Détails du service virtuel]](../../data-types/healthcare/virtual-service-detail.md) | Détails des contacts du service virtuel. |

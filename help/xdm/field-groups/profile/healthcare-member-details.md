---
title: Groupe de champs de schéma Détails du membre HealthCare
description: Découvrez le groupe de champs Détails du membre HealthCare .
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 3%

---

# [!UICONTROL Détails du membre du service de santé] groupe de champs de schéma

[!UICONTROL Healthcare Member Details] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) qui capture les détails d&#39;une personne qui a ou va recevoir des services ou des soins médicaux, tels que les coordonnées, le médecin en soins primaires et les informations sur le plan.

![Structure de groupe de champs](../../images/field-groups/healthcare-member-details/structure.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse de facturation de la personne. |
| `faxPhone` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de fax de la personne. |
| `homeAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse de la personne. |
| `homePhone` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de téléphone du domicile de la personne. |
| `mailingAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse postale de la personne. |
| `memberDetails` | Objet | Objet contenant des informations détaillées sur les attributs et relations liés à la santé de la personne. Pour plus d’informations sur la structure de l’objet, reportez-vous à la sous-section [ci-dessous](#memberDetails) . |
| `mobilePhone` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de téléphone portable de la personne. |
| `person` | [[!UICONTROL Personne]](../../data-types/person.md) | Acteur, contact ou propriétaire individuel lié à l’appartenance à la personne au service de santé. |
| `personalEmail` | [[!UICONTROL Adresse électronique]](../../data-types/email-address.md) | Adresse électronique personnelle de la personne. |
| `shippingAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse de livraison de la personne. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` est un objet qui contient des informations détaillées sur les attributs et relations liés à la santé de la personne. La structure de `memberDetails` est décrite ci-dessous.

![structure memberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `emergencyContact` | Objet | Capture les informations de contact d’urgence suivantes pour la personne : <ul><li>`fullName` : (chaîne). Nom complet du contact d’urgence.</li><li>`phone` : (chaîne). Numéro de téléphone du contact d’urgence.</li><li>`relationshipToMember` : (chaîne). Relation du contact d’urgence avec la personne.</li></ul> |
| `medications` | Tableau d’objets | Répertorie les détails des médicaments actuels et passés associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`refillLocation` : ([[!UICONTROL Adresse postale]](../../data-types/postal-address.md)) L’emplacement de remplissage du médicament.</li><li>`ID` : (chaîne) ID du médicament.</li><li>`isCurrent` : (booléen). Indique si le traitement est actuel ou passé.</li><li>`numberOfRefills` : (nombre entier) nombre de remplissages prescrits par le fournisseur de ce médicament.</li><li>`startDate` : (DateTime) date à laquelle la personne a commencé à prendre le traitement.</li></ul> |
| `multipleBirth` | Objet | Capture les détails des naissances multiples : <ul><li>`isMultipleBirth` : (booléen). Indique si la personne a donné plusieurs naissances.</li><li>`multipleBirthNumber` : (nombre entier) nombre de bébés nés si `isMultipleBirth` est vrai.</li></ul> |
| `plans` | Tableau d’objets | Répertorie les détails des plans médicaux actuels et antérieurs associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`coverageEndDate` : (DateTime) date à laquelle la couverture du plan se termine.</li><li>`coverageStartDate` : (DateTime) date à laquelle la couverture du plan commence.</li><li>`isActive` : (booléen). Indique si le plan est actif.</li><li>`planId` : (chaîne). ID de plan.</li></ul> |
| `primaryCarePhysicians` | Tableau d’objets | Répertorie les détails des médecins de soins primaires associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`endDate` : (DateTime) date à laquelle le médecin traitant a mis fin aux soins de la personne.</li><li>`fullname` : (chaîne). Nom complet du médecin.</li><li>`providerId` : (chaîne). Identifiant unique du médecin.</li><li>`startDate` : (DateTime) date à laquelle le médecin traitant a commencé à prendre soin de la personne.</li></ul> |
| `specialists` | Tableau d’objets | Répertorie les détails des spécialistes des soins de santé associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`fullname` : (chaîne). Nom complet du spécialiste.</li><li>`providerId` : (chaîne). Identifiant unique du spécialiste.</li><li>`specialty` : (chaîne). Spécialité du fournisseur (anesthésiologie, urologie, radiologie, dermatologie, etc.).</li></ul> |
| `beneficiaryRelationship` | Chaîne | La relation du bénéficiaire avec le membre du service de santé si la personne est une personne à charge (par exemple : elle-même, son conjoint, un enfant, etc.). |
| `billingAccountID` | Chaîne | Identifiant unique du compte de facturation de la personne. |
| `dateAgeCollected` | DateTime | Date à laquelle l’âge de la personne a été collecté. |
| `deceasedDate` | DateTime | Date à laquelle la personne est morte si elle est décédée. |
| `isDeceased` | Booléen | Indique si la personne est décédée. |
| `isDependent` | Booléen | Indique si la personne est une personne à charge. |
| `nationality` | Chaîne | La relation juridique entre la personne et son état, représentée à l’aide du code ISO 3166-1 Alpha-2. |
| `preferredAvailability` | Chaîne | Disponibilité du jour et de l’heure de votre choix pour un rendez-vous. |
| `primaryMemberID` | Chaîne | Identifiant unique de l’abonné principal si la personne est une personne à charge. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Reportez-vous à la documentation du schéma de l’industrie pour plus d’informations sur la façon dont ce groupe de champs peut être utilisé pour répondre aux [&#x200B; cas d’utilisation courants du secteur de la santé](../../schema/industries/healthcare.md).

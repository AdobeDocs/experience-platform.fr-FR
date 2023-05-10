---
title: Groupe de champs de schéma Détails du membre HealthCare
description: Ce document présente un aperçu du groupe de champs Détails du membre HealthCare.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 6%

---

# [!UICONTROL Détails des membres du service de santé] groupe de champs de schéma

[!UICONTROL Détails des membres du service de santé] est un groupe de champs de schéma standard pour la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) qui capture les détails d’une personne qui a ou va recevoir un service ou des soins médicaux, tels que les coordonnées, le médecin traitant Principal et les renseignements sur le plan.

![Structure du groupe de champs](../../images/field-groups/healthcare-member-details/structure.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse de facturation de la personne. |
| `faxPhone` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de fax de la personne. |
| `homeAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse du domicile de la personne. |
| `homePhone` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de téléphone du domicile de la personne. |
| `mailingAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse postale de la personne. |
| `memberDetails` | Objet | Objet contenant des informations détaillées sur les attributs et relations liés à la santé de la personne. Voir [sous-section](#memberDetails) pour plus d’informations sur la structure de l’objet. |
| `mobilePhone` | [[!UICONTROL Numéro de téléphone]](../../data-types/phone-number.md) | Numéro de téléphone portable de la personne. |
| `person` | [[!UICONTROL Personne]](../../data-types/person.md) | Acteur, contact ou propriétaire individuel lié à l’appartenance à la personne au service de santé. |
| `personalEmail` | [[!UICONTROL Adresse e-mail]](../../data-types/email-address.md) | Adresse électronique personnelle de la personne. |
| `shippingAddress` | [[!UICONTROL Adresse postale]](../../data-types/postal-address.md) | Adresse de livraison de la personne. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` est un objet qui contient des informations détaillées sur les attributs et relations liés à la santé de la personne. La structure de `memberDetails` est décrit ci-dessous.

![structure memberDetails](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `emergencyContact` | Objet | Capture les informations de contact d’urgence suivantes pour la personne : <ul><li>`fullName`: (Chaîne) Nom complet du contact d’urgence.</li><li>`phone`: (Chaîne) Numéro de téléphone du contact d’urgence.</li><li>`relationshipToMember`: (Chaîne) La relation du contact d’urgence avec la personne.</li></ul> |
| `medications` | Tableau d’objets | Répertorie les détails des médicaments actuels et passés associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`refillLocation`: ([[!UICONTROL Adresse postale]](../../data-types/postal-address.md)) L’emplacement de remplissage du médicament.</li><li>`ID`: (Chaîne) Identifiant de la médication.</li><li>`isCurrent`: (booléen) Indique si le médicament est à jour ou passé.</li><li>`numberOfRefills`: (Entier) Nombre de recharges prescrites par le fournisseur de ce médicament.</li><li>`startDate`: (DateTime) Date à laquelle la personne a commencé à prendre le traitement.</li></ul> |
| `multipleBirth` | Objet | Capture les détails des naissances multiples : <ul><li>`isMultipleBirth`: (Booléen) Indique si la personne a donné plusieurs naissances.</li><li>`multipleBirthNumber`: (Entier) Nombre de bébés nés si `isMultipleBirth` est vrai.</li></ul> |
| `plans` | Tableau d’objets | Répertorie les détails des plans médicaux actuels et antérieurs associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`coverageEndDate`: (DateTime) Date à laquelle la couverture du plan se termine.</li><li>`coverageStartDate`: (DateTime) Date à laquelle la couverture du plan commence.</li><li>`isActive`: (Booléen) Indique si le plan est principal.</li><li>`planId`: (Chaîne) ID de plan.</li></ul> |
| `primaryCarePhysicians` | Tableau d’objets | Répertorie les détails des médecins Principaux associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`endDate`: (DateTime) Date à laquelle le médecin traitant Principal a mis fin aux soins de la personne.</li><li>`fullname`: (Chaîne) Nom complet du médecin.</li><li>`providerId`: (Chaîne) Identifiant unique du médecin.</li><li>`startDate`: (DateTime) Date à laquelle le médecin traitant Principal a commencé à prendre soin de la personne.</li></ul> |
| `specialists` | Tableau d’objets | Répertorie les détails des spécialistes des soins de santé associés à la personne. Chaque élément du tableau est un objet qui capture les détails suivants : <ul><li>`fullname`: (Chaîne) Nom complet du spécialiste.</li><li>`providerId`: (Chaîne) Identifiant unique du spécialiste.</li><li>`specialty`: (Chaîne) La spécialité du fournisseur (anesthésiologie, urologie, radiologie, dermatologie, etc.).</li></ul> |
| `beneficiaryRelationship` | Chaîne | La relation du bénéficiaire avec le membre du service de santé si la personne est une personne à charge (par exemple : elle-même, son conjoint, un enfant, etc.). |
| `billingAccountID` | Chaîne | Identifiant unique du compte de facturation de la personne. |
| `dateAgeCollected` | DateTime | Date à laquelle l’âge de la personne a été collecté. |
| `deceasedDate` | DateTime | Date à laquelle la personne est morte si elle est décédée. |
| `isDeceased` | Booléen | Indique si la personne est décédée. |
| `isDependent` | Booléen | Indique si la personne est une personne à charge. |
| `nationality` | Chaîne | La relation juridique entre la personne et son état, représentée à l’aide du code ISO 3166-1 Alpha-2. |
| `preferredAvailability` | Chaîne | Disponibilité du jour et de l’heure de votre choix pour un rendez-vous. |
| `primaryMemberID` | Chaîne | Identifiant unique de l’abonné Principal si la personne est une personne à charge. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Pour plus d’informations sur l’utilisation de ce groupe de champs pour servir les [Cas pratiques du secteur de la santé](../../schema/industries/healthcare.md).

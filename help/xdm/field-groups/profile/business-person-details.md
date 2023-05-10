---
title: Groupe de champs de schéma de détails de personne professionnelle XDM
description: Ce document fournit un aperçu du groupe de champs de schéma XDM Business Person Details .
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 16%

---

# [!UICONTROL Informations détaillées sur les personnes commerciales XDM] groupe de champs de schéma

[!UICONTROL Informations détaillées sur les personnes commerciales XDM] est un groupe de champs de schéma standard pour la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) qui capture les informations sur une personne dans le contexte d’une entreprise B2B (business-to-business).

![](../../images/field-groups/business-person-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `b2b` | Objet | Objet qui capture les détails spécifiques à B2B sur la personne. |
| `b2b.accountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du compte professionnel associé à la personne. |
| `b2b.convertedContactKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du contact associé si la piste a été convertie. |
| `b2b.personKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne ou du fragment de profil. |
| `b2b.accountID` | Chaîne | Identifiant unique du compte professionnel auquel cette personne est associée. |
| `b2b.blockedCause` | Chaîne | Si la personne est bloquée, cette propriété explique pourquoi. |
| `b2b.convertedContactID` | Chaîne | L’ID de contact si la conversion de la piste a réussi. |
| `b2b.convertedDate` | DateTime | Date de conversion si la piste a été convertie avec succès. |
| `b2b.isBlocked` | Booléen | Indique si la personne est bloquée. |
| `b2b.isConverted` | Booléen | Indique si le prospect est converti. |
| `b2b.isMarketingSuspended` | Booléen | Indique si le marketing est suspendu pour la personne. |
| `b2b.marketingSuspendedCause` | Chaîne | Si le marketing est suspendu pour la personne, cette propriété en fournit la raison. |
| `b2b.personGroupID` | Chaîne | Identifiant de groupe de la personne. |
| `b2b.personScore` | Double | Score généré pour la personne par un système CRM. |
| `b2b.personSource` | Chaîne | Source de laquelle les informations de la personne ont été reçues. |
| `b2b.personStatus` | Chaîne | État actuel du marketing ou des ventes de la personne. |
| `b2b.personType` | Chaîne | Type de personne B2B. |
| `extSourceSystemAudit` | [Attributs d’audit du système de source externe](../../data-types/external-source-system-audit-attributes.md) | Si la relation homme-entreprise provient d’un système source externe, cet objet capture les attributs de contrôle de ce système. |
| `extendedWorkDetails` | Objet | Capture d’autres informations relatives au travail de la personne. |
| `extendedWorkDetails.assistantDetails` | Objet | Capture les attributs suivants liés à l’assistant de la personne : <ul><li>`name`: ([Nom de la personne](../../data-types/person-name.md)) Nom complet de l’assistant.</li><li>`phone`: ([Numéro de téléphone](../../data-types/phone-number.md)) Numéro de téléphone de l’assistant.</li></ul> |
| `extendedWorkDetails.departments` | Tableau de chaînes | Liste des noms des départements où la personne travaille. |
| `extendedWorkDetails.jobTitle` | Chaîne | Fonction de la personne. |
| `extendedWorkDetails.photoUrl` | Chaîne | URL d’une photo de la personne. |
| `extendedWorkDetails.reportsToID` | Chaîne | Identifiant du gestionnaire de rapports de la personne. |
| `faxPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Numéro de fax de la personne. |
| `homeAddress` | [Adresse postale](../../data-types/postal-address.md) | Adresse du domicile de la personne. |
| `homePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Numéro de téléphone du domicile de la personne. |
| `mobilePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Numéro de téléphone portable de la personne. |
| `otherAddress` | [Adresse postale](../../data-types/postal-address.md) | Adresse alternative de la personne. |
| `otherPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Numéro de téléphone alternatif de la personne. |
| `person` | [Personne](../../data-types/person.md) | Acteur, contact ou propriétaire individuel. |
| `personalEmail` | [Adresse e-mail](../../data-types/email-address.md) | Adresse électronique personnelle de la personne. |
| `workAddress` | [Adresse postale](../../data-types/postal-address.md) | Adresse professionnelle de la personne. |
| `workEmail` | [Adresse e-mail](../../data-types/email-address.md) | Adresse électronique professionnelle de la personne. |
| `workPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Numéro de téléphone professionnel de la personne. |
| `identityMap` | Carte | Champ de mappage contenant un ensemble d’identités d’espace de noms pour la personne. Ce champ est automatiquement mis à jour par le système lors de l’ingestion des données d’identité. Pour utiliser correctement ce champ pour [Profil client en temps réel](../../../profile/home.md), ne tentez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.<br /><br />Pour plus d’informations sur les cas d’utilisation des mappages dʼidentités, consultez la section correspondante sur la page consacrée aux [principes de base de la composition des schémas](../../schema/composition.md#identityMap). |
| `isDeleted` | Booléen | Indique si cette personne a été supprimée dans Marketo Engage.<br><br>Lors de l’utilisation de la variable [Connecteur source Marketo](../../../sources/connectors/adobe-applications/marketo/marketo.md), les enregistrements supprimés dans Marketo sont automatiquement répercutés dans Real-time Customer Profile. Cependant, les enregistrements relatifs à ces profils peuvent toujours persister dans le lac de données. En définissant `isDeleted` to `true`, vous pouvez utiliser ce champ pour filtrer les enregistrements qui ont été supprimés de vos sources lors de l’interrogation du lac de données. |
| `organizations` | Tableau de chaînes | Liste des noms de l’organisation dans laquelle la personne travaille. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)

---
title: Groupe De Champs Du Schéma D’Immunisation
description: Découvrez le groupe de champs Schéma d’immunisation .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: a392e26b-7631-4f54-b9ad-cc4586673ac5
TQID: https://experienceleague.adobe.com/485auccSgp9jhYJS9rHqNh4idHw6rMXbZcEBAIjgEpk
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: adf04a6a-050f-44bc-a52c-db79ccb22ebf
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 613
ht-degree: 8%

---

# [!UICONTROL Immunisation] groupe de champs de schéma

[!UICONTROL Immunisation] est un groupe de champs de schéma standard pour la [[!DNL XDM Experience Event] classe](../../../classes/experienceevent.md). Il fournit un `healthcareImmunization` de champ de type objet unique qui recueille les informations sur les événements de vaccination.

![Structure du groupe de champs](../../../images/healthcare/field-groups/immunization/immunization.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Produit administré] | `administeredProduct` | [[!UICONTROL Référence codable]](../data-types/codeable-reference.md) | Le produit administré. |
| [!UICONTROL Basé sur] | `basedOn` | Tableau de [[!UICONTROL référence]](../data-types/reference.md) | Autorité sur laquelle se fonde l’événement de vaccination. |
| [!UICONTROL Dose] | `doseQuantity` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | La quantité de vaccin administrée. |
| [!UICONTROL Rencontre] | `encounter` | [[!UICONTROL Référence]](../data-types/reference.md) | La rencontre à laquelle l&#39;immunisation faisait partie. |
| [!UICONTROL Financement de Source] | `fundingSource` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | La source de financement du vaccin. |
| [!UICONTROL Identifiant] | `identifier` | Tableau d’[[!UICONTROL identifiant]](../data-types/identifier.md) | Identifiant de l’entreprise. |
| Source d’informations | `informationSource` | [[!UICONTROL Référence codable]](../data-types/codeable-reference.md) | Indique la source de l’enregistrement signalé. |
| [!UICONTROL Emplacement] | `location` | [[!UICONTROL Référence]](../data-types/reference.md) | Emplacement où la vaccination a eu lieu. |
| [!UICONTROL Fabricant] | `manufacturer` | [[!UICONTROL Référence codable]](../data-types/codeable-reference.md) | Le fabricant du vaccin. |
| [!UICONTROL Remarque] | `note` | Tableau d’[[!UICONTROL annotation]](../data-types/annotation.md) | Notes de vaccination supplémentaires. |
| [!UICONTROL Patient] | `patient` | [[!UICONTROL Référence]](../data-types/reference.md) | Qui a été vacciné. |
| [!UICONTROL Lot] | `performer` | Tableau d’objets | Qui a effectué l’événement de vaccination. Pour plus d’informations, consultez la [section ci-dessous](#performer). |
| [!UICONTROL Admissibilité au programme] | `programEligibility` | Tableau d’objets | Admissibilité du patient à un programme de vaccination spécifique. Pour plus d’informations, consultez la [section ci-dessous](#program-eligibility). |
| [!UICONTROL Protocole appliqué] | `protocolApplied` | Tableau d’objets | Protocole fourni par le fournisseur. Pour plus d’informations, consultez la [section ci-dessous](#protocol-applied). |
| [!UICONTROL Réaction] | `reaction` | Tableau d’objets | Les détails d&#39;une réaction après immunisation. Pour plus d’informations, consultez la [section ci-dessous](#reaction). |
| [!UICONTROL Raison] | `reason` | Tableau de [[!UICONTROL référence codable]](../data-types/codeable-reference.md) | La raison de la vaccination. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Comment le vaccin est entré dans le corps. |
| [!UICONTROL Site &#x200B;] | `site` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Site sur le corps où le vaccin a été administré |
| [!UICONTROL Motif du statut] | `statusReason` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Raison du statut actuel. |
| [!UICONTROL Raison sous-puissante] | `subpotentReason` | Tableau de [[!UICONTROL concept codable]](../data-types/codeable-concept.md) | La raison pour laquelle le vaccin est sous-puissant. |
| [!UICONTROL Informations annexes] | `supportingInformation` | Tableau de [[!UICONTROL référence]](../data-types/reference.md) | Informations supplémentaires à l’appui de la vaccination. |
| [!UICONTROL Code du vaccin] | `vaccineCode` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Le code du vaccin administré. |
| [!UICONTROL Date d’expiration] | `expirationDate` | Date | La date de péremption du vaccin. |
| [!UICONTROL Est Sous-Puissant] | `isSubpotent` | Booléen | Indicateur de sous-puissance du vaccin. |
| [!UICONTROL &#x200B; Numéro de lot &#x200B;] | `lotNumber` | Chaîne | Le numéro de lot du vaccin. |
| [!UICONTROL Date et heure de l’occurrence] | `occurenceDateTime` | DateTime | La date d’administration du vaccin. |
| [!UICONTROL Chaîne d’occurrence] | `occurenceString` | Chaîne | La date d’administration du vaccin. |
| [!UICONTROL Principal Source] | `primarySource` | Booléen | Indique si les données ont été capturées à partir d’une source principale. |
| [!UICONTROL Statut] | `status` | Chaîne | État de la vaccination. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `completed` </li> <li> `entered-in-error` </li> <li> `not-done` </li> |

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.schema.json)

## `performer` {#performer}

`performer` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![structure de l’intervenant](../../../images/healthcare/field-groups/immunization/performer.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Acteur &#x200B;] | `actor` | [[!UICONTROL Référence]](../data-types/reference.md) | La personne ou l’organisation qui exécutait le spectacle. |
| [!UICONTROL Fonction] | `function` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Quel type de performance a été effectué ? |

## `programEligibility` {#program-eligibility}

`programEligibility` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![programEligibility structure](../../../images/healthcare/field-groups/immunization/program-eligibility.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Programme] | `program` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Programme pour lequel l’éligibilité est déclarée. |
| [!UICONTROL Statut du programme] | `programStatus` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Statut d&#39;éligibilité du patient au programme. |

## `protocolApplied` {#protocol-applied}

`protocolApplied` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![protocolApplied, structure](../../../images/healthcare/field-groups/immunization/protocol-applied.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Autorité] | `authority` | [[!UICONTROL Référence]](../data-types/reference.md) | Qui est responsable de la publication des recommandations ? |
| [!UICONTROL Maladie ciblée] | `targetDisease` | Tableau de [[!UICONTROL concept codable]](../data-types/codeable-concept.md) | La maladie évitable ciblée par le vaccin. |
| [!UICONTROL Numéro de dose] | `doseNumber` | Chaîne | Le numéro de dose dans la série. |
| [!UICONTROL Série] | `series` | Chaîne | Nom de la série de vaccins. |
| [!UICONTROL Doses de série] | `seriesDoses` | Chaîne | Nombre recommandé de doses pour l’immunité. |

## `reaction` {#reaction}

`reaction` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![structure de réaction](../../../images/healthcare/field-groups/immunization/reaction.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Manifestation &#x200B;] | `manifestation` | [[!UICONTROL Référence codable]](../data-types/codeable-concept.md) | Informations supplémentaires sur la réaction. |
| [!UICONTROL Date] | `date` | DateTime | Quand la réaction a commencé. |
| [!UICONTROL Signalé] | `reported` | Chaîne | Indique si la réaction a été auto-déclarée. |

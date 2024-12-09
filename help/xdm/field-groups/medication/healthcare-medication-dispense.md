---
title: Groupe de champs du schéma de destination des médicaments
description: En savoir plus sur le groupe de champs Schéma de dépenses de médicaments .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 4%

---

# Groupe de champs de schéma [!UICONTROL Dépense de médicaments]

[!UICONTROL Dépense de médicaments] est un groupe de champs de schéma standard pour la [[!DNL Medication] classe](../../classes/location.md), la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) et la [[!DNL Provider class]](../../classes/provider.md). Il fournit un seul champ de type objet `healthcareMedicationDispense` qui capture les informations sur un médicament qui doit être ou qui a été dispensé pour une personne/un patient nommé.

![Structure de groupe de champs](../../images/field-groups/healthcare-medication-dispense/medication-dispense.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Autorisation De La Prescription] | `authorizingPrescription` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | L&#39;ordonnance qui permet de délivrer l&#39;ordonnance. |
| [!UICONTROL Basé Sur] | `basedOn` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Le plan sur lequel se fonde la distribution du médicament. |
| [!UICONTROL Catégorie] | `category` | Tableau de [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | La catégorie sous laquelle les médicaments sont délivrés, par exemple la catégorie juridique des médicaments ou la classification des médicaments. |
| [!UICONTROL Jours d’approvisionnement] | `daysSupply` | [[!UICONTROL Quantité simple]](../../data-types/healthcare/simple-quantity.md) | Le nombre de jours pendant lesquels le médicament fournira au patient. |
| [!UICONTROL Destination] | `destination` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | L’installation ou le lieu où le médicament a été ou sera expédié, dans le cadre de l’événement de délivrance. |
| [!UICONTROL Instruction de publication] | `dosageInstruction` | Tableau de [[!UICONTROL Dosage]](../../data-types/healthcare/dosage.md) | Décrit comment le médicament doit être utilisé par le patient. |
| [!UICONTROL Rencontre] | `encounter` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | La rencontre qui définit le contexte de cet événement. |
| [!UICONTROL Historique des événements] | `eventHistory` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Résumé des événements qui se sont produits autour de la diffusion. |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../../data-types/healthcare/identifier.md) | Identifiants associés à la diffusion. Les identifiants doivent être définis par des processus d’entreprise et/ou utilisés pour y faire référence lorsqu’une référence URL directe n’est pas appropriée. |
| [!UICONTROL Emplacement] | `location` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | L&#39;emplacement physique principal où le médicament a été dispensé. |
| [!UICONTROL Medication] | `medication` | [[!UICONTROL Référence codeable]](../../data-types/healthcare/codeable-reference.md) | Identifie le médicament demandé. Il doit s’agir d’un lien vers une ressource qui représente les détails du médicament, ou d’un code qui identifie le médicament. |
| [!UICONTROL Raison non exécutée] | `notPerformedReason` | [[!UICONTROL Référence codeable]](../../data-types/healthcare/codeable-reference.md) | La raison pour laquelle le médicament n&#39;a pas été dispensé. |
| [!UICONTROL Remarque] | `note` | Tableau de [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Informations supplémentaires sur la diffusion. |
| [!UICONTROL Partie De] | `partOf` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | La procédure ou la demande de médicament qui a déclenché la délivrance. |
| [!UICONTROL Performer] | `performer` | Tableau d’objets | Indique qui ou quoi a exécuté l’événement de diffusion. Pour plus d’informations, consultez la [section ci-dessous](#performer) . |
| [!UICONTROL Quantity] | `quantity` | [[!UICONTROL Quantité simple]](../../data-types/healthcare/simple-quantity.md) | La quantité de médicaments délivrés, y compris l&#39;unité de mesure. |
| [!UICONTROL Receiver] | `receiver` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Identifie la personne qui a pris le médicament ou l’emplacement où il a été livré. |
| [!UICONTROL Objet] | `subject` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Lien vers une ressource représentant la personne ou le groupe à qui le médicament sera donné. |
| [!UICONTROL Substitution] | `substitution` | Objet | Indique si la substitution a été faite ou non dans le cadre de la livraison. Contient quatre propriétés : <li>`wasSubstituted` : valeur booléenne true si le distributeur a demandé une substitution.</li> <li>`type` : valeur [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) qui fournit un code indiquant si une substitution a été effectuée.</li> <li>`reason` : un tableau de valeurs [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) qui contient les raisons de la substitution.</li> <li>`responsibleParty` : valeur [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) qui fournit la personne ou la partie responsable de la substitution. </li> |
| [!UICONTROL Informations complémentaires] | `supportingInformation` | Tableau de [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Informations supplémentaires qui soutiennent le traitement dispensé. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Décrit le type d’événement de diffusion exécuté, par exemple un remplissage d’urgence ou partiel. |
| [!UICONTROL Enregistré] | `recorded` | DateTime | Date et heure de démarrage de l’activité de diffusion si `whenPrepared` ou `whenHandedOver` n’est pas renseigné. |
| [!UICONTROL Instruction de publication affichée] | `renderedDosageInstruction` | Chaîne | Représentation complète de la dose incluse dans toutes les instructions de dosage. À utiliser lorsque plusieurs instructions posologiques sont incluses pour représenter des doses complexes, telles que l’augmentation ou la réduction de doses. |
| [!UICONTROL Statut] | `status` | Chaîne | État de la diffusion. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL État modifié] | `statusChanged` | DateTime | Date et heure auxquelles l’état de l’enregistrement de diffusion a changé. |
| [!UICONTROL Lorsqu’il est transféré] | `whenHandedOver` | DateTime | Date et heure auxquelles le médicament administré a été fourni au patient. |
| [!UICONTROL Lorsqu’il est préparé] | `whenPrepared` | DateTime | Date et heure auxquelles le médicament administré a été emballé et examiné. |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![Structure de l’interprète](../../images/field-groups/healthcare-medication-dispense/performer.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Acteur] | `actor` | [[!UICONTROL Référence]](../../data-types/healthcare/reference.md) | Le praticien (ou similaire) qui a effectué l’action. On devrait supposer que l&#39;acteur est le dispensateur du médicament. |
| [!UICONTROL Fonction] | `function` | [[!UICONTROL Concept codeable]](../../data-types/healthcare/codeable-concept.md) | Type d’interprète dans la diffusion, par exemple l’initiateur de dates, le programme de package ou le vérificateur final. |

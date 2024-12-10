---
title: Groupe de champs de schéma de demande de médicaments
description: En savoir plus sur le groupe de champs Schéma de demande de médicaments .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 8502380f-9557-4ca6-84bc-65010dfc6066
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 3%

---

# Groupe de champs de schéma [!UICONTROL Demande de médicaments]

[!UICONTROL Demande de médicaments] est un groupe de champs de schéma standard pour la [[!DNL Medication] classe](../../../classes/medication.md), la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) et la [[!DNL Provider class]](../../../classes/provider.md). Il fournit un seul champ de type objet `healthcareMedicationDispense` qui capture une commande ou une demande pour la livraison du médicament et les instructions pour l&#39;administration du médicament à un patient.

![Structure de groupe de champs](../../../images/healthcare/field-groups/medication-request/medication-request.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Basé Sur] | `basedOn` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | Le plan ou la demande qui est rempli par cette demande de médicament. |
| [!UICONTROL Catégorie] | `category` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | La catégorisation ou le regroupement de la demande de médicament. |
| [!UICONTROL Type De Cours De Thérapie] | `courseOfTherapyType` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | La description du schéma général pour l&#39;administration du traitement au patient. |
| [!UICONTROL Appareil] | `device` | Tableau de [[!UICONTROL référence codeable]](../data-types/codeable-reference.md) | Type d’appareil à utiliser pour l’administration du médicament. |
| [!UICONTROL Demande de dépenses] | `dispenseRequest` | Objet | Indique les détails spécifiques de la demande de délivrance, souvent appelée commande de médicaments. Pour plus d’informations, consultez la [section ci-dessous](#dispense-request) . |
| [!UICONTROL Instruction de publication] | `dosageInstructions` | Tableau de [[!UICONTROL Dosage]](../data-types/dosage.md) | Instructions spécifiques sur la façon dont le médicament doit être utilisé par le patient. |
| [!UICONTROL Période effective] | `effectiveDosePeriod` | [[!UICONTROL Période]](../data-types/period.md) | La période pendant laquelle le traitement doit être pris. Lorsqu’il existe plusieurs lignes `dosageInstruction` (par exemple, lors de la réduction des doses), il s’agit de la date la plus ancienne et de la date la plus récente des instructions de dosage. |
| [!UICONTROL Rencontre] | `encounter` | [[!UICONTROL Référence]](../data-types/reference.md) | La rencontre au cours de laquelle la requête a été créée. |
| [!UICONTROL Historique des événements] | `eventHistory` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | Lien vers les enregistrements d’événements liés à la demande de médicaments, tels que le respect de la demande, les moments de transition clé de l’état ou les mises à jour pertinentes. |
| [!UICONTROL Identifiant de groupe] | `groupIdentifier` | [[!UICONTROL Identifiant]](../data-types/identifier.md) | Identifiant partagé sur plusieurs instances de requête indépendantes qui ont été activées par un seul auteur. |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../data-types/identifier.md) | Les identifiants associés à la demande de médicaments qui sont définis par les processus d’entreprise et/ou sont utilisés pour y faire référence lorsqu’une référence URL directe à la ressource elle-même n’est pas appropriée. |
| [!UICONTROL Source d’informations] | `informationSource` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | Personne ou organisation qui a fourni les informations pour la demande si la source est autre que `requester`. |
| [!UICONTROL Assurance] | `insurance` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | les plans d’assurance, les extensions de couverture, les préautorisations et/ou les prédéterminations qui peuvent être requis pour la prestation du service demandé. |
| [!UICONTROL Medication] | `medication` | [[!UICONTROL Référence codeable]](../data-types/codeable-reference.md) | Identifie le médicament demandé. Il doit s’agir d’un lien vers une ressource qui représente les détails du médicament, ou d’un code qui identifie le médicament. |
| [!UICONTROL Remarque] | `note` | Tableau de [[!UICONTROL Annotation]](../data-types/annotation.md) | Informations supplémentaires sur la prescription qui n’a pas pu être transmise par les autres attributs. |
| [!UICONTROL Performer] | `performer` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | L’agent spécifié du traitement/de l’administration du médicament. Pour les appareils, il s’agit de l’appareil destiné à administrer le traitement. |
| [!UICONTROL Type de personne] | `performerType` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Indique le type d’intervenant pour l’administration du médicament. |
| [!UICONTROL Prescription préalable] | `priorPrescription` | [[!UICONTROL Référence]](../data-types/reference.md) | Référence à une commande ou une ordonnance qui est remplacée par cette demande. |
| [!UICONTROL Motif] | `reason` | Tableau de [[!UICONTROL référence codeable]](../data-types/reference.md) | La raison ou l’indication de la commande ou non du médicament. |
| [!UICONTROL Enregistreur] | `recorder` | [[!UICONTROL Référence]](../data-types/reference.md) | La personne qui a saisi la commande au nom d’une autre personne. |
| [!UICONTROL Requester] | `requester` | [[!UICONTROL Référence]](../data-types/reference.md) | Personne, organisation ou appareil qui a initié la demande et est responsable de son activation. |
| [!UICONTROL Raison de l’état] | `statusReason` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Motif de l’état actuel de la requête. |
| [!UICONTROL Objet] | `subject` | [[!UICONTROL Référence]](../data-types/reference.md) | La personne ou le groupe pour lequel le traitement a été demandé. |
| [!UICONTROL Substitution] | `substitution` | Objet | Indique si une substitution peut ou non faire partie de la distribution. Contient trois propriétés : <li>`allowedBoolean` : valeur booléenne vraie si le prescripteur autorise une substitution.</li> <li>`allowedCodeableConcept` : valeur [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) qui fournit un code si le prescripteur autorise une substitution.</li> <li>`reason` : valeur [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) qui indique une raison de la substitution.</li> |
| [!UICONTROL Informations complémentaires] | `supportingInformation` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | Des informations pour aider le patient à prendre ses médicaments, comme sa taille et son poids. |
| [!UICONTROL Créé Le ] | `authoredOn` | DateTime | Date (et éventuellement heure) à laquelle l’ordonnance a été écrite. |
| [!UICONTROL Ne Pas Effectuer] | `doNotPerform` | Booléen | Un indicateur booléen qui est vrai est que le patient doit arrêter (ou ne pas commencer) de prendre le médicament. |
| [!UICONTROL Intent] | `intent` | Chaîne | L’intention de la demande. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `proposal` </li> <li> `plan` </li> <li> `order` </li> <li> `original-order` </li> <li> `reflex-order` </li> <li> `filler-order` </li> <li> `instance-order` </li> <li> `option` </li> |
| [!UICONTROL Priorité] | `priority` | Chaîne | Priorité de la requête. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `routine` </li> <li> `urgent` </li> <li> `asap` </li> <li> `stat` </li> |
| [!UICONTROL Instruction de publication affichée] | `renderedDosageInstruction` | Chaîne | Représentation complète de la dose incluse dans toutes les instructions de dosage. À utiliser lorsque plusieurs instructions posologiques sont incluses pour représenter des doses complexes, telles que l’augmentation ou la réduction de doses. |
| [!UICONTROL Signalé] | `reported` | Booléen | Indique si cet enregistrement a été capturé en tant qu’enregistrement secondaire signalé plutôt qu’en tant qu’enregistrement source principal de vérité original. |
| [!UICONTROL Statut] | `status` | Chaîne | État de la diffusion. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL État modifié] | `statusChanged` | DateTime | Date (et éventuellement heure) à laquelle l’état de a changé. |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationrequest.schema.json)

## `dispenseRequest` {#dispense-request}

`dispenseRequest` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![Structure de la demande de dépenses](../../../images/healthcare/field-groups/medication-request/dispense-request.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Intervalle de dépenses] | `dispenseInterval` | [[!UICONTROL Durée]](../data-types/duration.md) | La période minimale qui doit s’écouler entre la délivrance du médicament. |
| [!UICONTROL Disdistribueur] | `dispenser` | [[!UICONTROL Référence]](../data-types/reference.md) | L’organisme prévu qui distribuera le médicament comme indiqué par le prescripteur. |
| [!UICONTROL Instruction au distributeur] | `dispenserInstruction` | Tableau de [[!UICONTROL Annotation]](../data-types/annotation.md) | Informations supplémentaires pour le dispensateur, telles que conseils à fournir au patient |
| [!UICONTROL Aide à l’administration des doses] | `doseAdministrationAid` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Informations sur le type d&#39;emballage d&#39;adhérence à fournir pour la délivrance du médicament. |
| [!UICONTROL Durée de ravitaillement attendue] | `expectedSupplyDuration` | [[!UICONTROL Durée]](../data-types/duration.md) | La période pendant laquelle le produit fourni doit être utilisé ou la durée de la diffusion est attendue. |
| [!UICONTROL  Premier remplissage] | `initialFill` | Objet | Informations pour le remplissage initial. Contient deux propriétés : <li>`quantity` : valeur [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) qui fournit la quantité à fournir lors de la première diffusion.</li> <li>`duration` : valeur [[!UICONTROL Duration]](../data-types/duration.md) qui indique la durée de la première diffusion.</li> |
| [!UICONTROL Quantity] | `quantity` | [[!UICONTROL Quantité simple]](../data-types/simple-quantity.md) | Montant à distribuer pour un remplissage. |
| [!UICONTROL Période de validité] | `validityPeriod` | [[!UICONTROL Période]](../data-types/period.md) | La période de validité de la prescription. |
| [!UICONTROL Nombre De Répétements Autorisés] | `numberOfRepeatsAllowed` | Nombre entier | Nombre de recharges autorisé, avec une valeur minimale de 0. |

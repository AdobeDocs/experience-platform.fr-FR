---
title: Groupe de champs du schéma de couverture
description: Découvrez le groupe de champs de schéma de couverture.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 7b84c0cf-3bd4-4ba8-a8cc-85e6b3f2b59e
TQID: https://experienceleague.adobe.com/VErK3GE5VWp11FPYJiGQU3qlRmK2TlIyVoCMMsbW3P4
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 793
ht-degree: 6%

---

# Groupe de champs de schéma [!UICONTROL Couverture]

[!UICONTROL Couverture] est un groupe de champs de schéma standard pour la [[!DNL Plan] classe](../../../classes/plan.md). Il fournit un champ unique de type objet `healthcareCoverage` qui est destiné à fournir les identifiants et descripteurs de haut niveau d’un régime d’assurance, généralement les informations qui figureraient sur une carte d’assurance, qui peuvent être utilisés pour payer, en tout ou en partie, la fourniture de produits et de services de soins de santé.

![Structure du groupe de champs](../../../images/healthcare/field-groups/coverage/coverage.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Bénéficiaire du plan] | `beneficiary` | [[!UICONTROL Référence]](../data-types/reference.md) | La partie qui bénéficie de la couverture d&#39;assurance et le patient lorsque les produits ou services sont fournis. |
| [!UICONTROL Classe] | `class` | Tableau d’objets | Une suite de classificateurs spécifiques au souscripteur. Pour plus d’informations, consultez la [section ci-dessous](#class). |
| [!UICONTROL &#x200B; Contact &#x200B;] | `contract` | Tableau de [[!UICONTROL référence]](../data-types/reference.md) | Police(s) qui constituent cette couverture d’assurance. |
| [!UICONTROL Coût Pour Le Bénéficiaire] | `costToBeneficiary` | Tableau d’objets | Une suite de codes indiquant le poste de coût et le montant associé qui ont été détaillés dans la police et qui peuvent avoir été inclus sur la carte santé. Pour plus d’informations, consultez la [section ci-dessous](#cost-to-beneficiary). |
| [!UICONTROL Exception &#x200B;] | `exception` | Tableau d’objets | Une suite de codes indiquant les exceptions ou les réductions des coûts pour les patients et leurs périodes d&#39;effet. Pour plus d’informations, consultez la [section ci-dessous](#exception). |
| [!UICONTROL Identifiant] | `identifier` | Tableau d’[[!UICONTROL identifiant]](../data-types/identifier.md) | Identifiant de la couverture telle qu’elle est émise par l’assureur. |
| [!UICONTROL Régime d&#39;assurance] | `insurancePlan` | [[!UICONTROL Référence]](../data-types/reference.md) | Le plan d’assurance détaille, les avantages et les coûts qui constituent cette couverture d’assurance. |
| [!UICONTROL Assureur] | `insurer` | [[!UICONTROL Référence]](../data-types/reference.md) | Souscripteur, payeur ou compagnie d’assurance du programme ou du plan. |
| [!UICONTROL Paiement par] | `paymentBy` | Tableau d’objets | Le lien vers le payeur et éventuellement ce qu’il sera responsable de payer. Pour plus d’informations, consultez la [section ci-dessous](#payment-by). |
| [!UICONTROL Dates De Début Et De Fin De La Couverture] | `period` | [[!UICONTROL Période]](../data-types/period.md) | Période pendant laquelle la couverture est active. Une date de début manquante indique que la date de début n’est pas connue, une date de fin manquante signifie que la couverture est en cours. |
| [!UICONTROL Titulaire de police] | `policyHolder` | [[!UICONTROL Référence]](../data-types/reference.md) | Partie qui détient la police d’assurance. |
| [!UICONTROL Relation avec le bénéficiaire] | `relationship` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Relation entre le bénéficiaire et l’abonné. |
| [!UICONTROL Abonné] | `subscriber` | [[!UICONTROL Référence]](../data-types/reference.md) | Partie qui détient la relation contractuelle avec la police. |
| [!UICONTROL Identifiant de l’abonné] | `subscriberId` | Tableau d’[[!UICONTROL identifiant]](../data-types/identifier.md) | ID attribué par l’assureur à l’abonné. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Type de couverture. |
| [!UICONTROL Nombre Dépendant] | `dependent` | Chaîne | Indicateur d’une personne à charge couverte. |
| [!UICONTROL Type] | `kind` | Chaîne | Le type de couverture. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `insurance` </li> <li> `self-pay` </li> <li> `other` </li> |
| [!UICONTROL Réseau d’assureurs] | `network` | Chaîne | Le réseau de prestataires auquel le bénéficiaire peut demander un traitement qui sera couvert au tarif du réseau, sinon les conditions applicables en dehors du réseau. |
| [!UICONTROL Ordre de couverture] | `order` | Entier | Ordre relatif de la couverture, avec une valeur minimale de `0`. |
| [!UICONTROL Statut] | `status` | Chaîne | Statut de la couverture. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `active` </li> <li> `cancelled` </li> <li> `draft` </li> <li> `entered-in-error` </li> |
| [!UICONTROL Subrogation] | `subrogation` | Booléen | Lorsqu’elle est `true`, cette instance d’assurance a été incluse non pas pour l’arbitrage, mais pour fournir aux assureurs les détails permettant de récupérer les coûts. |

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `class` {#class}

`class` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![Structure de classe](../../../images/healthcare/field-groups/coverage/class.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Type] | `type` | Tableau de [[!UICONTROL concept codable]](../data-types/codeable-concept.md) | Type de classification pour lequel un libellé de classe spécifique à l’assureur, ou un numéro et un nom facultatif, est fourni. Par exemple, le type peut être utilisé pour identifier une catégorie de couverture, un groupe d&#39;employeurs, une police ou un plan. |
| [!UICONTROL Valeur] | `value` | [[!UICONTROL Identifiant]](../data-types/identifier.md) | Identifiant alphanumérique associé à l’étiquette émise par l’assureur. |
| [!UICONTROL Nom] | `name` | Chaîne | Brève description de la classe . |

## `costToBeneficiary` {#cost-to-beneficiary}

`costToBeneficiary` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![Coût pour la structure du bénéficiaire](../../../images/healthcare/field-groups/coverage/cost-to-beneficiary.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Catégorie] | `category` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Code permettant d’identifier le type général d’avantages en vertu desquels les produits et services sont fournis. |
| [!UICONTROL Réseau] | `network` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Code permettant d’indiquer si les avantages se rapportent aux fournisseurs intégrés au réseau ou à ceux hors réseau. |
| [!UICONTROL Terme] | `term` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Terme des valeurs telles que la prestation maximale à vie. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | La catégorie des coûts liés au traitement qui sont centrés sur le patient. |
| [!UICONTROL Unité] | `unit` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Indique si les avantages s&#39;appliquent à une personne ou à la famille. |

## `exception` {#exception}

`exception` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![Structure des exceptions](../../../images/healthcare/field-groups/coverage/exception.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Type] | `type` | [[!UICONTROL Concept codable]](../data-types/codeable-concept.md) | Code de l’exception spécifique. |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | La période pendant laquelle l’exception est active. |

## `paymentBy` {#payment-by}

`paymentBy` est fourni sous la forme d’un tableau d’objets . La structure de chaque objet est décrite ci-dessous.

![Paiement par structure](../../../images/healthcare/field-groups/coverage/payment-by.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Parti] | `party` | [[!UICONTROL Référence]](../data-types/reference.md) | La liste des parties fournissant des paiements hors assurance pour les coûts de traitement. |
| [!UICONTROL Responsabilité] | `responsibility` | Chaîne | Description de la responsabilité financière. |

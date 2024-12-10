---
title: Groupe de champs de schéma de compte
description: Découvrez le groupe de champs Schéma du compte .
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 376716bd-f79f-421d-b163-0f0e50876b48
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 7%

---

# Groupe de champs de schéma [!UICONTROL Compte]

[!UICONTROL Account] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../../classes/individual-profile.md) et le [[!DNL Provider class]](../../../classes/provider.md). Il fournit un champ de type objet unique `healthcareAccount` qui est utilisé pour enregistrer les transactions, les services et d’autres informations financières relatives aux services de santé fournis à un patient ou à un groupe d’individus (par exemple à des fins de police d’assurance ou de facturation).

![Structure de groupe de champs](../../../images/healthcare/field-groups/account/account.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Balance] | `balance` | Tableau d’objets | Les soldes de comptes qui sont calculés et traités par le système financier. Pour plus d’informations, voir la [section-ci-dessous](#balances) . |
| [!UICONTROL État de facturation] | `billingStatus` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Cela suit le cycle de vie du compte tout au long du processus de facturation. Elle indique comment les transactions sont traitées lorsqu’elles sont affectées au compte. |
| [!UICONTROL Couverture] | `coverage` | Tableau d’objets | Le(s) responsable(s) des coûts de ce compte et dans quel ordre doivent-ils être appliqués. Pour plus d’informations, consultez la [section ci-dessous](#coverage) . |
| [!UICONTROL Devise] | `currency` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Devise par défaut du compte. |
| [!UICONTROL Diagnostic] | `diagnosis` | Tableau d’objets | L’ensemble des diagnostics pertinents pour la facturation est stocké ici sur le compte où ils peuvent être séquencés de manière appropriée avant le traitement afin de produire la ou les demandes. Pour plus d’informations, consultez la [section ci-dessous](#diagnosis) . |
| [!UICONTROL Garant] | `guarantor` | Tableau d’objets | Les parties responsables de l&#39;équilibrage du compte si d&#39;autres options de paiement ne sont pas suffisantes. Pour plus d’informations, consultez la [section ci-dessous](#guarantor) . |
| [!UICONTROL Identifiant] | `identifier` | Tableau de [[!UICONTROL Identifiant]](../data-types/identifier.md) | Identifiant unique utilisé pour référencer le compte. Il peut ou non être destiné à un usage humain (par exemple, numéro de carte de crédit). |
| [!UICONTROL Propriétaire] | `owner` | [[!UICONTROL Référence]](../data-types/reference.md) | Indique la zone de service, l’hôpital, le service, etc. avec la responsabilité de la gestion du compte. |
| [!UICONTROL Procédure] | `procedure` | Tableau d’objets | L’ensemble des procédures pertinentes pour la facturation est stocké ici sur le compte où elles peuvent être séquencées de manière appropriée avant le traitement afin de produire la ou les demandes. Pour plus d’informations, consultez la [section ci-dessous](#procedure) . |
| [!UICONTROL Compte associé] | `relatedAccount` | Tableau d’objets | Autres comptes associés liés à ce compte. Pour plus d’informations, consultez la [section ci-dessous](#related-account) . |
| [!UICONTROL Période de service] | `servicePeriod` | [[!UICONTROL Période]](../data-types/period.md) | La période des services associés à ce compte. |
| [!UICONTROL Objet] | `subject` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | Identifie l’entité qui engage les dépenses. Bien que les destinataires immédiats de services ou de marchandises puissent être des entités liées au sujet, les dépenses ont finalement été engagées par l&#39;objet du compte. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Classe le compte à des fins de création de rapports et de recherche. |
| [!UICONTROL Calculé À] | `calculatedAt` | DateTime | Heure à laquelle le solde a été calculé. |
| [!UICONTROL Description] | `description` | Chaîne | Fournit des informations supplémentaires sur le suivi du compte et son utilisation. |
| [!UICONTROL Nom] | `name` | Chaîne | Nom du compte. |
| [!UICONTROL Statut] | `status` | Chaîne | État du compte. La valeur de cette propriété doit être égale à l’une des valeurs d’énumération connues suivantes. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> <li> `on-hold` </li> <li> `unknown`</li> |

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/account.schema.json)

## `balances` {#balances}

`balances` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure des soldes](../../../images/healthcare/field-groups/account/balance.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Agrégat] | `aggregate` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Qui doit payer cette partie du solde ? |
| [!UICONTROL Amount] | `amount` | [[!UICONTROL Money]](../data-types/money.md) | Le solde réel calculé pour l’âge défini dans la propriété term. |
| [!UICONTROL Term] | `term` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Terme du compte. |
| [!UICONTROL Estimateur] | `estimate` | Booléen | Si le montant est une valeur estimée. |

## `coverage` {#coverage}

`coverage` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure de couverture](../../../images/healthcare/field-groups/account/coverage.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Couverture] | `coverage` | [[!UICONTROL Référence]](../data-types/reference.md) | Le(s) responsable(s) des coûts de ce compte et dans quel ordre doivent-ils être appliqués. |
| [!UICONTROL Priorité] | `priority` | Nombre entier | La priorité de la couverture dans le contexte de ce compte, avec une valeur minimale de `0`. |

## `diagnosis` {#diagnosis}

`diagnosis` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure du diagnostic](../../../images/healthcare/field-groups/account/diagnosis.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Condition] | `condition` | [[!UICONTROL Référence codeable]](../data-types/codeable-reference.md) | Diagnostic pertinent pour le compte. |
| [!UICONTROL Code de module] | `packageCode` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Le code de package peut être utilisé pour regrouper les diagnostics qui peuvent être facturés ou livrés comme un seul produit (comme les DRG). |
| [!UICONTROL Type] | `type` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Type que ce diagnostic a en rapport avec le compte (par exemple admission, facturation, décharge, etc.). |
| [!UICONTROL Date De Diagnostic] | `dateOfDiagnosis` | DateTime | Date du diagnostic (au moment du diagnostic codé). |
| [!UICONTROL  On Admission] | `onAdmission` | Booléen | Si le diagnostic était présent à l&#39;admission. |
| [!UICONTROL Séquence] | `sequence` | Nombre entier | Classement du diagnostic (pour chaque type), avec une valeur minimale de `0`. |

## `guarantor` {#guarantor}

`guarantor` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![Structure du garant](../../../images/healthcare/field-groups/account/guarantor.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Party] | `party` | [[!UICONTROL Référence]](../data-types/reference.md) | L’entité responsable. |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | Période pendant laquelle le garant accepte la responsabilité du compte. |
| [!UICONTROL En attente] | `onHold` | Booléen | Un garant peut être mis à la crédit ou avoir temporairement suspendu son rôle. |

## `procedure` {#procedure}

`procedure` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure de procédure](../../../images/healthcare/field-groups/account/procedure.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Référence codeable]](../data-types/codeable-reference.md) | La procédure relative au compte. |
| [!UICONTROL Appareil] | `device` | Tableau de [[!UICONTROL Référence]](../data-types/reference.md) | Tous les périphériques associés à la procédure relative au compte. |
| [!UICONTROL Type] | `type` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Utilisation de la valeur de la procédure pour charger le compte. |
| [!UICONTROL Code de module] | `packageCode` | Tableau de [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Le code de package peut être utilisé pour regrouper des procédures qui peuvent être évaluées ou livrées sous la forme d’un seul produit (comme les DRG). |
| [!UICONTROL Date Du Service] | `dateOfService` | DateTime | Date à laquelle utiliser une procédure codée. Si vous utilisez une référence à une procédure, la date de la procédure doit être utilisée. |
| [!UICONTROL Séquence] | `sequence` | Nombre entier | Classement de la procédure (pour chaque type), avec une valeur minimale de `0`. |

## `relatedAccount` {#related-account}

`relatedAccount` est fourni sous la forme d’un tableau d’objets. La structure de chaque objet est décrite ci-dessous.

![structure relatedAccount](../../../images/healthcare/field-groups/account/related-account.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Compte] | `account` | [[!UICONTROL Référence]](../data-types/reference.md) | Référence à un compte associé. |
| [!UICONTROL Relation] | `relationship` | [[!UICONTROL Concept codeable]](../data-types/codeable-concept.md) | Relation du compte associé. |

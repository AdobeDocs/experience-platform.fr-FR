---
title: Groupe de champs de schéma Détails du plan de soins de santé
description: En savoir plus sur le groupe de champs Détails du plan de soins de santé .
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 9%

---

# Groupe de champs [!UICONTROL Détails du plan de soins de santé]

[!UICONTROL Health Care Plan Details] est un groupe de champs de schéma standard pour la classe [[!UICONTROL Plan]](../../classes/plan.md). Il fournit un champ de type objet unique `healthcarePlanDetails` qui capture les propriétés liées à un plan médical.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `networkDetails` | Tableau d’objets | Répertorie les détails du ou des réseaux définis par l&#39;assureur des fournisseurs auxquels le bénéficiaire peut demander un traitement et qui seront couverts au taux &quot;en réseau&quot;. Chaque objet comprend les propriétés suivantes : <ul><li>`networkID` : (chaîne). Identifiant spécifique à l’assureur pour le réseau.</li><li>`networkName` : (chaîne). Nom spécifique à l’assureur pour le réseau.</li></ul> |
| `affiliations` | Tableau de chaînes | Liste des entités commerciales affiliées au plan. |
| `coverageType` | Chaîne | Type de couverture du plan. Les valeurs acceptées sont les suivantes :<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booléen | Indique si le plan est actif. |
| `lastVerificationDate` | DateTime | La date de la dernière vérification du plan. |
| `payerID` | Chaîne | L’identifiant unique du payeur (en d’autres termes, le fournisseur d’assurance du plan). |
| `planLevel` | Chaîne | Indique le niveau du plan. Les valeurs acceptées sont les suivantes :<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Chaîne | Indique le type de plan. Les valeurs acceptées sont les suivantes :<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Chaîne | Le type de propriétaire auquel un forfait est destiné. Il peut s’agir d’un individu, d’un groupe, d’une organisation, etc. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).

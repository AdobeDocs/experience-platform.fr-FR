---
title: Groupe de champs de schéma Détails du plan de soins de santé
description: Ce document présente un aperçu du groupe de champs Détails du plan de soins de santé .
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 9%

---

# [!UICONTROL Détails du plan de soins de santé] groupe de champs de schéma

[!UICONTROL Détails du plan de soins de santé] est un groupe de champs de schéma standard pour la variable [[!UICONTROL Plan] class](../../classes/plan.md). Il fournit un champ de type objet unique. `healthcarePlanDetails` qui capture les propriétés liées à un plan médical.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `networkDetails` | Tableau d’objets | Répertorie les détails du ou des réseaux définis par l&#39;assureur des fournisseurs auxquels le bénéficiaire peut demander un traitement et qui seront couverts au taux &quot;en réseau&quot;. Chaque objet comprend les propriétés suivantes : <ul><li>`networkID`: (Chaîne) Identifiant spécifique à l’assureur pour le réseau.</li><li>`networkName`: (Chaîne) Nom spécifique de l’assureur pour le réseau.</li></ul> |
| `affiliations` | Tableau de chaînes | Liste des entités commerciales affiliées au plan. |
| `coverageType` | Chaîne | Type de couverture du plan. Les valeurs acceptées sont les suivantes :<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booléen | Indique si le plan est principal. |
| `lastVerificationDate` | DateTime | Date à laquelle le plan a été vérifié pour la dernière fois. |
| `payerID` | Chaîne | L’identifiant unique du payeur (en d’autres termes, le fournisseur d’assurance du plan). |
| `planLevel` | Chaîne | Indique le niveau du plan. Les valeurs acceptées sont les suivantes :<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Chaîne | Indique le type de plan. Les valeurs acceptées sont les suivantes :<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Chaîne | Le type de propriétaire auquel un forfait est destiné. Il peut s’agir d’un individu, d’un groupe, d’une organisation, etc. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous à la section [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).

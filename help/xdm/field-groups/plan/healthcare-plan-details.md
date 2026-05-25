---
title: Groupe de champs de schéma Détails du plan de soins de santé
description: Découvrez le groupe de champs de schéma Détails du plan de soins de santé .
exl-id: 5a480c5b-74f8-48dd-858a-5cf2628dc7f0
TQID: https://experienceleague.adobe.com/jQwPtDXiKRM87D2VJBNG9hY-2PzrkJXFq7C6Tc5VJag
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 9%

---

# [!UICONTROL Healthcare Plan Details] groupe de champs de schéma

[!UICONTROL Healthcare Plan Details] est un groupe de champs de schéma standard pour la classe [[!UICONTROL Plan]](../../classes/plan.md). Il fournit un `healthcarePlanDetails` de champ de type objet unique qui capture les propriétés liées à un plan médical.

![](../../images/field-groups/plan/healthcare-plan-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `networkDetails` | Tableau d’objets | Dresse la liste des coordonnées du ou des réseaux de prestataires définis par l’assureur auxquels le bénéficiaire peut demander un traitement, et sera couvert au taux « in-network ». Chaque objet comprend les propriétés suivantes : <ul><li>`networkID` : (chaîne) ID spécifique à l’assureur pour le réseau.</li><li>`networkName` : (chaîne). Nom spécifique à l’assureur pour le réseau.</li></ul> |
| `affiliations` | Tableau de chaînes | Liste des entités commerciales affiliées au plan. |
| `coverageType` | Chaîne | Type de couverture du plan. Les valeurs acceptées sont les suivantes :<ul><li>`medical`</li><li>`dental`</li><li>`vision`</li><li>`accident`</li></ul> |
| `isActive` | Booléen | Indique si le plan est actif. |
| `lastVerificationDate` | DateTime | Date de la dernière vérification du plan. |
| `payerID` | Chaîne | Identifiant unique du payeur (en d’autres termes, le fournisseur d’assurance du plan). |
| `planLevel` | Chaîne | Indique le niveau du plan. Les valeurs acceptées sont les suivantes :<ul><li>`primary`</li><li>`secondary`</li><li>`tertiary`</li><li>`quaternary`</li></ul> |
| `planType` | Chaîne | Indique le type de plan. Les valeurs acceptées sont les suivantes :<ul><li>`hmo`</li><li>`epo`</li><li>`pos`</li><li>`hdhp`</li></ul> |
| `targetOwnerType` | Chaîne | Type de propriétaire auquel un plan est destiné. Par exemple, un individu, un groupe, une organisation, etc. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/plan/healthcare-plan-details.schema.json).

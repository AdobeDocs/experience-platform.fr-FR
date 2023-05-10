---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;télécoms;abonnement;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'abonnement aux télécommunications
description: Ce document présente un aperçu du type de données XDM (Modèle de données d’expérience d’abonnement aux services de télécommunication).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 19%

---

# [!UICONTROL Abonnement aux télécommunications] type de données

[!UICONTROL Abonnement aux télécommunications] est un type de données XDM (Experience Data Model) standard qui décrit les détails de types d’abonnement aux télécommunications spécifiques, tels qu’Internet, mobile, média ou ligne fixe.

>[!NOTE]
>
>Ce document décrit le type de données. Pour le groupe de champs du même nom, reportez-vous à la section [[!UICONTROL Abonnement aux télécommunications] guide de référence des groupes de champs](../field-groups/profile/telecom-subscription.md).
>
>Si vous décrivez un type d&#39;abonnement sans rapport avec l&#39;industrie des télécommunications, utilisez le générique [[!UICONTROL Abonnement] type de données](./subscription.md) au lieu de .

![Structure de l&#39;abonnement aux télécommunications](../images/data-types/telecom-subscription/structure.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `devices` | Tableau d’objets | Décrit une liste des appareils et/ou accessoires associés au plan. Voir [section ci-dessous](#devices) pour plus d’informations sur la structure attendue de chaque élément de tableau. |
| `subscriber` | [[!UICONTROL Personne]](./person.md) | Décrit le propriétaire de l’abonnement. |
| `ID` | Chaîne | Identifiant unique de l’instance d’abonnement. |
| `billingPeriod` | Chaîne | Durée entre deux facturations. |
| `billingStartDate` | Date | Date à laquelle la période de facturation commence. Le format de date (sans heure) doit suivre le [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `chargeMethod` | Chaîne | Configuration de la facturation au client. |
| `contractID` | Chaîne | L’identifiant unique du contrat qui régit cet abonnement. |
| `country` | Chaîne | Pays dans lequel les termes du contrat et de l’accord d’abonnement trouvent leur origine. |
| `endDate` | Date | Date à laquelle l’abonnement actuel se termine. Le format de date (sans heure) doit suivre le [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `paymentDueDate` | Date | Date à laquelle le paiement de l’abonnement est exigible. Le format de date (sans heure) doit suivre le [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `paymentMethod` | Chaîne | Mode de paiement des paiements récurrents. |
| `paymentStatus` | Chaîne | État du paiement du compte. |
| `planName` | Chaîne | Nom lisible par l’utilisateur de l’abonnement. |
| `reason` | Chaîne | L’intention générale du membre concernant l’utilisation de l’abonnement. |
| `renew` | Chaîne | La manière dont l’abonnement peut continuer après la date de fin. |
| `startDate` | Date | Date du début de l’abonnement. Le format de date (sans heure) doit suivre le [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `status` | Chaîne | État actuel de l’abonnement. |
| `subscriptionCategory` | Chaîne | La catégorisation principale de niveau supérieur de ce type d’abonnement. |
| `subscriptionSKU` | Chaîne | Unité de gestion des stocks (SKU) pour l’abonnement. |
| `subscriptionSubCategory` | Chaîne | Sous-catégorie spécifique de l’abonnement. |
| `term` | Nombre entier | Valeur numérique du terme d’abonnement. |
| `termUnitOfTime` | Chaîne | Unité de temps pour la période du terme. |
| `topUp` | Chaîne | Décrit les conditions convenues concernant la manière dont les aspects consommables d’un abonnement sont rachetés au cours d’une période de facturation. |
| `type` | Chaîne | La portée du droit par rapport au nombre de personnes couvertes par l’abonnement. |

{style="table-layout:auto"}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` est un tableau d’objets, chaque objet décrivant un appareil ou un accessoire associé à l’abonnement.

![Structure du tableau de périphériques](../images/data-types/telecom-subscription/devices.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `deviceFees` | Objet | Objet qui capture les frais d’appareil pour des éléments tels que les routeurs, les modems et les récepteurs. Attend les propriétés suivantes :<ul><li>`amount`: Le montant monétaire, représenté par le `currencyCode`.</li><li>`conversionDate`: Date à laquelle la conversion de devise a été effectuée.</li><li>`currencyCode`: Le [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) code de devise pour la variable `amount`.</li></ul> |
| `ID` | Chaîne | Identifiant unique de l’appareil. |
| `OS` | Chaîne | Système d’exploitation du périphérique. |
| `deviceInsurance` | Chaîne | Indique si un client a accepté de souscrire à l’assurance de cet appareil. |
| `manufacturer` | Chaîne | fabricant de l’appareil. |
| `name` | Chaîne | Nom du périphérique. |
| `paymentOptions` | Chaîne | Indique si l’appareil sera payé par versements ou au prix de détail complet. |
| `serialNumber` | Chaîne | Numéro de série de l’appareil. |
| `status` | Chaîne | État du périphérique. |
| `storageCapacity` | Chaîne | Capacité de stockage de l’appareil. |
| `type` | Chaîne | Type d’appareil. |

{style="table-layout:auto"}

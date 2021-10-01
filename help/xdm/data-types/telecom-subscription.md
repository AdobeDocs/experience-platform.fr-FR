---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;télécoms;abonnement;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'abonnement aux télécommunications
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Modèle de données d’expérience d’abonnement aux services de télécommunication).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 18%

---

# [!UICONTROL Type ] Subscriptiondata de Telecom

[!UICONTROL Telecom ] Subscriptionest un type de données XDM (Experience Data Model) standard qui décrit les détails de types d’abonnement aux télécommunications spécifiques, tels qu’Internet, mobile, média ou ligne fixe.

>[!NOTE]
>
>Ce document décrit le type de données. Pour le groupe de champs du même nom, reportez-vous au [[!UICONTROL Guide de référence du groupe ](../field-groups/profile/telecom-subscription.md)Abonnement aux télécommunications].
>
>Si vous décrivez un type d&#39;abonnement sans rapport avec l&#39;industrie des télécommunications, utilisez plutôt le type de données générique [[!UICONTROL Abonnement]](./subscription.md).

![Structure de l&#39;abonnement aux télécommunications](../images/data-types/telecom-subscription/structure.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `devices` | Tableau d’objets | Décrit une liste des appareils et/ou accessoires associés au plan. Consultez la [section ci-dessous](#devices) pour plus d’informations sur la structure attendue de chaque élément de tableau. |
| `subscriber` | [[!UICONTROL Personne]](./person.md) | Décrit le propriétaire de l’abonnement. |
| `ID` | Chaîne | Identifiant unique de l’instance d’abonnement. |
| `billingPeriod` | Chaîne | Durée entre deux facturations. |
| `billingStartDate` | Date | Date à laquelle la période de facturation commence. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `chargeMethod` | Chaîne | Configuration de la facturation au client. |
| `contractID` | Chaîne | L’identifiant unique du contrat qui régit cet abonnement. |
| `country` | Chaîne | Pays dans lequel les termes du contrat et de l’accord d’abonnement trouvent leur origine. |
| `endDate` | Date | Date à laquelle l’abonnement actuel se termine. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentDueDate` | Date | Date à laquelle le paiement de l’abonnement est exigible. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Chaîne | Mode de paiement des paiements récurrents. |
| `paymentStatus` | Chaîne | État du paiement du compte. |
| `planName` | Chaîne | Nom lisible par l’utilisateur de l’abonnement. |
| `reason` | Chaîne | L’intention générale du membre concernant l’utilisation de l’abonnement. |
| `renew` | Chaîne | La manière dont l’abonnement peut continuer après la date de fin. |
| `startDate` | Date | Date du début de l’abonnement. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Chaîne | État actuel de l’abonnement. |
| `subscriptionCategory` | Chaîne | La catégorisation principale de niveau supérieur de ce type d’abonnement. |
| `subscriptionSKU` | Chaîne | Unité de gestion des stocks (SKU) pour l’abonnement. |
| `subscriptionSubCategory` | Chaîne | Sous-catégorie spécifique de l’abonnement. |
| `term` | Entier | Valeur numérique du terme d’abonnement. |
| `termUnitOfTime` | Chaîne | Unité de temps pour la période du terme. |
| `topUp` | Chaîne | Décrit les conditions convenues concernant la manière dont les aspects consommables d’un abonnement sont rachetés au cours d’une période de facturation. |
| `type` | Chaîne | La portée du droit par rapport au nombre de personnes couvertes par l’abonnement. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` est un tableau d’objets, chaque objet décrivant un appareil ou un accessoire associé à l’abonnement.

![Structure du tableau de périphériques](../images/data-types/telecom-subscription/devices.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `deviceFees` | Objet | Objet qui capture les frais d’appareil pour des éléments tels que les routeurs, les modems et les récepteurs. Attend les propriétés suivantes :<ul><li>`amount`: Montant monétaire tel qu’il est représenté par le  `currencyCode`.</li><li>`conversionDate`: Date à laquelle la conversion de devise a été effectuée.</li><li>`currencyCode`: Code de devise  [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)  pour  `amount`.</li></ul> |
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

{style=&quot;table-layout:auto&quot;}

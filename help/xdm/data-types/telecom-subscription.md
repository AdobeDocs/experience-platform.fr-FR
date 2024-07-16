---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;télécoms;abonnement;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données d'abonnement aux télécommunications
description: Découvrez le type de données Modèle de données d’expérience d’abonnement (XDM) de Telecom.
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 20%

---

# Type de données [!UICONTROL Telecom Subscription]

[!UICONTROL Inscription aux télécommunications] est un type de données XDM (Experience Data Model) standard qui décrit les détails de types d’abonnement à des télécommunications spécifiques, tels qu’Internet, mobile, média ou ligne fixe.

>[!NOTE]
>
>Ce document décrit le type de données. Pour le groupe de champs du même nom, reportez-vous au [[!UICONTROL guide de référence du groupe d’abonnements aux télécommunications]](../field-groups/profile/telecom-subscription.md).
>
>Si vous décrivez un type d&#39;abonnement qui n&#39;a rien à voir avec l&#39;industrie des télécommunications, utilisez plutôt le type de données générique [[!UICONTROL Subscription]](./subscription.md) .

![Structure d&#39;abonnement aux télécoms](../images/data-types/telecom-subscription/structure.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `devices` | Tableau d’objets | Décrit une liste des appareils et/ou accessoires associés au plan. Pour plus d’informations sur la structure attendue de chaque élément de tableau, reportez-vous à la section [ci-dessous](#devices) . |
| `subscriber` | [[!UICONTROL Personne]](./person.md) | Décrit le propriétaire de l’abonnement. |
| `ID` | Chaîne | Identifiant unique de l’instance d’abonnement. |
| `billingPeriod` | Chaîne | Durée entre deux facturations. |
| `billingStartDate` | Date | Date à laquelle la période de facturation commence. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `chargeMethod` | Chaîne | Configuration de la facturation au client. |
| `contractID` | Chaîne | L’identifiant unique du contrat qui régit cet abonnement. |
| `country` | Chaîne | Pays dans lequel les termes du contrat et de l’accord d’abonnement trouvent leur origine. |
| `endDate` | Date | Date à laquelle le terme d’abonnement actuel se termine. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentDueDate` | Date | Date à laquelle le paiement de l’abonnement est exigible. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Chaîne | Mode de paiement des paiements récurrents. |
| `paymentStatus` | Chaîne | État du paiement du compte. |
| `planName` | Chaîne | Nom lisible par l’utilisateur de l’abonnement. |
| `reason` | Chaîne | Intention générale du membre vis-à-vis de l’utilisation de l’abonnement. |
| `renew` | Chaîne | La manière dont l’abonnement peut continuer après la date de fin. |
| `startDate` | Date | Date à laquelle l’abonnement commence. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Chaîne | Statut actuel de l’abonnement. |
| `subscriptionCategory` | Chaîne | La catégorisation principale de niveau supérieur de ce type d’abonnement. |
| `subscriptionSKU` | Chaîne | Unité de gestion des stocks (SKU) pour l’abonnement. |
| `subscriptionSubCategory` | Chaîne | Sous-catégorie spécifique de l’abonnement. |
| `term` | Nombre entier | Valeur numérique du terme d’abonnement. |
| `termUnitOfTime` | Chaîne | Unité de temps pour la période du terme. |
| `topUp` | Chaîne | Décrit les conditions convenues concernant la manière dont les aspects consommables d’un abonnement sont rachetés au cours d’une période de facturation. |
| `type` | Chaîne | La portée du droit par rapport au nombre de personnes couvertes par l’abonnement. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` est un tableau d’objets, chaque objet décrivant un appareil ou un accessoire associé à l’abonnement.

![Structure de tableau de périphériques](../images/data-types/telecom-subscription/devices.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `deviceFees` | Objet | Objet qui capture les frais d’appareil pour des éléments tels que les routeurs, les modems et les récepteurs. Attend les propriétés suivantes :<ul><li>`amount` : la valeur monétaire représentée par le `currencyCode`.</li><li>`conversionDate` : date à laquelle la conversion de devise a été effectuée.</li><li>`currencyCode` : code de devise [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) pour `amount`.</li></ul> |
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

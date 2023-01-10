---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;abonnement;type de données;type de données;type de données
solution: Experience Platform
title: Type de données d’abonnement
description: Ce document présente un aperçu du type de données XDM (Subscription Experience Data Model).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 28%

---

# [!UICONTROL Abonnement] type de données

[!UICONTROL Abonnement] est un type de données XDM (Experience Data Model) standard qui décrit les droits sous licence à des logiciels, des services ou des produits utilisés en fonction du temps ou de l’utilisation.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [[!UICONTROL Appareil]](./device.md) | Décrit les détails de l’appareil associé à l’abonnement. |
| `environment` | [[!UICONTROL Environnement]](./environment.md) | Contient des informations sur la situation autour de laquelle l’observation de l’événement s’est produite, en particulier des informations transitoires telles que les versions du réseau ou des logiciels. |
| `subscriber` | [[!UICONTROL Personne]](./person.md) | Décrit une personne. Cela peut également représenter une personne qui joue différents rôles, comme un client, un contact ou un propriétaire. |
| `SKU` | Chaîne | L’unité de gestion des stocks (SKU), un identifiant unique d’un produit. |
| `billingPeriod` | Chaîne | Durée entre deux facturations. |
| `billingStartDate` | Date | Date d’exigibilité de la première facture. Le format de date (sans heure) doit suivre le [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `category` | Chaîne | La catégorisation principale de niveau supérieur de ce type d’abonnement. |
| `chargeMethod` | Chaîne | Configuration de la facturation au client. |
| `contractID` | Chaîne | L’identifiant unique du contrat qui régit cet abonnement. |
| `country` | Chaîne | Pays dans lequel les termes du contrat et de l’accord d’abonnement trouvent leur origine. |
| `endDate` | Date | Date à laquelle l’abonnement actuel se termine. Le format de date (sans heure) doit suivre le [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `paymentMethod` | Chaîne | Mode de paiement des paiements récurrents. |
| `paymentStatus` | Chaîne | État du paiement du compte. |
| `planName` | Chaîne | Nom lisible par l’utilisateur de l’abonnement. |
| `reason` | Chaîne | L’intention générale du membre concernant l’utilisation de l’abonnement. |
| `renew` | Chaîne | La manière dont l’abonnement peut continuer après la date de fin. |
| `revision` | Chaîne | Identification entre abonnements du même nom et de la même hiérarchie de catégories. |
| `startDate` | Date | Date du début de l’abonnement. Le format de date (sans heure) doit suivre le [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standard. |
| `status` | Chaîne | État actuel de l’abonnement. |
| `subCategory` | Chaîne | Sous-catégorie spécifique de l’abonnement. |
| `term` | Nombre entier | Valeur numérique du terme d’abonnement. |
| `termUnitOfTime` | Chaîne | Unité de temps pour la période du terme. |
| `topUp` | Chaîne | Décrit les conditions convenues concernant la manière dont les aspects consommables d’un abonnement sont rachetés au cours d’une période de facturation. |
| `type` | Chaîne | La portée du droit par rapport au nombre de personnes couvertes par l’abonnement. |

{style=&quot;table-layout:auto&quot;}

Pour obtenir plus d’informations sur ce type de données, reportez-vous au référentiel XDM public:

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

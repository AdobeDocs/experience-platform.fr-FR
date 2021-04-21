---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; abonnement ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données d'Abonnement
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM (Abonnement Experience Data Model).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 27%

---

# [!UICONTROL Type ] Subscriptiondata

[!UICONTROL L’] abonnement est un type de données XDM (Experience Data Model) standard qui décrit les droits sous licence aux logiciels, services ou biens utilisés en fonction du temps ou de l’utilisation.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `device` | [[!UICONTROL Appareil]](./device.md) | Décrit les détails sur le périphérique lié à l’abonnement. |
| `environment` | [[!UICONTROL Environnement]](./environment.md) | Contient des informations sur la situation environnante dans laquelle l&#39;observation du événement s&#39;est produite, en particulier des informations transitoires telles que les versions du réseau ou des logiciels. |
| `subscriber` | [[!UICONTROL Personne]](./person.md) | Décrit une personne individuelle. Il peut également représenter une personne jouant divers rôles, par exemple un client, un contact ou un propriétaire. |
| `SKU` | Chaîne | Unité de gestion des stocks (SKU), identifiant unique d’un produit. |
| `billingPeriod` | Chaîne | Durée entre deux facturations. |
| `billingStartDate` | Date | Date d’exigibilité de la première facture. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `category` | Chaîne | La catégorisation principale, de niveau supérieur, de ce type d&#39;abonnement. |
| `chargeMethod` | Chaîne | Configuration de la facturation au client. |
| `contractID` | Chaîne | ID unique du contrat qui régit cet abonnement. |
| `country` | Chaîne | Le pays dans lequel les clauses contractuelles et contractuelles de l&#39;abonnement trouvent leur origine. |
| `endDate` | Date | Date à laquelle l’abonnement actuel se termine. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `paymentMethod` | Chaîne | Mode de paiement des paiements récurrents. |
| `paymentStatus` | Chaîne | Statut de paiement du compte. |
| `planName` | Chaîne | Nom lisible par l&#39;homme de l&#39;abonnement. |
| `reason` | Chaîne | L&#39;intention générale du membre pour l&#39;utilisation de l&#39;abonnement. |
| `renew` | Chaîne | La manière dont l’abonnement peut continuer après la date de fin. |
| `revision` | Chaîne | Identification entre abonnements du même nom et de la même hiérarchie de catégories. |
| `startDate` | Date | Date du début de l’abonnement. Le format de date (sans heure) doit respecter la norme [RFC 3339, section 5.6](https://tools.ietf.org/html/rfc3339#section-5.6). |
| `status` | Chaîne | Statut actuel de l&#39;abonnement. |
| `subCategory` | Chaîne | Sous-catégorisation spécifique de l&#39;abonnement. |
| `term` | Entier | Valeur numérique du terme de l’abonnement. |
| `termUnitOfTime` | Chaîne | Unité de temps pour la période du terme. |
| `topUp` | Chaîne | Décrit les termes convenus sur la façon dont les aspects consommables d&#39;un abonnement sont rachetés au cours d&#39;une période de facturation. |
| `type` | Chaîne | L&#39;étendue des droits par rapport au nombre de personnes couvertes par l&#39;abonnement. |

Pour plus d&#39;informations sur le type de données, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

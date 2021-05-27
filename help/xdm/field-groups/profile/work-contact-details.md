---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schémas;conception de schéma;mixin;mixins;détails de travail;travail de profil;
solution: Experience Platform
title: Groupe de champs de schéma Détails du contact professionnel
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs de schéma Détails du contact du travail .
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 6%

---


# [!UICONTROL Groupe de champs Détails du ] schéma Contact professionnel

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Contact professionnel ] Détails d’un groupe de champs de schéma standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit plusieurs champs qui capturent des informations professionnelles concernant une personne, telles que son adresse professionnelle, son e-mail de travail, son numéro de téléphone de travail et les organisations auxquelles elle appartient.

![](../../images/field-groups/work-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `workAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l’adresse professionnelle de la personne. |
| `workEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique professionnelle de la personne. |
| `workPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone professionnel de la personne. |
| `organizations` | Chaîne (tableau) | Tableau de chaînes de forme libre représentant les organisations dont la personne est membre. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)

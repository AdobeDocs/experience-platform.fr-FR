---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;XDM;profil individuel;champs;schémas;schémas;conception de schéma;mixin;mixins;détails de travail;travail de profil;
solution: Experience Platform
title: Groupe de champs de schéma Détails du contact professionnel
description: Découvrez le groupe de champs Détails du contact du travail .
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 14%

---


# [!UICONTROL Détails du contact du travail] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Work Contact Details] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit plusieurs champs qui capturent des informations professionnelles concernant une personne, telles que son adresse professionnelle, son e-mail de travail, son numéro de téléphone de travail et les organisations auxquelles elle appartient.

![](../../images/field-groups/work-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `workAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l’adresse professionnelle de la personne. |
| `workEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique professionnelle de la personne. |
| `workPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone professionnel de la personne. |
| `organizations` | Chaîne (tableau) | Tableau de chaînes de forme libre représentant les organisations dont la personne est membre. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)

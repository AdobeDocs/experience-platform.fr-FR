---
keywords: Experience Platform;accueil;rubriques populaires;schéma;Schéma;XDM;profil individuel;champs;schémas;Schémas;Conception de schéma;mixin;mixins;détails de travail;travail sur le profil;
solution: Experience Platform
title: Groupe De Champs De Schéma Des Détails Du Contact Professionnel
description: Découvrez le groupe de champs de schéma Détails du contact professionnel .
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
TQID: https://experienceleague.adobe.com/jiX9U9BNZ5HGzcVFyCrc9IV5Vq9QDBvRQAW-zIl8Pz8
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2:
  - id: c132d929-fa62-4271-803e-b823be07b914
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 192
ht-degree: 12%

---

# [!UICONTROL Détails du contact professionnel] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Détails du contact professionnel] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit plusieurs champs qui capturent des informations professionnelles concernant une personne individuelle, telles que l’adresse professionnelle, l’adresse e-mail professionnelle, le numéro de téléphone professionnel et les organisations auxquelles la personne appartient.

![](../../images/field-groups/work-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `workAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l&#39;adresse professionnelle de la personne. |
| `workEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse e-mail professionnelle de la personne. |
| `workPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone professionnel de la personne. |
| `organizations` | Chaîne (tableau) | Tableau de chaînes de forme libre représentant les organisations dont la personne est membre. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)

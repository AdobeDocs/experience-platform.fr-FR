---
keywords: Experience Platform ; accueil ; thèmes populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; conception de Schéma ; mixin ; détails du travail ; travail profil ;
solution: Experience Platform
title: Groupe de champs Détails du contact de travail
topic-legacy: overview
description: Ce document fournit une vue d'ensemble du groupe de champs Détails du contact professionnel.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 5%

---


# [!UICONTROL Groupe de champs ] Détails du contact professionnel

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mise à jour du nom du groupe de champs](../name-updates.md).

[!UICONTROL Les ] détails des contacts professionnels constituent un groupe de champs de schéma standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le groupe de champs fournit plusieurs champs qui capturent des informations professionnelles relatives à une personne, telles que son adresse de travail, son courriel de travail, son numéro de téléphone de travail et les organisations auxquelles elle appartient.

![](../../images/field-groups/work-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `workAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l&#39;adresse professionnelle de la personne. |
| `workEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique professionnelle de la personne. |
| `workPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone professionnel de la personne. |
| `organizations` | Chaîne (tableau) | Tableau de chaînes de forme libre représentant les organisations dont la personne est membre. |

Pour plus d&#39;informations sur le groupe de champs, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)

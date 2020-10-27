---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Mélangeur Détails du contact professionnel
topic: overview
description: Ce document fournit une vue d’ensemble du mixin Coordonnées de travail.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 6%

---


# [!UICONTROL Mélange des détails] du contact professionnel

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document sur les mises à jour [des noms de](../name-updates.md) mixin.

[!UICONTROL Les détails] des contacts professionnels sont un mixin standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le mixin fournit plusieurs champs qui capturent des informations professionnelles concernant une personne, telles que son adresse de travail, son courriel de travail, son numéro de téléphone de travail et les organisations auxquelles elle appartient.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `workAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l&#39;adresse professionnelle de la personne. |
| `workEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique professionnelle de la personne. |
| `workPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone professionnel de la personne. |
| `organizations` | Chaîne (tableau) | Tableau de chaînes de forme libre représentant les organisations dont la personne est membre. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
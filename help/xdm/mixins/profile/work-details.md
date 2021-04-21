---
keywords: Experience Platform ; accueil ; thèmes populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; conception de Schéma ; mixin ; détails du travail ; travail profil ;
solution: Experience Platform
title: Mixage des détails des contacts professionnels
topic-legacy: overview
description: Ce document fournit une vue d’ensemble du mixin Coordonnées de travail.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 5%

---

# [!UICONTROL Mélangine ] des détails du contact professionnel

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document [Mises à jour du nom de mixin](../name-updates.md).

[!UICONTROL Coordonnées de travail ] Détaillez un mixin standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le mixin fournit plusieurs champs qui capturent des informations professionnelles concernant une personne, telles que son adresse de travail, son courriel de travail, son numéro de téléphone de travail et les organisations auxquelles elle appartient.

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

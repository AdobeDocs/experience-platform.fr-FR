---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: Mélange des informations personnelles du profil
topic: overview
description: Ce document fournit un aperçu de la classe de Profil XDM Individuel.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 11%

---


# [!UICONTROL Mélange des informations] personnelles du profil

[!UICONTROL Les informations] personnelles du profil sont un mélange standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le mixin fournit un objet de niveau racine `person` , dont les sous-champs décrivent les coordonnées d’une personne.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Propriété | Type de données | Description |
| --- | --- | --- |
| `faxPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de télécopie de la personne. |
| `homeAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l&#39;adresse résidentielle de la personne. |
| `homePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone de la personne. |
| `mobilePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone portable de la personne. |
| `personalEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique de la personne. |

Pour plus d’informations sur le mixin, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)

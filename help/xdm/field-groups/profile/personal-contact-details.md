---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; détails personnels ; conception de Schéma ; groupe de champs ; groupe de champs ;
solution: Experience Platform
title: Groupe de champs Détails du contact personnel
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs de schéma Coordonnées personnelles.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 8%

---


# [!UICONTROL Groupe de champs ] Détails du contact personnel

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mise à jour du nom du groupe de champs](../name-updates.md).

[!UICONTROL Coordonnées personnelles ] Détail d&#39;un schéma est un groupe de champs standard pour la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe qui décrit les coordonnées d&#39;une personne.

![](../../images/field-groups/personal-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `faxPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de télécopie de la personne. |
| `homeAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l&#39;adresse résidentielle de la personne. |
| `homePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone de la personne. |
| `mobilePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone portable de la personne. |
| `personalEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique de la personne. |

Pour plus d&#39;informations sur le groupe de champs, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)

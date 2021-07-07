---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;profil individuel;champs;schémas;schémas;détails personnels;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma Détails du contact personnel
topic-legacy: overview
description: Ce document présente un aperçu du groupe de champs de schéma Détails du contact personnel .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 10%

---


# [!UICONTROL Groupe de champs ] Détails du contact personnel

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document [mises à jour des noms de groupe de champs](../name-updates.md) .

[!UICONTROL Contact personnel ] Détails d’un schéma standard pour la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe qui décrit les coordonnées d’une personne.

![](../../images/field-groups/personal-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `faxPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de fax de la personne. |
| `homeAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l’adresse résidentielle de la personne. |
| `homePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone de la personne. |
| `mobilePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone portable de la personne. |
| `personalEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique de la personne. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

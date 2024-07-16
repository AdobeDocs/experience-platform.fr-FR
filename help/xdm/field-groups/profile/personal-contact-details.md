---
keywords: Experience Platform;accueil;rubriques populaires;schéma;schéma;XDM;profil individuel;champs;schémas;schémas;détails personnels;conception de schéma;groupe de champs;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma Détails du contact personnel
description: Découvrez le groupe de champs Détails du contact personnel .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 16%

---


# [!UICONTROL Détails du contact personnel] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Personal Contact Details] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) qui décrit les informations de contact pour une personne individuelle.

![](../../images/field-groups/personal-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `faxPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de fax de la personne. |
| `homeAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l’adresse de la personne. |
| `homePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone de la personne. |
| `mobilePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone portable de la personne. |
| `personalEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse électronique de la personne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

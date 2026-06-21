---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;Schéma;XDM;profil individuel;champs;schémas;Schémas;détails personnels;conception de schéma;groupe de champs;groupe de champs;
solution: Experience Platform
title: Groupe de champs de schéma des détails de contact personnels
description: Découvrez le groupe de champs de schéma Coordonnées personnelles .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
TQID: https://experienceleague.adobe.com/gU25SitmtH-ON-x0PqZqk1aPIAoVcz8d-G3FT8VxYFg
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 167
ht-degree: 14%

---

# [!UICONTROL Coordonnées personnelles] groupe de champs de schéma

>[!NOTE]
>
>Les noms de plusieurs groupes de champs de schéma ont changé. Pour plus d’informations, consultez le document sur les [mises à jour des noms de groupes de champs](../name-updates.md).

[!UICONTROL Coordonnées personnelles] est un groupe de champs de schéma standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md) qui décrit les informations de contact d’une personne individuelle.

![](../../images/field-groups/personal-contact-details.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `faxPhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de télécopie de la personne. |
| `homeAddress` | [Adresse postale](../../data-types/postal-address.md) | Décrit l’adresse résidentielle de la personne. |
| `homePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone personnel de la personne. |
| `mobilePhone` | [Numéro de téléphone](../../data-types/phone-number.md) | Décrit le numéro de téléphone mobile de la personne. |
| `personalEmail` | [Adresse électronique](../../data-types/email-address.md) | Décrit l’adresse e-mail de la personne. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; détails personnels ; conception de Schéma ; mixin ; Mixin ;
solution: Experience Platform
title: Mixage des coordonnées personnelles
topic-legacy: overview
description: Ce document présente un aperçu du mixin Coordonnées personnelles.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 9%

---

# [!UICONTROL Coordonnées personnelles ] Détailsmixin

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document [Mises à jour du nom de mixin](../name-updates.md).

[!UICONTROL Coordonnées personnelles ] Détail d&#39;un mélange standard pour la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe qui décrit les coordonnées d&#39;une personne.

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

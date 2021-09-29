---
title: Groupe de champs de schéma des composants de personne professionnelle XDM
description: Ce document fournit un aperçu du groupe de champs de schéma XDM Business Person Components.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 5%

---

# [!UICONTROL Groupe de champs ] de schéma de composants de personne professionnelle XDM (bêta)

>[!IMPORTANT]
>
>Ce groupe de champs est disponible dans le cadre de la plateforme de données clients en temps réel de l’édition B2B, actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

[!UICONTROL Les ] composants XDM Business Person constituent un groupe de champs de schéma standard pour la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) classe qui capture plusieurs enregistrements source pour une personne, ainsi que d’autres attributs requis pour la segmentation des personnes.

Lorsqu’un profil est créé pour une personne via [Real-time Customer Profile](../../../profile/home.md) dans l’édition B2B de la plateforme de données clients en temps réel, les informations utilisées pour créer ce profil peuvent potentiellement provenir de nombreux enregistrements source. Par exemple, si une personne travaille pour deux sociétés différentes, de nombreux systèmes de gestion de la relation client créent intentionnellement une copie en double de cette personne afin qu’une copie soit liée à la Société A, tandis que l’autre est liée à la Société B. Lorsque vous incorporez ces données dans Adobe Experience Platform, ce groupe de champs est utilisé pour fusionner ces différents enregistrements source en une seule représentation.

Le groupe de champs fournit un champ `personComponents` de niveau racine, qui est un tableau d’objets. Chaque objet du tableau représente un enregistrement source différent.

![](../../images/field-groups/business-person-components.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du compte associé à la personne. |
| `sourceConvertedContactKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du contact associé si ce prospect a été converti. |
| `sourceExternalKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite du système source d’où proviennent les données de la personne. |
| `sourcePersonKey` | [[!UICONTROL Source B2B]](../../data-types/b2b-source.md) | Identifiant composite de la personne. |
| `workEmail` | [[!UICONTROL Adresse électronique]](../../data-types/b2b-source.md) | ID de l’adresse électronique professionnelle de la personne. |
| `personGroupID` | Chaîne | Identifiant de groupe de la personne. |
| `personScore` | Chaîne | Score généré pour la personne par un système CRM. |
| `personSource` | Chaîne | Identifiant unique basé sur des chaînes pour le système source d’où proviennent les données de la personne. |
| `personStatus` | Chaîne | État actuel du marketing ou des ventes de la personne. |
| `personType` | Chaîne | Type de personne dans un contexte B2B. |
| `sourceAccountID` | Chaîne | Identifiant unique basé sur des chaînes pour le compte dans le système source associé à la personne. Ce champ est utilisé comme clé étrangère par le système pour rechercher les différentes entreprises pour lesquelles cette personne travaille. |
| `sourceConvertedContactID` | Chaîne | Identifiant unique basé sur des chaînes pour le contact associé si cette piste a été convertie. |
| `sourceExternalID` | Chaîne | Identifiant unique basé sur des chaînes pour le système source d’où proviennent les données de la personne. |
| `sourcePersonID` | Chaîne | Identifiant unique basé sur des chaînes pour la personne. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le groupe de champs, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)

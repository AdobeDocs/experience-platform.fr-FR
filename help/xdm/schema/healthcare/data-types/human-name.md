---
title: Type de données de nom humain
description: Découvrez le type de données Modèle de données d’expérience (XDM) de nom humain.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
TQID: https://experienceleague.adobe.com/MbkrIZ-lNUCvhqUg44kttkEykroqKJXcAEJMICo1oFE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 207
ht-degree: 5%

---

# [!UICONTROL Nom humain] type de données

[!UICONTROL Nom humain] est un type de données standard du modèle de données d’expérience (XDM) qui fournit des informations sur le nom d’un être humain ou d’une autre entité vivante. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données du nom humain](../../../images/healthcare/data-types/human-name.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | Période au cours de laquelle le nom est ou était utilisé. |
| [!UICONTROL  Famille ] | `family` | Chaîne | Le nom de famille ou de famille. |
| [!UICONTROL Donné] | `given` | Tableau de chaînes | Le prénom, y compris le ou les deuxième prénom(s). |
| [!UICONTROL Préfixe] | `prefix` | Tableau de chaînes | Toute partie du nom précédant le prénom ou le prénom. |
| [!UICONTROL Suffixe] | `suffix` | Tableau de chaînes | Toute partie du nom postérieure au nom de famille ou de famille. |
| [!UICONTROL Texte] | `text` | Chaîne | Représentation en texte brut du nom complet. |
| [!UICONTROL Utiliser] | `use` | Chaîne | Utilisation du nom. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)

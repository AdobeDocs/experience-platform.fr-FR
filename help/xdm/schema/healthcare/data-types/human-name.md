---
title: Type de données de nom humain
description: Découvrez le type de données XDM (Human Name Experience Data Model).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 5dd6fda4-c076-4c34-bdd9-259203b6ea73
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# Type de données [!UICONTROL Human Name]

[!UICONTROL Human Name] est un type de données XDM (Experience Data Model) standard qui fournit des informations sur le nom d’une entité humaine ou d’une autre entité vivante. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données Nom de l’homme](../../../images/healthcare/data-types/human-name.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Période] | `period` | [[!UICONTROL Période]](../data-types/period.md) | Période pendant laquelle le nom est ou a été utilisé. |
| [!UICONTROL Famille] | `family` | Chaîne | La famille ou le nom. |
| [!UICONTROL Donné] | `given` | Tableau de chaînes | Le prénom, y compris le(s) nom(s) intermédiaire(s). |
| [!UICONTROL Préfixe] | `prefix` | Tableau de chaînes | Toutes les parties du nom situées avant le prénom ou le prénom. |
| [!UICONTROL Suffix] | `suffix` | Tableau de chaînes | Toutes les parties du nom suivant la famille ou le nom de famille. |
| [!UICONTROL Texte] | `text` | Chaîne | Représentation en texte brut du nom complet. |
| [!UICONTROL Utiliser] | `use` | Chaîne | L’utilisation du nom. Les valeurs de cette propriété doivent être égales à une ou plusieurs des valeurs d’énumération connues suivantes. <li> `usual` </li> <li> `offical` </li> <li> `temp` </li> <li> `nickname` </li> <li> `anonymous` </li> <li> `old` </li> <li> `maiden` </li> |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/humanname.schema.json)

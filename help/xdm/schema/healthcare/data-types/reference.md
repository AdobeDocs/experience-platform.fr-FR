---
title: Type de données de référence
description: Découvrez le type de données Modèle de données d’expérience de référence (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: eb724dbb-2918-43b5-8e50-c8aabfe6e96c
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 12%

---

# Type de données [!UICONTROL Reference]

[!UICONTROL Reference] est un type de données XDM (Experience Data Model) standard qui fournit une référence d’une ressource à une autre. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de référence](../../../images/healthcare/data-types/reference.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Identifiant] | `identifier` | [[!UICONTROL Identifiant]](../data-types/identifier.md) | Référence logique lorsque la référence littérale n’est pas connue. |
| [!UICONTROL Affichage] | `display` | Chaîne | Texte secondaire de la référence. |
| [!UICONTROL Référence] | `reference` | Chaîne | Référence littérale, URL relative, interne ou absolue. |
| [!UICONTROL Type] | `type` | Chaîne | Type auquel la référence fait référence, représenté sous la forme d’un URI. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/reference.schema.json)

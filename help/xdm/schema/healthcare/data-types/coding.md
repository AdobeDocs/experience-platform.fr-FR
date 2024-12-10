---
title: Type de données de codage
description: Découvrez le type de données Coding Experience Data Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 11%

---

# Type de données [!UICONTROL Coding]

[!UICONTROL Coding] est un type de données XDM (Experience Data Model) standard qui décrit une référence à un code défini par un système terminologique. Ce type de données est créé conformément aux spécifications de la version 5 de HL7 FHIR.

![Structure de type de données de codage](../../../images/healthcare/data-types/coding.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Symbole de la syntaxe définie par le système. |
| [!UICONTROL Affichage] | `display` | Chaîne | Représentation définie par le système. |
| [!UICONTROL Système] | `system` | Chaîne | L’espace de noms de la valeur de l’identifiant, spécifié en tant qu’URI. |
| [!UICONTROL Est Sélectionné Par L’Utilisateur] | `userSelected` | Booléen | Indicateur précisant si ce codage a été choisi par l’utilisateur. La valeur par défaut est false. |
| [!UICONTROL Version] | `version` | Chaîne | Version du système. |

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)

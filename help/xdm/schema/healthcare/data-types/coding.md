---
title: Type de données de codage
description: Découvrez le type de données du modèle de données d’expérience de codage (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
source-git-commit: 0e902b50cce148e0fbbb8e33c227165942b08832
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 11%

---

# Type de données [!UICONTROL Coding]

[!UICONTROL Coding] est un type de données standard du modèle de données d’expérience (XDM) qui décrit une référence à un code défini par un système terminologique. Ce type de données est créé conformément aux spécifications HL7 FHIR Release 5.

![Structure du type de données de codage](../../../images/healthcare/data-types/coding.png)

| Nom d’affichage | Propriété | Type de données | Description |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | Chaîne | Symbole dans la syntaxe définie par le système. |
| [!UICONTROL Display] | `display` | Chaîne | Représentation définie par le système. |
| [!UICONTROL System] | `system` | Chaîne | Espace de noms de la valeur d’identifiant, représentée sous la forme d’un URI. |
| [!UICONTROL Is Selected By User] | `userSelected` | Booléen | Indicateur indiquant si ce codage a été choisi par l’utilisateur. La valeur par défaut est false. |
| [!UICONTROL Version] | `version` | Chaîne | Version du système. |

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/coding.schema.json)

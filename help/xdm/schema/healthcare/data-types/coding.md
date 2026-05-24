---
title: Type de données de codage
description: Découvrez le type de données du modèle de données d’expérience de codage (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
exl-id: 23b789da-1feb-4001-8268-f0d7e2e8563b
TQID: https://experienceleague.adobe.com/83-qVEyxPmFNDDKDuKh89-0djh49tuUmZEN5zsds0lE
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 155
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

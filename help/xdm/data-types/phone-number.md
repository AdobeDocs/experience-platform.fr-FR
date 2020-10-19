---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: Type de données de numéro de téléphone
topic: overview
description: Ce document présente un aperçu du type de données XDM du numéro de téléphone.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 10%

---


# [!UICONTROL Type de données de numéro] de téléphone

[!UICONTROL Le numéro] de téléphone est un type de données XDM standard qui décrit les détails d&#39;un numéro de téléphone.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propriété | Description |
| --- | --- |
| `extension` | Numéro de numérotation interne utilisé pour appeler à partir d&#39;un central de change privé, d&#39;un opérateur ou d&#39;un standard. |
| `number` | Numéro de téléphone. Note the phone number is a string and may include meaningful characters such as brackets `()`, hyphens `-`, or characters to indicate sub-dialing identifiers like extensions `x` for example, `1-353(0)18391111` or `+613 9403600x1234`. |
| `primary` | Valeur booléenne qui indique s’il s’agit du numéro de téléphone Principal de l’individu. Contrairement à l&#39;adresse ou à l&#39;adresse électronique, il peut y avoir plusieurs numéros de téléphone Principaux ; un par canal de communication. Le canal de communication est défini par le type (indiqué par le nom de la propriété parent) : `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`et `fax`. |
| `status` | Indique si le numéro de téléphone peut actuellement être utilisé. |
| `statusReason` | Description de l’état actuel. |
| `validity` | Niveau de précision technique du numéro de téléphone. |

Pour plus d&#39;informations sur le type de données des numéros de téléphone, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)
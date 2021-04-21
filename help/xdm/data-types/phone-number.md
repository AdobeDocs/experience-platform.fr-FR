---
keywords: Experience Platform ; accueil ; rubriques populaires ; schéma ; Schéma ; XDM ; champs ; schémas ; Schémas ; numéro de téléphone ; xdm:numéro de téléphone ; type de données ; type de données ; type de données ;
solution: Experience Platform
title: Type de données de numéro de téléphone
topic-legacy: overview
description: Ce document présente un aperçu du type de données XDM du numéro de téléphone.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 9%

---

# [!UICONTROL Type de ] données de numéro de téléphone

[!UICONTROL Le ] numéro de téléphone est un type de données XDM standard qui décrit les détails d&#39;un numéro de téléphone.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propriété | Description |
| --- | --- |
| `extension` | Numéro de numérotation interne utilisé pour appeler à partir d&#39;un central de change privé, d&#39;un opérateur ou d&#39;un standard. |
| `number` | Numéro de téléphone. Notez que le numéro de téléphone est une chaîne et peut inclure des caractères significatifs tels que des crochets `()`, des tirets `-` ou des caractères pour indiquer des identifiants de sous-numérotation tels que des extensions `x`, par exemple `1-353(0)18391111` ou `+613 9403600x1234`. |
| `primary` | Valeur booléenne qui indique s’il s’agit du numéro de téléphone Principal de l’individu. Contrairement à l&#39;adresse ou à l&#39;adresse électronique, il peut y avoir plusieurs numéros de téléphone Principaux ; un par canal de communication. Le canal de communication est défini par le type (indiqué par le nom de la propriété parent) : `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` et `fax`. |
| `status` | Indique si le numéro de téléphone peut actuellement être utilisé. |
| `statusReason` | Description de l’état actuel. |
| `validity` | Niveau de précision technique du numéro de téléphone. |

Pour plus d&#39;informations sur le type de données des numéros de téléphone, consultez le référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)

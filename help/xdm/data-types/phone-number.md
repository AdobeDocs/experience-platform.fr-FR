---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;schéma;XDM;champs;schémas;schémas;numéroTéléphone;xdm:numéroDeTéléphone;type de données;type de données;type de données;
solution: Experience Platform
title: Type de données de numéro de téléphone
description: Découvrez le type de données XDM Phone Number.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 18%

---

# Type de données [!UICONTROL Numéro de téléphone]

[!UICONTROL Numéro de téléphone] est un type de données XDM standard qui décrit les détails d’un numéro de téléphone.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propriété | Description |
| --- | --- |
| `extension` | Numéro d’appel interne utilisé pour appeler à partir d’un central privé, d’un opérateur ou d’un standard. |
| `number` | Numéro de téléphone. Notez que le numéro de téléphone est une chaîne qui peut contenir des caractères significatifs tels que des crochets `()`, des tirets `-` ou des caractères pour indiquer des identifiants de sous-numérotation comme des extensions `x`, par exemple `1-353(0)18391111` ou `+613 9403600x1234`. |
| `primary` | Une valeur booléenne qui indique s’il s’agit du numéro de téléphone principal de l’individu. Contrairement à l’adresse ou à l’adresse électronique, il peut y avoir plusieurs numéros de téléphone primaires, un par canal de communication. Le canal de communication est défini par le type (indiqué par le nom de la propriété parent) : `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` et `fax`. |
| `status` | Indique si le numéro de téléphone peut être utilisé. |
| `statusReason` | Description de l’état actuel. |
| `validity` | Niveau de précision technique du numéro de téléphone. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données du numéro de téléphone, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)

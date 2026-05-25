---
keywords: Experience Platform;accueil;rubriques les plus consultées;schéma;Schéma;XDM;champs;schémas;Schémas;numéro de téléphone;xdm:numéroDeTéléphone;typeDonnées;type de données;
solution: Experience Platform
title: Type de données de numéro de téléphone
description: Découvrez le type de données XDM Numéro de téléphone.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
TQID: https://experienceleague.adobe.com/6HBKe4hxVBLAELodREhTOKUE0zTf0BIlwL7Va9x7WCg
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 204
ht-degree: 9%

---

# Type de données [!UICONTROL Phone number]

[!UICONTROL Phone number] est un type de données XDM standard qui décrit les détails d’un numéro de téléphone.

![](../images/data-types/phone-number.png){width=600}

| Propriété | Description |
| --- | --- |
| `extension` | Numéro d’appel interne utilisé pour appeler à partir d’un central privé, d’un opérateur ou d’un standard. |
| `number` | Numéro de téléphone. Notez que le numéro de téléphone est une chaîne et peut inclure des caractères significatifs tels que des crochets `()`, des tirets `-` ou des caractères pour indiquer des identifiants de sous-numérotation tels que des extensions `x` par exemple `1-353(0)18391111` ou `+613 9403600x1234`. |
| `primary` | Valeur booléenne qui indique s’il s’agit du numéro de téléphone principal de l’individu. Contrairement à l’adresse ou à l’adresse e-mail, il peut y avoir plusieurs numéros de téléphone principaux ; un par canal de communication. Le canal de communication est défini par le type (indiqué par le nom de la propriété parent) : `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` et `fax`. |
| `status` | Indique si le numéro de téléphone peut actuellement être utilisé. |
| `statusReason` | Description de l’état actuel. |
| `validity` | Niveau de précision technique du numéro de téléphone. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données de numéro de téléphone, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)

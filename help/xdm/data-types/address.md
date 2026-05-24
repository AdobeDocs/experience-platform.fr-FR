---
title: Type De Données D’Adresse Postale
description: Découvrez le type de données Modèle de données d’expérience d’adresse postale (XDM).
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
TQID: https://experienceleague.adobe.com/qLVVFaB0ZzZVwq0tNWYKkCOZRFLwGpaAKMcQNgLEX4c
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 37%

---

# Type de données [!UICONTROL Postal Address]

[!UICONTROL Postal Address] est un type de données standard du modèle de données d’expérience (XDM) qui fournit des détails d’adresse.

![Diagramme du type de données [!UICONTROL Postal Address].](../images/data-types/postal-address.png)

| Nom d’affichage | Propriété | Type de données | Description |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Primary] | `primary` | booléen | Indicateur d’adresse du Principal. Un profil ne peut avoir qu’une seule adresse `primary` à un moment donné. |
| [!UICONTROL Label] | `label` | chaîne | Nom de l’adresse de forme libre. |
| [!UICONTROL Street 1] | `street1` | chaîne | Informations au niveau de la rue du Principal, numéro de l’appartement, numéro de la rue et nom de la rue. |
| [!UICONTROL Street 2] | `street2` | chaîne | Informations facultatives sur la rue, deuxième ligne. |
| [!UICONTROL Street 3] | `street3` | chaîne | Informations facultatives sur la rue, troisième ligne. |
| [!UICONTROL Street 4] | `street4` | chaîne | Informations facultatives sur la rue, quatrième ligne. |
| [!UICONTROL Region] | `region` | chaîne | Partie de l’adresse qui indique la région, le département ou le district. |
| [!UICONTROL Post office box] | `postOfficeBox` | chaîne | Boîte postale de l’adresse. |
| [!UICONTROL Country] | `country` | chaîne | Nom du territoire administré par un gouvernement. Champ de forme libre que peut avoir le nom du pays dans n’importe quelle langue, autre que ``countryCode``. |
| [!UICONTROL State] | `state` | chaîne | Nom de l’État. Il s’agit d’un champ à structure libre. |
| [!UICONTROL Status] | `status` | chaîne | Indication quant à la possibilité d’utiliser l’adresse. |
| [!UICONTROL Status reason] | `statusReason` | chaîne | Description de l’état actuel. |
| [!UICONTROL Last verified date] | `lastVerifiedDate` | chaîne | Date à laquelle l’adresse a été vérifiée pour la dernière fois comme étant toujours associée à la personne. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) sur le référentiel XDM public :

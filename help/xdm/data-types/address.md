---
title: Type de données d’adresse postale
description: Découvrez le type de données XDM (Postal Address Experience Data Model).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 36%

---

# [!UICONTROL Adresse postale] type de données

[!UICONTROL Adresse postale] est un type de données XDM (Experience Data Model) standard qui fournit des détails d’adresse.

![Un diagramme de [!UICONTROL Adresse postale] type de données.](../images/data-types/postal-address.png)

| Nom d’affichage | Propriété | Type de données | Description |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Instance principale] | `primary` | booléen | Indicateur d’adresse de Principal. Un profil ne peut avoir qu’un seul `primary` adresse à un moment donné. |
| [!UICONTROL Libellé] | `label` | chaîne | Nom du formulaire libre de l&#39;adresse. |
| [!UICONTROL Rue 1] | `street1` | chaîne | Informations au niveau de la rue par Principal, numéro d’appartement, numéro de rue et nom de rue. |
| [!UICONTROL Rue 2] | `street2` | chaîne | Informations facultatives sur la rue, deuxième ligne. |
| [!UICONTROL Rue 3] | `street3` | chaîne | Informations facultatives sur la rue, troisième ligne. |
| [!UICONTROL Rue 4] | `street4` | chaîne | Informations facultatives sur la rue, quatrième ligne. |
| [!UICONTROL Zone géographique] | `region` | chaîne | Partie de l’adresse qui indique la région, le département ou le district. |
| [!UICONTROL Boîte postale] | `postOfficeBox` | chaîne | Boîte postale de l’adresse. |
| [!UICONTROL Pays] | `country` | chaîne | Nom du territoire administré par un gouvernement. Champ de forme libre que peut avoir le nom du pays dans n’importe quelle langue, autre que ``countryCode``. |
| [!UICONTROL État] | `state` | chaîne | Nom de l’État. C&#39;est un champ de forme libre. |
| [!UICONTROL Statut] | `status` | chaîne | Une indication quant à la possibilité d’utiliser l’adresse. |
| [!UICONTROL Raison de l’état] | `statusReason` | chaîne | Description de l’état actuel. |
| [!UICONTROL Date de dernière vérification] | `lastVerifiedDate` | chaîne | Date à laquelle l’adresse a été vérifiée pour la dernière fois comme toujours associée à la personne. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) sur le référentiel XDM public :

---
title: Type de données d’adresse postale
description: Découvrez le type de données XDM (Postal Address Experience Data Model).
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 51%

---

# Type de données [!UICONTROL Postal Address]

[!UICONTROL Postal Address] (Adresse postale) est un type de données XDM (modèle de données d’expérience) standard qui fournit des détails d’adresse.

![Schéma du type de données [!UICONTROL Postal Address].](../images/data-types/postal-address.png)

| Nom d’affichage | Propriété | Type de données | Description |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Principal] | `primary` | Booléen | Indicateur d’adresse de Principal. Un profil ne peut avoir qu’une seule adresse `primary` à un moment donné. |
| [!UICONTROL Libellé] | `label` | Chaîne | Nom de l’adresse de forme libre. |
| [!UICONTROL Rue 1] | `street1` | Chaîne | Informations principales au niveau de la rue, numéro d’appartement, numéro de rue et nom de la rue. |
| [!UICONTROL Rue 2] | `street2` | Chaîne | Informations facultatives sur la rue, deuxième ligne. |
| [!UICONTROL Rue 3] | `street3` | Chaîne | Informations facultatives sur la rue, troisième ligne. |
| [!UICONTROL Rue 4] | `street4` | Chaîne | Informations facultatives sur la rue, quatrième ligne. |
| [!UICONTROL Région] | `region` | Chaîne | Partie de l’adresse qui indique la région, le département ou le district. |
| [!UICONTROL Boîte de bureau Post] | `postOfficeBox` | Chaîne | Boîte postale de l’adresse. |
| [!UICONTROL Country] | `country` | Chaîne | Nom du territoire administré par un gouvernement. Champ de forme libre que peut avoir le nom du pays dans n’importe quelle langue, autre que ``countryCode``. |
| [!UICONTROL État] | `state` | Chaîne | Le nom de l’état. Il s’agit d’un champ à forme libre. |
| [!UICONTROL Statut] | `status` | Chaîne | Indication quant à la possibilité d’utiliser l’adresse. |
| [!UICONTROL Raison de l’état] | `statusReason` | Chaîne | Description de l’état actuel. |
| [!UICONTROL Date de dernière vérification] | `lastVerifiedDate` | Chaîne | Date à laquelle l’adresse a été vérifiée pour la dernière fois comme toujours associée à la personne. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au [schéma complet](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) sur le référentiel XDM public :

---
title: Type de données de retour
description: Découvrez le type de données Modèle de données d’expérience de retour (XDM).
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 8%

---

# [!UICONTROL Retour] type de données

[!UICONTROL Retour] est un type de données XDM (Experience Data Model) standard qui capture les informations essentielles liées à une autorisation de marchandisage de retour (RMA).

![Diagramme du type de données Retour .](../images/data-types/return.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Identifiant de retour] | `returnID` | chaîne | Identifiant unique de cette RAM. |
| [!UICONTROL Statut de retour] | `returnStatus` | chaîne | État actuel de la RAM (par exemple, En attente ou Fermé). |
| [!UICONTROL Identifiant de commande] | `purchaseID` | chaîne | Identifiant unique de la commande/de l’achat auquel la RMA se rapporte. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)


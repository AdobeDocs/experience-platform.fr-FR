---
title: Type de données de retour
description: Découvrez le type de données Modèle de données d’expérience d’élément de retour (XDM) .
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# [!UICONTROL Élément de retour] type de données

[!UICONTROL Élément de retour] est un type de données XDM (Experience Data Model) standard qui capture les détails essentiels liés au processus de retour d’un article acheté.

![Schéma du type de données Article renvoyé.](../images/data-types/return-item.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Statut de retour] | `returnStatus` | chaîne | État de l’élément renvoyé (par exemple, En attente ou Approuvé). |
| [!UICONTROL Raison du retour] | `returnReason` | chaîne | Motif pour lequel le retour a été demandé pour l’élément. |
| [!UICONTROL Condition de retour] | `returnItemCondition` | chaîne | La condition de l’élément pour lequel le retour est demandé. |
| [!UICONTROL Résolution des retours] | `returnResolution` | chaîne | Résolution ou résultat souhaité attendu du retour (par exemple, Remboursement ou Exchange). |
| [!UICONTROL Quantité renvoyée demandée] | `returnQuantityRequested` | nombre entier | Quantité de l’article que l’acheteur a demandé de renvoyer. |
| [!UICONTROL Quantité renvoyée autorisée] | `returnQuantityAuthorized` | nombre entier | Quantité de l’article autorisée à être renvoyée. |
| [!UICONTROL Quantité renvoyée] | `returnQuantityReceived` | nombre entier | Nombre d’éléments renvoyés reçus. |
| [!UICONTROL Quantité renvoyée approuvée] | `returnQuantityApproved` | nombre entier | La quantité de l’élément avec un retour complet et approuvé. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)

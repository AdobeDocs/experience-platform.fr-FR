---
title: Type de données de retour
description: Découvrez le type de données Modèle de données d’expérience d’élément de retour (XDM) .
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 7%

---

# Type de données [!UICONTROL Return Item]

[!UICONTROL Article de retour] est un type de données XDM (Experience Data Model) standard qui capture les détails essentiels liés au processus de retour d’un article acheté.

![Schéma du type de données Article de retour.](../images/data-types/return-item.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Statut de retour] | `returnStatus` | Chaîne | État de l’élément renvoyé (par exemple, En attente ou Approuvé). |
| [!UICONTROL Raison de retour] | `returnReason` | Chaîne | Motif pour lequel le retour a été demandé pour l’élément. |
| [!UICONTROL Condition de retour de l’élément] | `returnItemCondition` | Chaîne | La condition de l’élément pour lequel le retour est demandé. |
| [!UICONTROL Résolution de retour] | `returnResolution` | Chaîne | Résolution ou résultat souhaité attendu du retour (par exemple, Remboursement ou Exchange). |
| [!UICONTROL Quantité renvoyée demandée] | `returnQuantityRequested` | Entier | Quantité de l’article que l’acheteur a demandé de renvoyer. |
| [!UICONTROL Quantité renvoyée autorisée] | `returnQuantityAuthorized` | Entier | Quantité de l’article autorisée à être renvoyée. |
| [!UICONTROL Quantité renvoyée ] | `returnQuantityReceived` | Entier | Nombre d’éléments renvoyés reçus. |
| [!UICONTROL Retour Quantité Approuvé] | `returnQuantityApproved` | Entier | La quantité de l’élément avec un retour complet et approuvé. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)

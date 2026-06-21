---
title: Type de données d'article retourné
description: Découvrez le type de données Modèle de données d’expérience d’élément renvoyé (XDM).
exl-id: e703d65b-a133-484e-96d6-6b1f50fc1e48
TQID: https://experienceleague.adobe.com/L7f0Y1UQQlslZr4oLtAoc7EDOG2DJndUtpU56-boWZw
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 206
ht-degree: 6%

---

# Type de données [!UICONTROL Article renvoyé]

[!UICONTROL Article renvoyé] est un type de données standard du modèle de données d’expérience (XDM) qui capture les détails essentiels liés au processus de retour d’un article acheté.

![Diagramme du type de données Article renvoyé.](../images/data-types/return-item.png)

| Nom d’affichage | Propriété | Type de données | Description |
|-----------------------------|------------------------------|-----------|--------------------------------------------------------|
| [!UICONTROL Statut de retour] | `returnStatus` | chaîne | Statut de l’élément renvoyé (par exemple, En attente ou Approuvé). |
| [!UICONTROL Motif de retour] | `returnReason` | chaîne | Motif pour lequel le retour a été demandé pour l&#39;article. |
| [!UICONTROL Condition de retour de l&#39;article] | `returnItemCondition` | chaîne | Condition de l&#39;article pour lequel le retour est demandé. |
| [!UICONTROL Résolution de retour] | `returnResolution` | chaîne | Résolution souhaitée ou résultat attendu du retour (par exemple, remboursement ou échange). |
| [!UICONTROL Quantité de retour demandée] | `returnQuantityRequested` | entier | Quantité de l&#39;article que l&#39;acheteur a demandé de retourner. |
| [!UICONTROL Quantité de retour autorisée] | `returnQuantityAuthorized` | entier | Quantité de l’article dont le retour est autorisé. |
| [!UICONTROL Quantité de retour reçue] | `returnQuantityReceived` | entier | Quantité d&#39;articles retournés reçue. |
| [!UICONTROL Quantité retournée approuvée] | `returnQuantityApproved` | entier | Quantité de l&#39;article avec un retour entièrement terminé et approuvé. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/returnitem.schema.json)

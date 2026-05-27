---
title: Type de données de rapport des détails du pod Advertising
description: Découvrez le type de données du modèle de données d’expérience (XDM) de création de rapports sur les détails des capsules Advertising.
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
TQID: https://experienceleague.adobe.com/nRZ1HWwdKpV3MY11mMyC5yGWbZOiZyCYbb-zVhBb0ik
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c20d46e7-1c7d-476c-a50e-3961d4dce35f
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 164
ht-degree: 11%

---

# Type de données [!UICONTROL Advertising Pod Details Reporting]

[!UICONTROL Advertising Pod Details Reporting] est un type de données standard du modèle de données d’expérience (XDM). Il définit une séquence ou un groupe d’annonces généralement lues successivement pendant les pauses de contenu. Utilisez le type de données [!UICONTROL Advertising Pod Details Reporting] pour capturer des détails tels que l’identifiant de coupure publicitaire, un nom convivial pour la coupure publicitaire, l’index des publicités dans la coupure et le décalage de la coupure publicitaire dans le journal du contenu en secondes.

![Diagramme du type de données Rapports détaillés sur les pods Advertising.](../images/data-types/advertising-pod-details-information.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Ad Break ID] | `ID` | chaîne | Identifiant de la coupure publicitaire. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | chaîne | Nom facilement compréhensible de la coupure publicitaire. |
| [!UICONTROL Ad In Pod Position] | `index` | entier | Index de la publicité à l’intérieur du début de la coupure publicitaire parent. |
| [!UICONTROL Pod Offset] | `offset` | entier | **Obligatoire** décalage de la coupure publicitaire dans le contenu, en secondes. |

{style="table-layout:auto"}

Pour plus d’informations sur le groupe de champs , consultez le [référentiel XDM public](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)

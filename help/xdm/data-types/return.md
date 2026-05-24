---
title: Type de données de retour
description: Découvrez le type de données du modèle de données d’expérience de retour (XDM).
exl-id: 1fd99a25-547f-49e7-8980-dda7db2ebb8a
TQID: https://experienceleague.adobe.com/4tYQzlTE8Otqmv-W3sVw5nhNShuSFqGwjF0mEIClpMQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 118
ht-degree: 7%

---

# Type de données [!UICONTROL Return]

[!UICONTROL Return] est un type de données XDM (modèle de données d’expérience) standard qui capture les informations essentielles liées à une autorisation de retour de marchandise (RMA).

![Diagramme du type de données Retour.](../images/data-types/return.png)

| Nom d’affichage | Propriété | Type de données | Description |
|----------------------------------|----------------------|-----------|--------------------------------------------------|
| [!UICONTROL Return ID] | `returnID` | chaîne | Identifiant unique de ce RMA. |
| [!UICONTROL Return Status] | `returnStatus` | chaîne | Statut actuel du RMA (par exemple En attente ou Fermé). |
| [!UICONTROL Order Purchase ID] | `purchaseID` | chaîne | Identifiant unique de la commande/de l&#39;achat auquel la RMA se rapporte. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/return.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/return.schema.json)

---
title: Type de données de liste de demandes d'approvisionnement
description: Découvrez le type de données Modèle de données d'expérience (XDM) de liste de demandes d'approvisionnement.
exl-id: cbea6b08-9d4d-4cbe-b0c5-506bccc6df67
TQID: https://experienceleague.adobe.com/PJjU5TIr7vs8HD1Y5Ymo3KwDU1jprtGjLD6OGqRAazQ
product_v2:
  - id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 126
ht-degree: 7%

---

# Type de données [!UICONTROL Requisition List]

[!UICONTROL Requisition List] est un type de données XDM (modèle de données d’expérience) standard qui décrit une collection sélectionnée d’articles pour l’approvisionnement ou l’achat. Utilisez le type de données [!UICONTROL Requisition List] pour identifier et décrire les listes de demandes d&#39;approvisionnement.

![Diagramme du type de données [!UICONTROL Requisition List].](../images/data-types/requisition-list.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL Requisition List ID] | `ID` | chaîne | Identifiant unique de la liste des demandes d&#39;approvisionnement. |
| [!UICONTROL Requisition List Name] | `name` | chaîne | Nom de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| [!UICONTROL Requisition List Description] | `description` | chaîne | Description de la liste de demandes d&#39;approvisionnement spécifiée par le client. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)

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
source-wordcount: 143
ht-degree: 6%

---

# [!UICONTROL Liste des demandes] type de données

[!UICONTROL Liste de demandes d&#39;approvisionnement] est un type de données standard des modèles de données d&#39;expérience (XDM) qui décrit une collection sélectionnée d&#39;articles pour l&#39;approvisionnement ou l&#39;achat. Utilisez le type de données [!UICONTROL Liste de demandes d&#39;approvisionnement] pour identifier et décrire les listes de demandes d&#39;approvisionnement.

![Diagramme du type de données [!UICONTROL Liste de demandes].](../images/data-types/requisition-list.png)

| Nom d’affichage | Propriété | Type de données | Description |
|---------------------------|-------------------|-----------|--------------------------------------------------|
| [!UICONTROL ID de la liste de demandes] | `ID` | chaîne | Identifiant unique de la liste des demandes d&#39;approvisionnement. |
| [!UICONTROL Nom de la liste de demandes d&#39;approvisionnement] | `name` | chaîne | Nom de la liste de demandes d&#39;approvisionnement spécifiée par le client. |
| [!UICONTROL Description de la liste de demandes d&#39;approvisionnement] | `description` | chaîne | Description de la liste de demandes d&#39;approvisionnement spécifiée par le client. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/requisitionlist.schema.json)

---
title: Détails de l’audit du système Source externe
description: Découvrez le groupe de champs Modèle de données d’expérience (XDM) des détails de l’audit du système Source externe.
exl-id: 6aa154f3-620f-4a2e-9e33-a0757d0491c1
TQID: https://experienceleague.adobe.com/MtjYYQcIRWhPkj90NFtJZzB7uZDuIny9xN5cCJsgvaE
product_v2: id: edbd1a0e-46c8-49da-8c10-dba9ec80bba9
feature_v2: id: c132d929-fa62-4271-803e-b823be07b914
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 150
ht-degree: 4%

---

# [!UICONTROL External Source System Audit Details] le groupe de champs

[!UICONTROL External Source System Audit Details] est un groupe de champs standard du modèle de données d’expérience (XDM) qui étend le type de données principal « Attributs d’audit du système Source externe » en référençant ses propriétés et en ajoutant des métadonnées contextuelles. Cela permet un suivi d’audit détaillé et une intégration de données flexible à partir de sources externes.

![Schéma du groupe de champs Détails de l’audit du système Source externe.](../../images/field-groups/shared/external-source-system-audit-details.png)

| Nom d’affichage | Propriété | Type de données | Description |
| -------------------------------------------------| ---------------------------------------- | --------- | --- |
| [!UICONTROL External Source System Audit Details] | `external-source-system-audit-details` | [[!UICONTROL External Source System Audit Attributes]](../../data-types/external-source-system-audit-attributes.md) | Le groupe de champs « [!UICONTROL External Source System Audit Details] » étend le type de données principal « Attributs d’audit du système Source externe » en référençant ses propriétés et en ajoutant des métadonnées contextuelles. Cela facilite le suivi d’audit détaillé et l’intégration de données flexible pour les sources externes, en prenant en charge la nature asynchrone de l’ingestion de profils. |

{style="table-layout:auto"}

Pour plus d’informations sur ce type de données, reportez-vous au référentiel XDM public :

* [Schéma complet](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.json)

---
title: Détails de l’audit du système Source externe
description: Découvrez le groupe de champs Modèle de données d’expérience (XDM) des détails de l’audit du système Source externe.
exl-id: 6aa154f3-620f-4a2e-9e33-a0757d0491c1
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '136'
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

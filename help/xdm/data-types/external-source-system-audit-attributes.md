---
title: Type de données Attributs d’audit du système Source externe
description: Découvrez le type de données Modèle de données d’expérience (XDM) des attributs de contrôle du système Source externe.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: 03735e7099ffb2cfd44fc7fffd35e3a4a858e3ba
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---

# Type de données [!UICONTROL Attributs d’audit de système Source externes]

[!UICONTROL Attributs d’audit de système Source externe] est un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système source externe.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Source B2B]](./b2b-source.md) | Identifiant composite de la source utilisée pour le contrôle. |
| `createdBy` | Chaîne | Nom de l’utilisateur qui a créé cet enregistrement. |
| `createdDate` | DateTime | Date de création de cet enregistrement. |
| `externalID` | Chaîne | Identifiant unique externe de la source. Cette valeur permet d’identifier et de dédupliquer si nécessaire. |
| `lastActivityDate` | DateTime | Date de la dernière activité du système source. |
| `lastReferencedDate` | DateTime | Dernière date référencée pour le système source. |
| `lastUpdatedBy` | Chaîne | Nom de la personne qui a mis à jour cet enregistrement pour la dernière fois. |
| `lastUpdatedDate` | DateTime | Date de la dernière mise à jour du système source. Cette valeur est utilisée par la [stratégie de fusion d’attributs](../../profile/api/merge-policies.md#attribute-merge) pour déterminer la priorité en cas de conflit de fusion. |
| `lastViewedDate` | DateTime | Date de dernière consultation du système source. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple renseigné](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)

---
title: Type de données Attributs d’audit du système de source externe
description: Découvrez le type de données Modèle de données d’expérience (XDM) des attributs d’audit du système source externe.
exl-id: ebdd8707-9675-4232-a5b7-4e4a481d706a
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---

# [!UICONTROL Attributs d’audit du système de source externe] type de données

[!UICONTROL Attributs d’audit du système de source externe] est un type de données XDM (Experience Data Model) standard qui capture les détails de l’audit sur un système source externe.

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
| `lastUpdatedDate` | DateTime | Date de la dernière mise à jour du système source. |
| `lastViewedDate` | DateTime | Date de dernière consultation du système source. |

{style="table-layout:auto"}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)

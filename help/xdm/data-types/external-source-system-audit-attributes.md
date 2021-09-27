---
title: Type de données Attributs d’audit du système de source externe
description: Ce document présente un aperçu du type de données XDM (Extend Source Audit System Attributes) du modèle de données d’expérience (XDM).
source-git-commit: 8bf0c63f33ae9cbfb01d4db9e5220c6762575c5b
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 6%

---

# [!UICONTROL Type de données ] Attributs d’audit du système de source externe

>[!NOTE]
>
>Ce type de données est uniquement disponible pour les organisations qui ont accès à l’édition B2B de la plateforme de données clients en temps réel.

[!UICONTROL Les ] attributs d’audit du système source externe sont un type de données XDM (Experience Data Model) standard qui capture les détails d’audit d’un système source externe.

![](../images/data-types/external-source-system-audit-attributes.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `externalKey` | [[!UICONTROL Source B2B]](./b2b-source.md) | Identifiant composite de la source utilisée pour le contrôle. |
| `createdBy` | Chaîne | Nom de l’utilisateur qui a créé cet enregistrement. |
| `createdDate` | DateTime | Date de création de cet enregistrement. |
| `externalID` | Chaîne | Identifiant unique externe de la source. Cette valeur permet d’identifier et de dédupliquer si nécessaire. |
| `lastActivityDate` | DateTime | Date de la dernière activité du système source. |
| `lastReferencedDate` | DateTime | Dernière date référencée du système source. |
| `lastUpdatedBy` | Chaîne | Nom de la personne qui a mis à jour cet enregistrement pour la dernière fois. |
| `lastUpdatedDate` | DateTime | Date de la dernière mise à jour du système source. |
| `lastViewedDate` | DateTime | Date de dernière consultation du système source. |

{style=&quot;table-layout:auto&quot;}

Pour plus d’informations sur le type de données, reportez-vous au référentiel XDM public :

* [Exemple rempli](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.example.1.json)
* [Schéma complet](https://github.com/adobe/xdm/blob/master/components/datatypes/auditing/external-source-system-audit.schema.json)

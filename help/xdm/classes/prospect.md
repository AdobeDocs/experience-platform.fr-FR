---
title: Classe XDM Individual Prospect
description: Ce document présente la classe XDM Individual Prospect Profile dans le modèle de données d’expérience (XDM).
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 12%

---

# [!UICONTROL Profil XDM Individual Prospect] class

Dans le modèle de données d’expérience (XDM), le [!UICONTROL Profil XDM Individual Prospect] capture les profils prospect provenant généralement des partenaires de données pour les cas d’utilisation d’acquisition client top-of-the-funnel.

![Schéma de la classe XDM Prospect.](../images/classes/individual-prospect-profile.png)

| Propriété | Type de données | Description |
| --- | --- | --- |
| `_repo` | Objet | Cette classe vous permet d’importer des profils de prospect provenant de fournisseurs de données pour gérer les cas d’utilisation d’acquisition de clients. |
| `_repo.createDate` | [!UICONTROL DateTime] | Date et heure du serveur auxquelles la ressource a été créée dans le référentiel. L’heure de création peut être le premier chargement d’un fichier de ressource ou la création d’un répertoire par le serveur en tant que parent d’une nouvelle ressource. La propriété datetime doit être conforme à la norme ISO 8601. Exemple de ce format : &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_repo.modifyDate` | [!UICONTROL DateTime] | Date et heure du serveur auxquelles la ressource a été modifiée dans le référentiel pour la dernière fois, par exemple lorsqu’une ressource est chargée ou que la ressource enfant d’un répertoire est ajoutée ou supprimée. La propriété datetime doit être conforme à la norme ISO 8601. Exemple de formulaire : &quot;2004-10-23T12:00:00-06:00&quot;. |
| `_id` | [!UICONTROL Chaîne] | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne fournit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez. |
| `createdByBatchID` | [!UICONTROL Chaîne] | Identifiant du lot ingéré à l’origine de la création de l’enregistrement. |
| `modifiedByBatchID` | [!UICONTROL Chaîne] | L’identifiant du dernier lot ingéré qui a provoqué la mise à jour de l’enregistrement. |
| `partnerID` | [!UICONTROL Chaîne] | En règle générale, un identifiant pseudonyme unique qui identifie un prospect individuel. Consultez la documentation relative à [types d’identité](../../identity-service/namespaces.md#identity-type) pour en savoir plus sur l’identifiant de partenaire et les autres types d’identité disponibles dans Adobe Experience Platform. |
| `repositoryCreatedBy` | [!UICONTROL Chaîne] | L’identifiant de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | [!UICONTROL Chaîne] | L’identifiant de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. Lors de la création de l’enregistrement, la variable `modifiedByUser` est définie comme `createdByUser` . |

{style="table-layout:auto"}

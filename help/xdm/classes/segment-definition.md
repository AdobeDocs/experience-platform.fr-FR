---
solution: Experience Platform
title: Classe de définition de segment
description: Découvrez la classe de définition de segment dans le modèle de données d’expérience (XDM).
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 1%

---

# [!UICONTROL Définition de segment] class

&quot;[!UICONTROL Définition de segment]&quot; est une classe XDM (Experience Data Model) standard qui capture les détails d’une définition de segment. La classe comprend les champs obligatoires tels que l’identifiant et le nom d’une audience, ainsi que d’autres attributs facultatifs. Cette classe doit être utilisée si vous incorporez des définitions de segment à partir de systèmes externes dans Adobe Experience Platform.

>[!NOTE]
>
>Cette classe ne doit être utilisée que pour capturer des informations sur les définitions de segment elles-mêmes. Pour capturer les informations d’appartenance à une audience dans vos données de profil, vous devez utiliser la variable [Groupe de champs Détails de l’appartenance à un segment](../field-groups/profile/segmentation.md) dans votre [!UICONTROL XDM Individual Profile] schéma.

![](../images/classes/segment-definition.png)

| Propriété | Description |
| --- | --- |
| `_repo` | Un objet contenant les éléments suivants [!UICONTROL DateTime] fields : <ul><li>`createDate`: date et heure de création de la ressource dans l’entrepôt de données, telles que le moment où les données ont été ingérées pour la première fois.</li><li>`modifyDate`: date et heure de la dernière modification de la ressource.</li></ul> |
| `_id` | Identifiant de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l’unicité d’un enregistrement individuel, d’éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’ingestion des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’identifiant uniques si vous le souhaitez.<br><br>Il est important de distinguer que ce champ **ne fait pas** représentent une identité liée à une personne individuelle, mais plutôt l’enregistrement des données lui-même. Les données d’identité relatives à une personne doivent être reléguées à [champs d’identité](../schema/composition.md#identity) au lieu de . |
| `createdByBatchID` | Identifiant du lot ingéré à l’origine de la création de l’enregistrement. |
| `description` | Description de la définition de segment. |
| `identityMap` | Champ de mappage contenant un ensemble d’identités d’espace de noms pour les individus auxquels s’applique l’audience. Consultez la section sur les mappages d’identité dans la [principes de base de la composition des schémas](../schema/composition.md#identityMap) pour plus d’informations sur leur cas d’utilisation. |
| `modifiedByBatchID` | L’identifiant du dernier lot ingéré qui a provoqué la mise à jour de l’enregistrement. |
| `repositoryCreatedBy` | L’identifiant de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | L’identifiant de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |
| `segmentName` | **(Obligatoire)** Nom de la définition de segment. |
| `segmentStatus` | État de l’audience du système externe. Les valeurs suivantes sont acceptées : <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Numéro de la dernière version de la définition de segment. |

{style="table-layout:auto"}

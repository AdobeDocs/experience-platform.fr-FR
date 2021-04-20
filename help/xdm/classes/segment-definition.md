---
solution: Experience Platform
title: Classe de définition de segment
topic: overview
description: Ce document fournit un aperçu de la classe de définition de segment dans le modèle de données d’expérience (XDM).
translation-type: tm+mt
source-git-commit: f4e80cc6a5e5e135bedb77b2d56ae5cb2c8d8c53
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# [!UICONTROL Classe de ] définition de segment

&quot;[!UICONTROL Définition de segment]&quot; est une classe XDM (Experience Data Model) standard qui capture les détails d’une définition de segment. La classe comprend les champs obligatoires tels que l&#39;ID et le nom d&#39;un segment, ainsi que d&#39;autres attributs facultatifs. Cette classe doit être utilisée si vous incorporez des définitions de segment à partir de systèmes externes dans Adobe Experience Platform.

>[!NOTE]
>
>Cette classe ne doit être utilisée que pour capturer des informations sur les définitions de segment elles-mêmes. Afin de capturer les informations d’appartenance aux segments dans vos données de profil, vous devez utiliser le [mixin Détails d’appartenance aux segments](../mixins/profile/segmentation.md) dans votre schéma [!UICONTROL Profil individuel XDM].

![](../images/classes/segment-definition.png)

| Propriété | Description |
| --- | --- |
| `_repo` | Objet contenant les champs [!UICONTROL DateTime] suivants : <ul><li>`createDate`: Date et heure de création de la ressource dans le magasin de données, par exemple, date à laquelle les données ont été ingérées pour la première fois.</li><li>`modifyDate`: Date et heure de la dernière modification de la ressource.</li></ul> |
| `_id` | Identificateur de chaîne unique généré par le système pour l’enregistrement. Ce champ permet de suivre l&#39;unicité d&#39;un enregistrement individuel, d&#39;éviter la duplication des données et de rechercher cet enregistrement dans les services en aval.<br><br>Ce champ étant généré par le système, il ne reçoit pas de valeur explicite lors de l’assimilation des données. Cependant, vous pouvez toujours choisir de fournir vos propres valeurs d’ID uniques si vous le souhaitez.<br><br>Il est important de distinguer que ce champ  **ne** représente pas une identité liée à une personne, mais plutôt l&#39;enregistrement des données. Les données d&#39;identité relatives à une personne doivent être reléguées à [champs d&#39;identité](../schema/composition.md#identity). |
| `createdByBatchID` | ID du lot assimilé à l&#39;origine de la création de l&#39;enregistrement. |
| `description` | Description de la définition de segment. |
| `identityMap` | Champ de mappage contenant un ensemble d’identités d’espacement de noms pour les individus auxquels s’applique le segment. Ce champ est automatiquement mis à jour par le système lorsque des données d&#39;identité sont saisies.<br /><br />Consultez la section sur les cartes d&#39;identité dans les  [bases de la ](../schema/composition.md#identityMap) composition de schémas pour plus d&#39;informations sur leur cas d&#39;utilisation. |
| `modifiedByBatchID` | ID du dernier lot assimilé qui a provoqué la mise à jour de l&#39;enregistrement. |
| `repositoryCreatedBy` | ID de l’utilisateur qui a créé l’enregistrement. |
| `repositoryLastModifiedBy` | ID de l’utilisateur qui a modifié l’enregistrement pour la dernière fois. |
| `segmentName` | **(Obligatoire)** Nom de la définition de segment. |
| `segmentStatus` | Statut du segment à partir du système externe. Les valeurs suivantes sont acceptées : <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | Numéro de la dernière version de la définition de segment. |

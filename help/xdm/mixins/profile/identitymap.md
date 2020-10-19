---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Mélin IdentityMap
topic: overview
description: Ce document fournit un aperçu de la classe de Profil XDM Individuel.
translation-type: tm+mt
source-git-commit: fd5bd4134bd35d5d87c79bf1e75bc88c67511b2b
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# [!UICONTROL Mélin IdentityMap]

[!UICONTROL IdentityMap] est un mixin standard pour la [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le mixin fournit un champ de mappage unique, qui contient un ensemble d’identités utilisateur clés par espace de nommage.

>[!WARNING]
>
>Le `IdentityMap` champ est automatiquement mis à jour par le système lorsque des données d&#39;identité sont saisies. Afin d’utiliser correctement ce champ pour le Profil [client en temps](../../../profile/home.md)réel, n’essayez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Consultez la section sur les cartes d&#39;identité dans les [bases de la composition](../../schema/composition.md#identityMap) des schémas pour plus d&#39;informations sur leur cas d&#39;utilisation.
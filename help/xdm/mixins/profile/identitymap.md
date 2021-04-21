---
keywords: Experience Platform ; accueil ; sujets populaires ; schéma ; Schéma ; XDM ; profil individuel ; champs ; schémas ; Schémas ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; IdentityMap ; Schéma design ; map ; Map ; union schéma ; union
solution: Experience Platform
title: Mélange IdentityMap
topic-legacy: overview
description: Ce document fournit un aperçu de la classe de Profil XDM Individuel.
exl-id: c9928e85-ef1e-4739-ba1d-80505a9e60c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

#  IdentityMapmixin

>[!NOTE]
>
>Les noms de plusieurs mixins ont changé. Pour plus d’informations, consultez le document [Mises à jour du nom de mixin](../name-updates.md).

 IdentityMapis est un mixin standard pour la  [[!DNL XDM Individual Profile] classe](../../classes/individual-profile.md). Le mixin fournit un champ de mappage unique, qui contient un ensemble d’identités utilisateur clés par espace de nommage.

>[!WARNING]
>
>Le champ `IdentityMap` est automatiquement mis à jour par le système lorsque des données d&#39;identité sont saisies. Afin d’utiliser correctement ce champ pour [Profil client en temps réel](../../../profile/home.md), n’essayez pas de mettre à jour manuellement le contenu du champ dans vos opérations de données.

<img src="../../images/mixins/identitymap.png" width="600" /><br />

Consultez la section sur les cartes d&#39;identité dans les [bases de la composition des schémas](../../schema/composition.md#identityMap) pour plus d&#39;informations sur leur cas d&#39;utilisation.

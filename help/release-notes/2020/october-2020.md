---
title: Notes de mise à jour d’Adobe Experience Platform
description: Notes de mise à jour des Experience Platform Octobre 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 50%

---


# Notes de mise à jour d’Adobe Experience Platform

**Date de publication : Octobre 2020**

Nouvelles fonctionnalités d’Adobe Experience Platform :

- [[ !Contrôle d&#39;accès DNL]](#access-control)
- [[ ! Sandbox DNL]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] exploite les profils de produit [Adobe Admin Console](https://adminconsole.adobe.com) pour lier les utilisateurs à des autorisations et des environnements de test. Les autorisations contrôlent l’accès à de nombreuses fonctionnalités de Platform, notamment la modélisation des données, la gestion des profils et l’administration des environnements de test.

**Fonctionnalités clés**

| Fonctionnalité | Description |
|--- | ---|
| Autorisations | In the [!DNL Admin Console], the  tab within a [!DNL Platform] product profile allows you customize which [!DNL Platform] capabilities are available for the users attached to that profile. Available permission categories include: [!UICONTROL Data Modeling], [!UICONTROL Data Management], [!UICONTROL Profile Management], [!UICONTROL Identities], [!UICONTROL Data Monitoring], [!UICONTROL Sandbox Administration], [!UICONTROL Destinations], [!UICONTROL Sources]. |
| Accès aux environnements de test | L’onglet [!UICONTROL _Autorisations_] d’un profil de produit peut accorder aux utilisateurs l’accès à des environnements de test spécifiques. [!DNL Platform] Consultez la section sur les [environnements de test](#sandboxes) ci-dessous pour plus d’informations. |

Pour plus d’informations, consultez la [présentation du contrôle d’accès](../../access-control/home.md).

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] est conçu pour enrichir les applications d’expérience numérique à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience numérique en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. In order to address this need, [!DNL Experience Platform] provides sandboxes which partition a single [!DNL Platform] instance into separate virtual environments to help develop and evolve digital experience applications.

**Fonctionnalités clés**

| Fonctionnalité | Description |
|--- | ---|
| Environnement de test de production | [!DNL Experience Platform] fournit un environnement de test de production unique, qui ne peut pas être supprimé ou réinitialisé. |
| Environnement de test hors production | Multiple non-production sandboxes can be created for a single [!DNL Platform] instance, allowing you to test features, run experiments, and make custom configurations without impacting your production sandbox. |
| Sélecteur d’environnement de test | In the [!DNL Experience Platform] user interface, the sandbox switcher in the top-left corner of the screen allows you to switch between available sandboxes through a dropdown menu. |
| En-tête `x-sandbox-name` | All calls to [!DNL Experience Platform] APIs must now include the new `x-sandbox-name` header, whose value references the `name` attribute of the sandbox the operation will take place in. |

Pour plus d’informations, consultez la [présentation des environnements de test](../../sandboxes/home.md).
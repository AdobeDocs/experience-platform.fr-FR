---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Confidentialité du profil de données client en temps réel
seo-title: Confidentialité du profil de données client en temps réel
description: Le profil de données client en temps réel vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les règles de confidentialité.
seo-description: Le profil de données client en temps réel vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les règles de confidentialité.
translation-type: tm+mt
source-git-commit: f9b21ee51d6246dbdae4500aad050b200539ff88
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 57%

---


# Confidentialité dans la plateforme de données client en temps réel

[!DNL Real-time Customer Data Platform] (CDP en temps réel) aide les marketeurs à rassembler les données issues de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et impliquer leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

La plupart des fonctionnalités de la plateforme CDP en temps réel fonctionnent avec Adobe Experience Platform. This document provides information about the various privacy enhancement technologies supported by Real-time CDP, with links to [!DNL Experience Platform] documentation for more information.

## [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] vous permet de rationaliser le processus de conservation de vos opérations de données en conformité avec les réglementations sur la confidentialité, telles que le [!DNL General Data Protection Regulation] (RGPD) et l&#39; [!DNL California Consumer Privacy Act] (ACCP). Since Real-time CDP leverages [!DNL Experience Platform] capabilities for data collection and storage, the access and delete requests for GDPR and CCPA should be managed within [!DNL Platform]. Consultez le document [Présentation du service confidentialité](../../privacy-service/home.md) pour une présentation plus détaillée du service.

Il existe deux manières de soumettre des requêtes individuelles pour consulter ou supprimer des données de propriétaires dans le cadre du RGPD ou de la CCPA :

* Use the [[!DNL Privacy Service UI]](https://privacyui.cloud.adobe.io/) to create and monitor access and delete requests within a visual workspace. See the [Privacy Service user guide](../../privacy-service/ui/overview.md) for step-by-step instructions.
* Use the [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) to manage access and delete requests with RESTful API calls. Consultez le [tutoriel sur L’API du service confidentialité](../../privacy-service/api/getting-started.md) pour obtenir des instructions étapes par étape.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](../../profile/home.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Étapes suivantes

Ce document présente brièvement les fonctionnalités de gestion de la confidentialité de la plateforme CDP en temps réel. Pour des informations plus détaillées sur les bonnes pratiques et les étapes à suivre pour envoyer des requêtes d’accès/de suppression, consultez la [documentation du service confidentialité](../../privacy-service/home.md).
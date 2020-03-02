---
title: Confidentialité du profil de données client en temps réel
seo-title: Confidentialité du profil de données client en temps réel
description: Le profil de données client en temps réel vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les règles de confidentialité.
seo-description: Le profil de données client en temps réel vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les règles de confidentialité.
translation-type: ht
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# Confidentialité dans la plateforme de données client en temps réel

La plateforme de données client (CDP) en temps réel permet aux spécialistes marketing de rassembler des données issues de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et interagir avec leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

La plupart des fonctionnalités de la plateforme CDP en temps réel fonctionnent avec Adobe Experience Platform. Ce document fournit des informations sur les différentes technologies d’amélioration de la confidentialité prises en charge par la plateforme CDP en temps réel ainsi que des liens vers la documentation plus exhaustive d’Experience Platform.

## Service confidentialité

Le service confidentialité d’Adobe Experience Platform permet de rationaliser le processus de mise en conformité de vos opérations de données aux règles de confidentialité telles que le règlement général sur la protection des données (RGPD) et la Loi sur la protection de la confidentialité des consommateurs (CCPA) de Californie. Comme la plateforme CDP en temps réel utilise les fonctionnalités d’Experience Platform pour collecter et stocker les données, les demandes d’accès et de suppression dans le cadre du RGPD et de la CCPA doivent être gérées dans Platform. Consultez le document [Présentation du service confidentialité](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md) pour une présentation plus détaillée du service.

Il existe deux manières de soumettre des requêtes individuelles pour consulter ou supprimer des données de propriétaires dans le cadre du RGPD ou de la CCPA :

* Utiliser l’[interface utilisateur du service confidentialité](https://gdprui.cloud.adobe.io/) pour créer et surveiller des requêtes d’accès et de suppression dans un espace de travail visuel. Consultez le [tutoriel sur l’interface utilisateur du service confidentialité](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) pour obtenir des instructions étape par étape.
* Utiliser [l’API du service confidentialité](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html) pour gérer les requêtes d’accès et de suppression avec les appels d’API RESTful. Consultez le [tutoriel sur L’API du service confidentialité](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md) pour obtenir des instructions étapes par étape.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Étapes suivantes

Ce document présente brièvement les fonctionnalités de gestion de la confidentialité de la plateforme CDP en temps réel. Pour des informations plus détaillées sur les bonnes pratiques et les étapes à suivre pour envoyer des requêtes d’accès/de suppression, consultez la [documentation du service confidentialité](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html).
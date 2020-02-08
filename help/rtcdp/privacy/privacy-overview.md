---
title: Confidentialité dans le profil de données client en temps réel
seo-title: Confidentialité dans le profil de données client en temps réel
description: Le profil de données client en temps réel vous permet de rationaliser le processus de conformité de vos opérations de données aux règles de confidentialité.
seo-description: Le profil de données client en temps réel vous permet de rationaliser le processus de conformité de vos opérations de données aux règles de confidentialité.
translation-type: tm+mt
source-git-commit: 5d3bedd97208d9eed3977a35e16a10f4864aedd9

---


# Confidentialité dans CDP en temps réel

La plate-forme de données clientes en temps réel (CDP en temps réel) permet aux spécialistes du marketing de rassembler les données de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et impliquer leurs clients. Adobe considère la confidentialité des données des consommateurs comme un principe fondamental de la conception et fournit divers contrôles pour aider les spécialistes du marketing à gérer la confidentialité des données de leurs clients.

La plupart des fonctionnalités CDP en temps réel sont optimisées par Adobe Experience Platform. Ce document fournit des informations sur les différentes technologies d’amélioration de la confidentialité prises en charge par CDP en temps réel, avec des liens vers la documentation de la plateforme d’expérience pour plus d’informations.

## Service de confidentialité

Le service de confidentialité d’Adobe Experience Platform vous permet de rationaliser le processus de conformité de vos opérations de données aux règles de confidentialité, telles que le Règlement général sur la protection des données (GDPR) et la Loi sur la protection des renseignements personnels des consommateurs (CCPA) de Californie. Comme le CDP en temps réel utilise les fonctionnalités de la plateforme Experience Platform pour la collecte et le stockage des données, les demandes d’accès et de suppression pour le GDPR et le CCPA doivent être gérées dans Platform. Consultez le document d’aperçu [de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/technical_overview/privacy_service_overview/privacy_service_overview.md) Privacy Service pour une présentation plus détaillée du service.

Il existe deux méthodes pour soumettre des demandes individuelles de renseignements sur les RDDC et les personnes visées par l’ACCP pour accéder aux données sur les clients et les supprimer :

* Utilisez l’interface utilisateur [de](https://gdprui.cloud.adobe.io/) Privacy Service pour créer et surveiller des requêtes d’accès et de suppression dans un espace de travail visuel. Consultez le didacticiel [sur l’interface utilisateur de](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_ui_tutorial.md) Privacy Service pour obtenir des instructions détaillées.
* Utilisez l’API [](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html) Privacy Service pour gérer les demandes d’accès et de suppression avec les appels d’API RESTful. Consultez le didacticiel [sur l’API](https://www.adobe.io/apis/experiencecloud/gdpr/docs/alldocs.html#!api-specification/markdown/narrative/tutorials/privacy_service_tutorial/privacy_service_api_tutorial.md) Privacy Service pour obtenir des instructions détaillées.

<!-- (Capability will not be available for November GA) 
## Opt-out capabilities

Real-time CDP provides two types of consumer opt-out capabilities:

1. **General opt-out**: (Waiting on info)
1. **Segment-level opt-out of sale**: Opt-out of sale requests are captured using the Profile Privacy mixin (see the section on "Handling opt-out requests" in the [Real-time Customer Profile overview](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md) for more information). Using this, you can exclude users who have opted out from a segment using boolean logic ("AND NOT") in the segment predicate.
-->

## Étapes suivantes

Ce document présente brièvement les fonctionnalités de protection de la vie privée du CDP en temps réel. Pour plus d’informations sur les meilleures pratiques et les étapes à suivre pour envoyer des demandes d’accès/de suppression, veuillez consulter la documentation [du Service de](https://www.adobe.io/apis/experiencecloud/gdpr/docs.html)protection de la vie privée.
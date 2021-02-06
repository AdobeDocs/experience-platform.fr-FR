---
keywords: gouvernance des données rtcdp ; gestion des données rtcdp ; gestion des données client en temps réel ; gestion des données de profil ; respect de la vie privée rtcdp ; respect de la vie privée rtcdp
title: Confidentialité dans la plateforme de données client en temps réel
seo-title: Confidentialité dans la plateforme de données client en temps réel
description: La plate-forme de données clientes en temps réel vous permet de rationaliser le processus de gestion de vos données en conformité avec les règles de confidentialité.
seo-description: La plate-forme de données clientes en temps réel vous permet de rationaliser le processus de gestion de vos données en conformité avec les règles de confidentialité.
translation-type: tm+mt
source-git-commit: 8d403e73a804953f9584d6a72f945d4444e65d11
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 6%

---


# Confidentialité dans la plateforme de données client en temps réel

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) aide les spécialistes du marketing à rassembler les données de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et impliquer leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

La majorité des capacités [!DNL Real-time CDP] sont alimentées par Adobe Experience Platform. Ce document fournit des informations sur les diverses technologies d&#39;amélioration de la vie privée prises en charge par [!DNL Real-time CDP], avec des liens vers la documentation [!DNL Experience Platform] pour plus d&#39;informations.

## Respect des demandes d’accès et de suppression des clients

Les réglementations légales en matière de confidentialité, telles que le [!DNL General Data Protection Regulation] (RGPD) et le [!DNL California Consumer Privacy Act] (APCC), donnent aux clients le droit de demander l&#39;accès aux données personnelles que vous leur collectez ou de les supprimer. [!DNL Real-time CDP] exploitant les capacités [!DNL Experience Platform] de collecte de données et d&#39;enregistrement, les demandes d&#39;accès et de suppression de leurs données personnelles des clients doivent être gérées dans [!DNL Platform]. Pour plus d&#39;informations, consultez l&#39;aperçu sur [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Fonctionnalités d’exclusion

[!DNL Real-time CDP] permet aux clients de opt-out faire inclure leurs données personnelles dans les cas d’utilisation de la segmentation. Les préférences d’exclusion des clients sont capturées et stockées par [!DNL Real-time Customer Profile] et peuvent être appliquées en excluant les utilisateurs qui se sont retirés d’un segment à l’aide de la logique booléenne (&quot;AND NOT&quot;) dans le prédicat de segment.

Pour plus d’informations, consultez le document [respect des demandes d’exclusion](../../segmentation/honoring-opt-outs.md) dans la documentation de Adobe Experience Platform Segmentation Service.

## Prise en charge d’IAB TCF 2.0

[!DNL Real-time CDP] est construit sur Adobe Experience Platform, qui fait partie de la liste des  [fournisseurs enregistrés ](https://iabeurope.eu/vendor-list-tcf-v2-0/) pour le  [!DNL Transparency & Consent Framework (TCF)], comme indiqué par le  [!DNL Interactive Advertising Bureau (IAB)]. Conformément aux exigences de TCF 2.0, Platform vous permet de collecter des données détaillées sur le consentement des clients et de les intégrer à vos profils clients stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si certains profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

Pour plus d&#39;informations, consultez la présentation de la [prise en charge de l&#39;IAB TCF 2.0 dans Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md).

## Étapes suivantes

Ce document présente brièvement les capacités de [!DNL Real-time CDP] en matière de protection de la vie privée. Veuillez consulter la documentation associée à ce guide pour plus d&#39;informations sur chaque fonction.
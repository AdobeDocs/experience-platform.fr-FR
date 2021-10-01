---
keywords: gouvernance des données rtcdp;gouvernance des données rtcdp;gouvernance des données de profil client en temps réel;rtcdp de confidentialité;rtcdp de confidentialité
title: Confidentialité dans la plateforme de données clients en temps réel
seo-title: Privacy in Real-time Customer Data Platform
description: La plateforme de données clients en temps réel vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les réglementations de confidentialité.
seo-description: Real-time Customer Data Platform allows you to streamline the process of keeping your data operations compliant with privacy regulations.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f193787ac27e30c69d25418656ae9c59c89622dc
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 7%

---

# Confidentialité dans la plateforme de données clients en temps réel

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) aide les marketeurs à rassembler les données de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et impliquer leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

La plupart des fonctionnalités [!DNL Real-time CDP] sont optimisées par Adobe Experience Platform. Ce document fournit des informations sur les différentes technologies d’amélioration de la confidentialité prises en charge par [!DNL Real-time CDP], avec des liens vers la documentation [!DNL Experience Platform] pour plus d’informations.

## Respect des demandes d’accès et de suppression des clients

Les réglementations légales relatives à la confidentialité, telles que le RGPD et le CCPA, donnent aux clients le droit de demander l’accès aux données personnelles que vous collectez auprès d’eux ou de les supprimer. [!DNL General Data Protection Regulation][!DNL California Consumer Privacy Act] Comme [!DNL Real-time CDP] tire parti des fonctionnalités [!DNL Experience Platform] de collecte et de stockage des données, les demandes des clients d’accès et de suppression de leurs données personnelles doivent être gérées dans [!DNL Platform]. Pour plus d’informations, consultez la présentation sur [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) .

## Fonctionnalités d’exclusion

[!DNL Real-time CDP] permet aux clients de ne pas inclure leurs données personnelles dans les cas d’utilisation de segmentation. Les préférences d’exclusion des clients sont capturées et stockées par [!DNL Real-time Customer Profile] et peuvent être appliquées en excluant les utilisateurs qui se sont désinscrits d’un segment à l’aide d’une logique booléenne (&quot;AND NOT&quot;) dans le prédicat de segment.

Pour plus d’informations, consultez le document sur le [respect des demandes d’exclusion](../../segmentation/consents.md) dans la documentation de Adobe Experience Platform Segmentation Service.

## Prise en charge du TCF 2.0 de l’IAB

[!DNL Real-time CDP] est basé sur Adobe Experience Platform, qui fait partie de la  [liste de ](https://iabeurope.eu/vendor-list-tcf-v2-0/) fournisseurs enregistrée pour  [!DNL Transparency & Consent Framework (TCF)], comme indiqué par le  [!DNL Interactive Advertising Bureau (IAB)]. Conformément aux exigences de TCF 2.0, Platform vous permet de collecter des données détaillées sur le consentement des clients et de les intégrer à vos profils client stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si certains profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

Pour plus d’informations, consultez la présentation sur la [prise en charge du TCF 2.0 de l’IAB dans Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) .

## Étapes suivantes

Ce document présente brièvement les fonctionnalités de confidentialité de [!DNL Real-time CDP]. Pour plus d’informations sur chaque fonctionnalité, veuillez consulter la documentation associée à ce guide.

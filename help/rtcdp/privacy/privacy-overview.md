---
keywords: gouvernance des données rtcdp;gouvernance des données rtcdp;gouvernance des données et profil client en temps réel;rtcdp et confidentialité;rtcdp et confidentialité
title: Confidentialité dans Adobe Real-Time Customer Data Platform
description: Adobe Real-Time Customer Data Platform vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les règles de confidentialité.
feature: Get Started, Privacy
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 80%

---

# Confidentialité dans Adobe Real-Time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) permet aux spécialistes marketing de rassembler des données issues de plusieurs systèmes d’entreprise, afin de mieux identifier, comprendre et interagir avec leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

La plupart des fonctionnalités de [!DNL Real-Time CDP] fonctionnent avec Adobe Experience Platform. Ce document fournit des informations sur les différentes technologies d’amélioration de la confidentialité prises en charge par [!DNL Real-Time CDP], ainsi que des liens vers la documentation plus exhaustive d’[!DNL Experience Platform].

## Respect des demandes d’accès et de suppression des clients

Les réglementations légales relatives à la confidentialité, telles que le [!DNL General Data Protection Regulation] (RGPD) et le [!DNL California Consumer Privacy Act] (CCPA) donne aux clients le droit de demander l’accès ou la suppression des données personnelles que vous collectez auprès d’eux. Étant donné que [!DNL Real-Time CDP] tire parti des fonctionnalités d’[!DNL Experience Platform] en matière de collecte et de stockage des données, les demandes d’accès et de suppression des données personnelles des clients doivent être gérées dans [!DNL Experience Platform]. Pour plus d’informations, consultez la présentation d’[Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

>[!IMPORTANT]
>
> Les demandes d’accès à des informations personnelles envoyées par le biais d’Adobe Experience Platform Privacy Service pour Adobe Marketo Engage s’appliquent uniquement aux clients B2B Real-Time CDP.

## Fonctionnalités de désinscription

[!DNL Real-Time CDP] permet aux clients de refuser (opt-out) que leurs données personnelles soient incluses dans les cas d’utilisation de segmentation. Les préférences de désinscription des clients sont capturées et stockées par [!DNL Real-Time Customer Profile] et peuvent être appliquées en excluant les utilisateurs qui se sont désinscrits d’une audience à l’aide d’une logique booléenne (« AND NOT ») dans le prédicat de segment.

Consultez le document sur le [respect des demandes de désinscription](../../segmentation/tutorials/consents.md) dans la documentation du service de segmentation d’Adobe Experience Platform pour plus d’informations.

## Prise en charge de l’IAB TCF 2.0

[!DNL Real-Time CDP] est basé sur Adobe Experience Platform, qui fait partie de la [liste de fournisseurs](https://iabeurope.eu/vendor-list-tcf/) enregistrée pour le [!DNL Transparency & Consent Framework (TCF)], comme indiqué par le [!DNL Interactive Advertising Bureau (IAB)]. Conformément aux exigences de TCF 2.0, Experience Platform vous permet de collecter des données détaillées sur le consentement des clients et de les intégrer à vos profils clients stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si certains profils sont inclus dans les audiences exportées, selon leur cas d’utilisation.

Consultez la présentation sur la [prise en charge de l’IAB TCF 2.0 dans Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) pour plus d’informations.

## Étapes suivantes

Ce document présente brièvement les fonctionnalités de gestion de la confidentialité de [!DNL Real-Time CDP]. Pour plus d’informations sur chaque fonctionnalité, veuillez consulter la documentation associée à ce guide.

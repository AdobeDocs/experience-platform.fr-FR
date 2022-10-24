---
keywords: gouvernance des données rtcdp;gouvernance des données rtcdp;gouvernance des données de profil client en temps réel;rtcdp de confidentialité;rtcdp de confidentialité
title: Confidentialité dans Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les réglementations de confidentialité.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 6%

---

# Confidentialité dans Real-time Customer Data Platform

[!DNL Adobe Real-Time Customer Data Platform] ([!DNL Real-Time CDP]) permet aux marketeurs de rassembler des données issues de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et impliquer leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

La majorité des [!DNL Real-Time CDP] Les fonctionnalités sont optimisées par Adobe Experience Platform. Ce document fournit des informations sur les différentes technologies d’amélioration de la confidentialité prises en charge par [!DNL Real-Time CDP], avec des liens vers [!DNL Experience Platform] pour plus d’informations.

## Respect des demandes d’accès et de suppression des clients

Les réglementations légales relatives à la confidentialité, telles que [!DNL General Data Protection Regulation] (RGPD) et le [!DNL California Consumer Privacy Act] (CCPA) donne aux clients le droit de demander l’accès ou la suppression des données personnelles que vous collectez auprès d’eux. Depuis [!DNL Real-Time CDP] tire [!DNL Experience Platform] Les fonctionnalités de collecte et de stockage des données, les demandes de clients d’accès et de suppression de leurs données personnelles doivent être gérées dans [!DNL Platform]. Consultez la présentation sur [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) pour plus d’informations.

>[!IMPORTANT]
>
> Les demandes d’accès à des informations personnelles envoyées par le biais d’Adobe Experience Platform Privacy Service for Adobe Marketo Engage s’appliquent uniquement aux clients Real-Time CDP B2B.

## Fonctionnalités d’exclusion

[!DNL Real-Time CDP] permet aux clients de ne pas inclure leurs données personnelles dans les cas d’utilisation de segmentation. Les préférences de désinscription des clients sont capturées et stockées par [!DNL Real-time Customer Profile], et peuvent être appliqués en excluant les utilisateurs qui se sont désinscrits d’un segment à l’aide d’une logique booléenne (&quot;AND NOT&quot;) dans le prédicat de segment.

Consultez le document sur [respect des demandes d’exclusion](../../segmentation/consents.md) pour plus d’informations, voir la documentation de Adobe Experience Platform Segmentation Service .

## Prise en charge du TCF 2.0 de l’IAB

[!DNL Real-Time CDP] est basé sur Adobe Experience Platform, qui fait partie de la [liste de fournisseurs](https://iabeurope.eu/vendor-list-tcf-v2-0/) pour le [!DNL Transparency & Consent Framework (TCF)], comme indiqué par la variable [!DNL Interactive Advertising Bureau (IAB)]. Conformément aux exigences de TCF 2.0, Platform vous permet de collecter des données détaillées sur le consentement des clients et de les intégrer à vos profils client stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si certains profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

Consultez la présentation sur [Prise en charge du TCF 2.0 de l’IAB dans Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) pour plus d’informations.

## Étapes suivantes

Ce document présente brièvement les fonctionnalités de confidentialité de [!DNL Real-Time CDP]. Pour plus d’informations sur chaque fonctionnalité, veuillez consulter la documentation associée à ce guide.

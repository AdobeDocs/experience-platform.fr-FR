---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance;privacy rtcdp;rtcdp privacy
title: Confidentialité du profil de données client en temps réel
seo-title: Confidentialité du profil de données client en temps réel
description: Le profil de données client en temps réel vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les règles de confidentialité.
seo-description: Le profil de données client en temps réel vous permet de rationaliser le processus de mise en conformité de vos opérations de données avec les règles de confidentialité.
translation-type: tm+mt
source-git-commit: 1eaadb1877cc5221bf6b0b8eed042287e59155bf
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 21%

---


# Confidentialité dans [!DNL Real-time CDP]

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) aide les spécialistes du marketing à rassembler les données de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et impliquer leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

The majority of [!DNL Real-time CDP] capabilities are powered by Adobe Experience Platform. This document provides information about the various privacy enhancement technologies supported by [!DNL Real-time CDP], with links to [!DNL Experience Platform] documentation for more information.

## Respect des demandes d’accès et de suppression des clients

Les réglementations légales en matière de protection des renseignements personnels, telles que le [!DNL General Data Protection Regulation] (RGPD) et le [!DNL California Consumer Privacy Act] (CCPA), donnent aux clients le droit de demander l&#39;accès aux données personnelles que vous leur fournissez ou de les supprimer. Dans la mesure où [!DNL Real-time CDP] il tire parti [!DNL Experience Platform] des capacités de collecte et d’enregistrement des données, les demandes des clients d’accès et de suppression de leurs données personnelles doivent être gérées dans [!DNL Platform]les limites de ces capacités. See the overview on [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) for more information.

## Fonctionnalités d’exclusion

[!DNL Real-time CDP] permet aux clients de opt-out faire inclure leurs données personnelles dans les cas d’utilisation de la segmentation. Les préférences d’exclusion des clients sont capturées et stockées par [!DNL Real-time Customer Profile]et peuvent être appliquées en excluant les utilisateurs qui se sont retirés d’un segment à l’aide d’une logique booléenne (&quot;AND NOT&quot;) dans le prédicat de segment.

Pour plus d’informations, consultez le document sur le [traitement des demandes](../../segmentation/honoring-opt-outs.md) d’exclusion dans la documentation de Adobe Experience Platform Segmentation Service.

## Prise en charge d’IAB TCF 2.0

[!DNL Real-time CDP] fait partie de la liste [du](https://iabeurope.eu/vendor-list-tcf-v2-0/) fournisseur enregistré pour le [!DNL Transparency & Consent Framework] (TCF), telle que définie par le [!DNL Interactive Advertising Bureau] (IAB). Conformément aux exigences de TCF 2.0, [!DNL Real-time CDP] vous permet de collecter des données détaillées sur le consentement des clients et de les intégrer à vos profils clients stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si certains profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

Pour plus d’informations, voir la présentation de la prise en charge [IAB TCF 2.0 dans [!DNL Real-time CDP]](./iab/overview.md) la section

## Étapes suivantes

This document provided a brief introduction to the privacy capabilities of [!DNL Real-time CDP]. Veuillez consulter la documentation associée à ce guide pour plus d&#39;informations sur chaque fonction.
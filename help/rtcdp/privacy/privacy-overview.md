---
keywords: gouvernance des données rtcdp ; gouvernance des données rtcdp ; gouvernance des données du profil de données client en temps réel ; gouvernance des données du profil de données client ; respect de la vie privée rtcdp ; rtcdp
title: Confidentialité à Real-time Customer Data Platform
seo-title: Privacy in Real-time Customer Data Platform
description: Real-time Customer Data Platform vous permet de simplifier le processus de maintien de vos opérations de données en conformité avec les réglementations en matière de confidentialité.
seo-description: Real-time Customer Data Platform allows you to streamline the process of keeping your data operations compliant with privacy regulations.
exl-id: bcb0e42e-4549-4952-bb69-5534aee353f8
source-git-commit: e3519817559dca372e228ed19bba4f9adf279768
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 6%

---

# Confidentialité à Real-time Customer Data Platform

[!DNL Real-time Customer Data Platform] ([!DNL Real-time CDP]) aide les spécialistes du marketing à rassembler les données de plusieurs systèmes d’entreprise, ce qui leur permet de mieux identifier, comprendre et impliquer leurs clients. Adobe considère la confidentialité des données des clients comme un principe de conception fondamental et fournit divers contrôles pour aider les spécialistes marketing à gérer la confidentialité des données de leurs clients.

La majorité des [!DNL Real-time CDP] sont alimentées par Adobe Experience Platform. Ce document fournit des informations sur les diverses technologies d&#39;amélioration de la vie privée prises en charge par [!DNL Real-time CDP], avec des liens vers [!DNL Experience Platform] pour plus d’informations.

## Respect des demandes d’accès et de suppression des clients

Réglementations juridiques relatives à la confidentialité, telles que [!DNL General Data Protection Regulation] (RGPD) et [!DNL California Consumer Privacy Act] (CCPA) donne aux clients le droit de demander l’accès aux données personnelles que vous leur collectez ou de les supprimer. Depuis [!DNL Real-time CDP] exploitation [!DNL Experience Platform] les capacités de collecte et de stockage des données, les demandes des clients d&#39;accès et de suppression de leurs données personnelles doivent être gérées dans [!DNL Platform]. Voir la présentation sur [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) pour plus d’informations.

>[!IMPORTANT]
>
> Les demandes de confidentialité soumises par l&#39;intermédiaire d&#39;Adobe Experience Platform Privacy Service pour Adobe Marketo Engage s&#39;appliquent uniquement aux clients CDP B2B en temps réel.

## Fonctionnalités d’exclusion

[!DNL Real-time CDP] permet aux clients de ne pas inclure leurs données personnelles dans les cas d’utilisation de la segmentation. Les préférences d’exclusion des clients sont capturées et stockées par [!DNL Real-time Customer Profile]et peut être appliqué en excluant les utilisateurs qui ont choisi de quitter un segment à l’aide de la logique booléenne (&quot;ET NON&quot;) dans le prédicat de segment.

Voir le document sur [traitement des demandes d’exclusion](../../segmentation/consents.md) pour plus d’informations, consultez la documentation du service de segmentation Adobe Experience Platform.

## Prise en charge de l’IAB TCF 2.0

[!DNL Real-time CDP] est construit sur Adobe Experience Platform, qui fait partie de l’enregistrement [liste des fournisseurs](https://iabeurope.eu/vendor-list-tcf-v2-0/) pour la [!DNL Transparency & Consent Framework (TCF)], comme indiqué par le [!DNL Interactive Advertising Bureau (IAB)]. Conformément aux exigences de TCF 2.0, Platform vous permet de collecter des données détaillées de consentement client et de les intégrer à vos profils clients stockés. Ces données de consentement peuvent ensuite être prises en compte pour déterminer si certains profils sont inclus dans les segments d’audience exportés, selon leur cas d’utilisation.

Voir la présentation sur [Prise en charge de l’IAB TCF 2.0 dans l’Experience Platform](../../landing/governance-privacy-security/consent/iab/overview.md) pour plus d’informations.

## Étapes suivantes

Ce document présente brièvement les capacités de protection de la vie privée des [!DNL Real-time CDP]. Pour plus d&#39;informations sur chaque fonctionnalité, veuillez consulter la documentation liée à tout ce guide.

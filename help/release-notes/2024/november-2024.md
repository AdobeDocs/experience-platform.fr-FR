---
title: Notes de mise à jour d’Adobe Experience Platform – Novembre 2024
description: Les notes de mise à jour de novembre 2024 pour Adobe Experience Platform.
source-git-commit: d87747c2181f4ae378e1341c3c190cc6fa57d4b0
workflow-type: tm+mt
source-wordcount: '854'
ht-degree: 25%

---

# Notes de mise à jour d’Adobe Experience Platform

>[!TIP]
>
>La nouvelle [page d’entrée de la documentation du produit de l’assistant d’IA](../../ai-assistant/landing.md) est désormais disponible. Utilisez cette page comme hub pour toutes les ressources liées aux assistants d’IA.

**Date de publication : mercredi 26 novembre 2024.**

Mises à jour des fonctionnalités et de la documentation existantes dans Adobe Experience Platform :

- [Assistant IA](#ai-assistant)
- [Destinations](#destinations)
- [Query Service](#query-service)
- [Sandbox](#sandboxes)
- [Mises à jour de la documentation](#documentation-updates)
   - [Documentation interactive de l’API Experience Platform](#interactive-experience-platform-api-documentation)
   - [Nouvelle table des matières sur l’Experience League](#new-table-of-contents-on-experience-league)
   - [Nouvelle page d’entrée des assistants IA](#new-ai-assistant-landing-page)

## Assistant IA {#ai-assistant}

L’assistant d’IA dans Adobe Experience Platform est une expérience conversationnelle que vous pouvez utiliser pour accélérer vos workflows dans les applications Adobe. Vous pouvez utiliser l’assistant d’IA pour mieux comprendre les connaissances sur les produits, résoudre les problèmes ou rechercher des informations et trouver des informations opérationnelles. L’assistant d’IA prend en charge Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer et Customer Journey Analytics.

**Nouvelles fonctionnalités**

| Fonctionnalité | Description |
| --- | --- |
| [!BADGE Alpha]{type=Informative} Surveiller les changements significatifs et prévoir la croissance de l’audience | Utilisez l’assistant d’IA pour surveiller les modifications importantes et fournir des prévisions de croissance pour votre audience et la taille de vos jeux de données. Vous pouvez ensuite utiliser ces informations pour garantir l’intégrité de vos données d’audience et proposer des projections prospectives à l’appui d’une prise de décision éclairée par les données. Pour plus d’informations, consultez le guide sur la [surveillance des changements significatifs et la prévision de la croissance de l’audience](../../ai-assistant/new-features/audience-forecasting.md). |
| [!BADGE Alpha]{type=Informative} Estimation du langage naturel | Utilisez les fonctionnalités d’estimation de langage naturel de l’assistant d’IA pour estimer la taille des audiences et prédire la propension des audiences en fonction de questions simples et conversationnelles. Pour plus d’informations, consultez le guide sur l’ [utilisation de l’estimation du langage naturel avec l’assistant d’IA](../../ai-assistant/new-features/natural-language.md). |

{style="table-layout:auto"}

## Destinations {#destinations}

Les [!DNL Destinations] sont des intégrations préconfigurées à des plateformes de destination qui permettent d’activer facilement des données provenant d’Adobe Experience Platform. Vous pouvez utiliser les destinations pour activer vos données connues et inconnues pour les campagnes marketing cross-canal, les campagnes par e-mail, la publicité ciblée et de nombreux autres cas d’utilisation.

**Fonctionnalités nouvelles ou mises à jour** {#new-updated-destinations}

| Destination | Description |
| --- | --- |
| [Temps réel de diffusion en continu Magnite](/help/destinations/catalog/advertising/magnite-streaming.md) | Exportez des audiences pour activation, ciblage ou suppression dans la plateforme de diffusion en continu Magnite. Notez que pour que les audiences soient correctement exportées vers Magnite, vous devez utiliser à la fois les destinations temps réel et par lot. |
| [Lot de diffusion en continu Magnite](/help/destinations/catalog/advertising/magnite-batch.md) | Exportez des audiences pour activation, ciblage ou suppression dans la plateforme de diffusion en continu Magnite. Notez que pour que les audiences soient correctement exportées vers Magnite, vous devez utiliser à la fois les destinations temps réel et par lot. |

{style="table-layout:auto"}

**Fonctionnalités nouvelles ou mises à jour** {#destinations-new-updated-functionality}

| Fonctionnalité | Description |
| --- | --- |
| [Recherche d’attributs de profil en temps réel sur la périphérie](/help/destinations/ui/activate-edge-profile-lookup.md) | Découvrez comment rechercher des attributs de profil de périphérie en temps réel pour offrir des expériences de personnalisation ou informer les règles de prise de décision par le biais d’applications en aval, à l’aide de la destination Personalization personnalisée et de l’API Edge Network. |

{style="table-layout:auto"}

Pour plus d’informations, reportez-vous à la [vue d’ensemble des destinations](../../destinations/home.md).

## Query Service {#query-service}

Requête de données dans le lac de données Adobe Experience Platform à l’aide de SQL standard avec Query Service. Combinez en toute transparence des jeux de données et générez de nouveaux jeux à partir des résultats de vos requêtes pour alimenter les rapports, activer les workflows de science des données ou faciliter l’ingestion dans Real-time Customer Profile. Vous pouvez, par exemple, fusionner les données de transaction client avec les données comportementales afin d’identifier les audiences à forte valeur ajoutée pour les campagnes marketing ciblées.

**Fonctionnalités mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| API Dater Distiller Authorization | Gérez et appliquez des restrictions d’accès basées sur les adresses IP pour les environnements de test de Query Service, afin d’améliorer la sécurité des données et de garantir la conformité aux stratégies organisationnelles. Pour plus d’informations sur ses principales fonctionnalités, reportez-vous au [guide de l’API d’autorisation de Data Distiller](../../query-service/auth-api/overview.md) ou à la [documentation d’OpenAPI](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/) pour obtenir des informations complètes, notamment des détails de point de terminaison, des listes de paramètres, des exemples de requête/réponse et des fonctionnalités de test. |

Pour plus d’informations sur Query Service [!DNL Query Service], consultez la [[!DNL Query Service] présentation](../../query-service/home.md) de Query Service.

## Sandbox {#sandboxes}

Adobe Experience Platform est conçu pour enrichir les applications d’expérience digitale à l’échelle mondiale. Les entreprises exécutent souvent plusieurs applications d’expérience digitale en parallèle et doivent prendre en charge le développement, les tests et le déploiement de ces applications tout en assurant la conformité opérationnelle. Pour répondre à ce besoin, Experience Platform fournit des sandbox qui divisent une instance de Platform unique en environnements virtuels distincts pour favoriser le développement et l’évolution d’applications d’expérience digitale.

**Fonctionnalités nouvelles ou mises à jour**

| Fonctionnalité | Description |
| --- | --- |
| Partage de modules avec l’API des outils Sandbox | Utilisez deux nouveaux points de terminaison API, [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) et [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages) pour gérer le partage de packages entre les organisations, tels que les approbations de demandes, la visibilité des packages et l’importation de packages, à l’aide de l’API de l’outil de test. |

Pour plus d’informations sur les sandbox, consultez la [vue d’ensemble des sandbox](../../sandboxes/home.md).

## Mises à jour de la documentation {#documentation-updates}

### Documentation interactive de l’API Experience Platform {#interactive-api-documentation}

La [ documentation de l’API Experience Platform](https://developer.adobe.com/experience-platform-apis/) est désormais entièrement interactive, ce qui vous permet d’authentifier et d’explorer les API directement sur la page de documentation de référence de l’API. Vous pouvez maintenant accéder à la page de documentation de référence de l’API souhaitée, créer ou obtenir vos informations d’authentification de l’API, les coller dans le bloc **[!UICONTROL Essayez-le]** et exécuter l’appel . Tout sur une page. [En savoir plus](/help/landing/api-authentication.md#get-credentials-functionality) sur la fonctionnalité.

### Nouvelle table des matières sur l’Experience League {#new-table-of-contents-on-experience-league}

La table des matières des pages de documentation Experience League a été améliorée afin de fournir une expérience améliorée aux lecteurs, notamment un filtre de mots-clés pour découvrir la page exacte dont vous avez besoin, la possibilité de développer toutes les pages, etc. <br> ![Nouvelle expérience de table des matières comprenant le filtre de mots-clés et la possibilité de développer toutes les pages.](../2024/assets/november/new-toc-experience.gif " Nouvelle expérience de table des matières comprenant le filtre de mots-clés et la possibilité de développer toutes les pages."){width="250" align="center" zoomable="yes"}

### Nouvelle page d’entrée des assistants IA {#new-ai-assistant-landing-page}

Utilisez la nouvelle page [Documentation du produit de l’assistant d’IA](../../ai-assistant/landing.md) comme hub pour tout ce qui est l’assistant d’IA. Reportez-vous à la documentation du produit pour consulter des tutoriels vidéo, de la documentation technique, des cas d’utilisation et des liens vers des publications de blog sur l’assistant d’IA.
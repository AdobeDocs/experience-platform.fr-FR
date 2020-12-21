---
keywords: data governance rtcdp;rtcdp data governance;real time customer data profile data governance
title: Présentation de la gouvernance des données
seo-title: Gouvernance des données sur la plateforme des données clients en temps réel
description: 'La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. '
seo-description: 'La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. '
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 40%

---


# [!DNL Data Governance] dans CDP en temps réel

[!DNL Real-time Customer Data Platform] (CDP en temps réel) rassemble les données de plusieurs systèmes d’entreprise, ce qui permet aux spécialistes du marketing de mieux identifier, comprendre et impliquer leurs clients. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que la plateforme des données clients en temps réel est conforme aux politiques d’utilisation lors de la gestion de vos données.

Adobe Experience Platform [!DNL Data Governance] vous permet de gérer les données client et de veiller au respect des réglementations, restrictions et stratégies applicables à l’utilisation des données. Elle joue un rôle essentiel dans la plateforme des données clients en temps réel, ce qui vous permet de définir des politiques d’utilisation, de classer vos données en fonction de ces politiques et de rechercher les violations de politiques lors de l’exécution de certaines actions marketing.

Le CDP en temps réel est construit sur Adobe Experience Platform et la majorité des capacités [!DNL Data Governance] sont donc couvertes dans la documentation [!DNL Experience Platform]. Ce document est destiné à compléter la [présentation de la gouvernance des données](../../data-governance/home.md) pour et décrit les fonctionnalités de gouvernance disponibles dans la plateforme des données clients en temps réel. [!DNL Experience Platform] Les sujets suivants sont abordés :

* [Application des libellés d’utilisation aux données](#labels)
* [Gestion des politiques d’utilisation des données](#policies)
* [Application de la conformité de l’utilisation des données](#enforce)

## Application des libellés d’utilisation aux données  {#labels}

[!DNL Data Governance] vous permet d’appliquer des étiquettes d’utilisation à vos données, soit au niveau du jeu de données, soit au niveau du champ de jeu de données. Les libellés d’utilisation des données vous permettent de classer les données en fonction des politiques d’utilisation qui s’appliquent à celles-ci.

Pour plus d’informations sur l’utilisation des libellés d’utilisation des données, consultez le [Guide de l’utilisateur des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour Adobe Experience Platform.

## Configurer des cas d&#39;utilisation marketing pour les destinations {#destinations}

Vous pouvez définir des restrictions d’utilisation des données sur une destination en définissant des cas d’utilisation marketing (également appelés actions marketing) pour cette destination. Un cas d’utilisation marketing pour une destination indique l’intention des données qui seront exportées vers cette destination.

>[!NOTE]
>
>Pour plus d&#39;informations sur les actions marketing et leur utilisation dans les stratégies d&#39;utilisation des données, consultez la [présentation des stratégies d&#39;utilisation des données](../../data-governance/policies/overview.md) dans la documentation [!DNL Experience Platform].

La définition de cas d’utilisation marketing sur les destinations vous permet de vous assurer que les profils ou segments envoyés vers ces destinations sont conformes aux stratégies d’utilisation des données. Par conséquent, vous devez ajouter des cas d’utilisation marketing appropriés à vos destinations en fonction des besoins de votre entreprise pour appliquer des restrictions de stratégie à l’activation.

Les cas d’utilisation marketing ne peuvent être sélectionnés que lors de la configuration d’une destination pour la première fois. Selon le type de destination que vous utilisez, la possibilité de configurer des cas d’utilisation marketing s’affiche à différents moments du processus de configuration. Consultez la [documentation relative aux destinations](../destinations/overview.md) pour savoir comment configurer votre destination particulière.

## Gestion des politiques d’utilisation des données   {#policies}

Les politiques d’utilisation des données doivent être définies et activées pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé, ou non, à effectuer sur des données de la plateforme des données clients en temps réel. Pour plus d&#39;informations, consultez la section &quot;Stratégies d&#39;utilisation des données&quot; dans [!DNL Experience Platform] [Présentation de la gouvernance des données](../../data-governance/home.md).

Adobe Experience Platform propose plusieurs politiques fondamentales pour les cas d’utilisation courants de l’expérience client. Vous pouvez afficher ces stratégies dans l’interface utilisateur en accédant à l’espace de travail **[!UICONTROL Stratégies]** et en sélectionnant l’onglet **[!UICONTROL Parcourir]**. Consultez le [guide de l’utilisateur des stratégies](../../data-governance/policies/user-guide.md) dans la documentation [!DNL Experience Platform] pour obtenir des instructions plus détaillées sur l’utilisation des stratégies dans l’interface utilisateur, y compris sur la manière de créer vos propres stratégies personnalisées.

## Application de la conformité de l’utilisation des données {#enforce}

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez appliquer les stratégies d’utilisation des données. Lors de l’activation de segments d’audience vers des destinations dans le CDP en temps réel, [!DNL Data Governance] applique automatiquement les stratégies d’utilisation en cas de violation.

Pour plus d&#39;informations, consultez le document sur [l&#39;application automatique de la stratégie](../../data-governance/enforcement/auto-enforcement.md).

## Étapes suivantes

Maintenant que vous avez découvert les fonctionnalités [!DNL Data Governance] clés du CDP en temps réel et comment [!DNL Experience Platform] les active, consultez la [documentation relative à la gouvernance des données sur Adobe Experience Platform](../../data-governance/home.md). La documentation fournit des aperçus des concepts [!DNL Data Governance] essentiels ainsi que des workflows détaillés pour la gestion des étiquettes et des stratégies d&#39;utilisation des données.

La vidéo suivante présente un aperçu de [!DNL Data Governance] dans le CDP en temps réel, y compris l&#39;utilisation de cas d&#39;utilisation marketing sur les destinations et des exemples de workflows pour différents scénarios :

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)
---
keywords: gouvernance des données rtcdp;gouvernance des données rtcdp;gouvernance des données de profil client en temps réel
title: Présentation de la gouvernance des données
seo-title: Data Governance in Real-time Customer Data Platform
description: 'La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. '
seo-description: Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 0085306a2f5172eb19590cc12bc9645278bd2b42
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 41%

---

# [!DNL Data Governance] dans la plateforme de données clients en temps réel

[!DNL Real-time Customer Data Platform] (CDP en temps réel) rassemble des données issues de plusieurs systèmes d’entreprise, ce qui permet aux marketeurs de mieux identifier, comprendre et impliquer leurs clients. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que la plateforme des données clients en temps réel est conforme aux politiques d’utilisation lors de la gestion de vos données.

Adobe Experience Platform [!DNL Data Governance] vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Elle joue un rôle essentiel dans la plateforme des données clients en temps réel, ce qui vous permet de définir des politiques d’utilisation, de classer vos données en fonction de ces politiques et de rechercher les violations de politiques lors de l’exécution de certaines actions marketing.

La plateforme de données clients en temps réel repose sur Adobe Experience Platform. Par conséquent, la majorité des fonctionnalités [!DNL Data Governance] sont abordées dans la documentation [!DNL Experience Platform]. Ce document est destiné à compléter la [présentation de la gouvernance des données](../../data-governance/home.md) pour et décrit les fonctionnalités de gouvernance disponibles dans la plateforme des données clients en temps réel. [!DNL Experience Platform] Les sujets suivants sont abordés :

* [Application des libellés d’utilisation aux données ](#labels)
* [Gestion des politiques d’utilisation des données ](#policies)
* [Appliquer des stratégies d’utilisation des données](#enforce)

## Application des libellés d’utilisation aux données  {#labels}

[!DNL Data Governance] vous permet d’appliquer des libellés d’utilisation à vos données, au niveau du jeu de données ou du champ du jeu de données. Les libellés d’utilisation des données vous permettent de classer les données en fonction des politiques d’utilisation qui s’appliquent à celles-ci.

Pour plus d’informations sur l’utilisation des libellés d’utilisation des données, consultez le [Guide de l’utilisateur des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour Adobe Experience Platform.

## Configuration des actions marketing pour les destinations {#destinations}

Vous pouvez définir des restrictions d’utilisation des données sur une destination en définissant des actions marketing (également appelées cas d’utilisation marketing) pour cette destination. Une action marketing pour une destination indique l’intention des données qui seront exportées vers cette destination.

>[!NOTE]
>
>Pour plus d’informations sur les actions marketing et leur utilisation dans les stratégies d’utilisation des données, consultez la [présentation des stratégies d’utilisation des données](../../data-governance/policies/overview.md) dans la documentation [!DNL Experience Platform].

La définition d’actions marketing sur les destinations vous permet de vous assurer que les profils ou segments envoyés vers ces destinations sont conformes aux politiques d’utilisation des données. Vous devez donc ajouter des actions marketing appropriées à vos destinations en fonction des besoins de votre entreprise pour appliquer des restrictions de stratégie à l’activation.

Les actions marketing ne peuvent être sélectionnées que lors de la configuration d’une destination pour la première fois. Selon le type de destination que vous utilisez, la possibilité de configurer des actions marketing s’affiche à différents points du workflow de configuration. Consultez la [documentation sur les destinations](../destinations/overview.md) pour savoir comment configurer votre destination particulière.

## Gestion des politiques d’utilisation des données {#policies}

Les politiques d’utilisation des données doivent être définies et activées pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé, ou non, à effectuer sur des données de la plateforme des données clients en temps réel. Pour plus d’informations, consultez la section &quot;Politiques d’utilisation des données&quot; dans la [!DNL Experience Platform] [Présentation de la gouvernance des données](../../data-governance/home.md).

Adobe Experience Platform propose plusieurs politiques fondamentales pour les cas d’utilisation courants de l’expérience client. Vous pouvez afficher ces stratégies dans l’interface utilisateur en accédant à l’espace de travail **[!UICONTROL Stratégies]** et en sélectionnant l’onglet **[!UICONTROL Parcourir]** . Pour obtenir des instructions plus détaillées sur l’utilisation des stratégies dans l’interface utilisateur, notamment sur la création de vos propres stratégies personnalisées, consultez le [guide d’utilisation des stratégies](../../data-governance/policies/user-guide.md) dans la documentation [!DNL Experience Platform] .

## Appliquer des stratégies d’utilisation des données {#enforce}

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez appliquer les stratégies d’utilisation des données. Lors de l’activation des segments d’audience vers des destinations dans la plateforme de données clients en temps réel, [!DNL Data Governance] applique automatiquement les stratégies d’utilisation en cas de violation.

Pour plus d’informations, voir le document [application automatique des stratégies](../../data-governance/enforcement/auto-enforcement.md) .

## Étapes suivantes

Maintenant que vous avez découvert les fonctionnalités [!DNL Data Governance] clés de la plateforme de données clients en temps réel et la manière dont [!DNL Experience Platform] les active, consultez la [documentation sur la gouvernance des données dans Adobe Experience Platform](../../data-governance/home.md). La documentation présente les concepts [!DNL Data Governance] essentiels, ainsi que les processus détaillés de gestion des libellés et des stratégies d’utilisation des données.

La vidéo suivante présente un aperçu de [!DNL Data Governance] dans la plateforme de données clients en temps réel, y compris l’utilisation de cas d’utilisation marketing sur les destinations et d’exemples de processus pour différents scénarios :

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)

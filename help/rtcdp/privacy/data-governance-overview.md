---
keywords: gouvernance des données rtcdp;gouvernance des données rtcdp;gouvernance des données de profil client en temps réel
title: Présentation de la gouvernance des données
seo-title: Data Governance in Real-time Customer Data Platform
description: 'La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. '
seo-description: Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use.
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 49%

---

# Gouvernance des données sur la plateforme des données clients en temps réel

[!DNL Real-time Customer Data Platform] (CDP en temps réel) rassemble des données issues de plusieurs systèmes d’entreprise, ce qui permet aux marketeurs de mieux identifier, comprendre et impliquer leurs clients. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que la plateforme des données clients en temps réel est conforme aux politiques d’utilisation lors de la gestion de vos données.

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux stratégies applicables à l’utilisation des données. Elle joue un rôle essentiel dans la plateforme des données clients en temps réel, ce qui vous permet de définir des politiques d’utilisation, de classer vos données en fonction de ces politiques et de rechercher les violations de politiques lors de l’exécution de certaines actions marketing.

La plateforme des données clients en temps réel repose sur Adobe Experience Platform. Par conséquent, la plupart des fonctionnalités de gouvernance des données sont abordées dans la section [!DNL Experience Platform] documentation. Ce document est destiné à compléter la [présentation de la gouvernance des données](../../data-governance/home.md) pour et décrit les fonctionnalités de gouvernance disponibles dans la plateforme des données clients en temps réel. [!DNL Experience Platform] Les sujets suivants sont abordés :

* [Application des libellés d’utilisation aux données ](#labels)
* [Gestion des politiques d’utilisation des données ](#policies)
* [Appliquer des stratégies d’utilisation des données](#enforce)

## Application des libellés d’utilisation aux données {#labels}

La gouvernance des données vous permet d’appliquer des libellés d’utilisation aux données, soit au niveau du jeu de données, soit au niveau du champ du jeu de données. Les libellés d’utilisation des données vous permettent de classer les données en fonction des politiques d’utilisation qui s’appliquent à celles-ci.

Pour plus d’informations sur l’utilisation des libellés d’utilisation des données, consultez le [Guide de l’utilisateur des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour Adobe Experience Platform.

## Configuration des actions marketing pour les destinations {#destinations}

Vous pouvez définir des restrictions d’utilisation des données sur une destination en définissant des actions marketing (également appelées cas d’utilisation marketing) pour cette destination. Une action marketing pour une destination indique l’intention des données qui seront exportées vers cette destination.

>[!NOTE]
>
>Pour plus d’informations sur les actions marketing et leur utilisation dans les stratégies d’utilisation des données, voir [présentation des stratégies d’utilisation des données](../../data-governance/policies/overview.md) dans le [!DNL Experience Platform] documentation.

La définition d’actions marketing sur les destinations vous permet de vous assurer que les profils ou segments envoyés vers ces destinations sont conformes aux politiques d’utilisation des données. Vous devez donc ajouter des actions marketing appropriées à vos destinations en fonction des besoins de votre entreprise pour appliquer des restrictions de stratégie à l’activation.

Les actions marketing ne peuvent être sélectionnées que lors de la configuration d’une destination pour la première fois. Selon le type de destination que vous utilisez, la possibilité de configurer des actions marketing s’affiche à différents points du workflow de configuration. Voir [documentation sur les destinations](../destinations/overview.md) pour savoir comment configurer votre destination spécifique.

## Gestion des politiques d’utilisation des données {#policies}

Les politiques d’utilisation des données doivent être définies et activées pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé, ou non, à effectuer sur des données de la plateforme des données clients en temps réel. Voir la section &quot;Stratégies d’utilisation des données&quot; dans la section [!DNL Experience Platform] [Présentation de la gouvernance des données](../../data-governance/home.md) pour plus d’informations.

Adobe Experience Platform propose plusieurs politiques fondamentales pour les cas d’utilisation courants de l’expérience client. Ces stratégies peuvent être visualisées dans l’interface utilisateur en accédant à la variable **[!UICONTROL Stratégies]** l’espace de travail et en sélectionnant **[!UICONTROL Parcourir]** . Voir [guide d’utilisation des stratégies](../../data-governance/policies/user-guide.md) dans le [!DNL Experience Platform] documentation pour obtenir des instructions plus détaillées sur l’utilisation des stratégies dans l’interface utilisateur, y compris sur la création de vos propres stratégies personnalisées.

## Appliquer des stratégies d’utilisation des données {#enforce}

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez appliquer les stratégies d’utilisation des données. Lors de l’activation des segments d’audience vers des destinations dans la plateforme des données clients en temps réel, la gouvernance des données applique automatiquement les politiques d’utilisation en cas de violation.

Consultez le document sur [application automatique des stratégies](../../data-governance/enforcement/auto-enforcement.md) pour plus d’informations.

## Étapes suivantes

Maintenant que vous avez découvert les fonctionnalités clés de gouvernance des données sur la plateforme de données clients en temps réel et comment [!DNL Experience Platform] les active, veuillez continuer à [Documentation sur la gouvernance des données sur Adobe Experience Platform](../../data-governance/home.md). Cette documentation présente les principaux concepts de la gouvernance des données, ainsi que les processus détaillés de gestion des libellés et des politiques d’utilisation des données.

La vidéo suivante présente un aperçu de la gouvernance des données dans la plateforme des données clients en temps réel, y compris l’utilisation de cas d’utilisation marketing sur les destinations et d’exemples de processus pour différents scénarios :

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)

---
keywords: gouvernance des données rtcdp;gouvernance des données rtcdp;gouvernance des données de profil client en temps réel
title: Présentation de la gouvernance des données
description: La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 30%

---

# Gouvernance des données dans Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) rassemble des données provenant de plusieurs systèmes d’entreprise, ce qui permet aux marketeurs de mieux identifier, comprendre et impliquer leurs clients. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que Real-Time CDP est conforme aux politiques d’utilisation lors de la gestion de vos données.

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Il joue un rôle clé dans Real-Time CDP. Il vous permet de définir des stratégies d’utilisation, de classer vos données en fonction de ces stratégies et de rechercher les violations de stratégie lors de l’exécution de certaines actions marketing.

Real-Time CDP repose sur Adobe Experience Platform. Par conséquent, la plupart des fonctionnalités de gouvernance des données sont abordées dans la documentation [!DNL Experience Platform]. Ce document est destiné à compléter la [présentation de la gouvernance des données](../../data-governance/home.md) pour [!DNL Experience Platform] et décrit les fonctionnalités de gouvernance disponibles dans Real-Time CDP. Les sujets suivants sont abordés :

* [Application des libellés d’utilisation aux données &#x200B;](#labels)
* [Gestion des politiques d’utilisation des données &#x200B;](#policies)
* [Appliquer des stratégies d’utilisation des données](#enforce)

## Application des libellés d’utilisation aux données {#labels}

La gouvernance des données vous permet d’appliquer des libellés d’utilisation aux données, soit au niveau du jeu de données, soit au niveau du champ du jeu de données. Les libellés d’utilisation des données vous permettent de classer les données en fonction des politiques d’utilisation qui s’appliquent à celles-ci.

Pour plus d’informations sur l’utilisation des étiquettes d’utilisation des données, consultez le [Guide de l’utilisateur des étiquettes d’utilisation des données](../../data-governance/labels/overview.md) pour Adobe Experience Platform.

## Configuration des actions marketing pour les destinations {#destinations}

Vous pouvez définir des restrictions d’utilisation des données sur une destination en définissant des actions marketing (également appelées cas d’utilisation marketing) pour cette destination. Une action marketing pour une destination indique l’intention des données qui seront exportées vers cette destination.

>[!NOTE]
>
>Pour plus d’informations sur les actions marketing et leur utilisation dans les stratégies d’utilisation des données, consultez la [présentation des stratégies d’utilisation des données](../../data-governance/policies/overview.md) dans la documentation [!DNL Experience Platform].

La définition d’actions marketing sur les destinations vous permet de vous assurer que les profils ou les audiences envoyés vers ces destinations sont conformes aux politiques d’utilisation des données. Vous devez donc ajouter des actions marketing appropriées à vos destinations en fonction des besoins de votre entreprise pour appliquer des restrictions de stratégie à l’activation.

Les actions marketing ne peuvent être sélectionnées que lors de la configuration d’une destination pour la première fois. Selon le type de destination que vous utilisez, la possibilité de configurer des actions marketing s’affiche à différents points du workflow de configuration. Consultez la [documentation sur les destinations](../destinations/overview.md) pour savoir comment configurer votre destination particulière.

## Gestion des politiques d’utilisation des données {#policies}

Les politiques d’utilisation des données doivent être définies et activées pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les stratégies d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur les données de Real-Time CDP. Pour plus d’informations, consultez la section &quot;Politiques d’utilisation des données&quot; dans la [!DNL Experience Platform] [Présentation de la gouvernance des données](../../data-governance/home.md) .

Adobe Experience Platform fournit plusieurs stratégies de base pour les cas d’utilisation courants de l’expérience client. Ces stratégies peuvent être visualisées dans l’interface utilisateur en accédant à l’espace de travail **[!UICONTROL Stratégies]** et en sélectionnant l’onglet **[!UICONTROL Parcourir]** . Pour obtenir des instructions plus détaillées sur l’utilisation des stratégies dans l’interface utilisateur, y compris sur la création de vos propres stratégies personnalisées, consultez le [guide d’utilisation des stratégies](../../data-governance/policies/user-guide.md) dans la documentation [!DNL Experience Platform] .

## Appliquer des stratégies d’utilisation des données {#enforce}

Une fois que les données sont étiquetées et que les politiques d’utilisation sont définies, vous pouvez appliquer les politiques d’utilisation des données. Lors de l’activation d’audiences vers des destinations dans Real-Time CDP, la gouvernance des données applique automatiquement les stratégies d’utilisation en cas de violation.

Pour plus d’informations, consultez le document sur l’ [application automatique de la stratégie](../../data-governance/enforcement/auto-enforcement.md) .

## Étapes suivantes

Maintenant que vous avez découvert les fonctionnalités clés de gouvernance des données sur Real-Time CDP et que [!DNL Experience Platform] les active, reportez-vous à la [documentation sur la gouvernance des données sur Adobe Experience Platform](../../data-governance/home.md). Cette documentation présente les principaux concepts de la gouvernance des données, ainsi que les processus détaillés de gestion des libellés et des politiques d’utilisation des données.

La vidéo suivante présente un aperçu de la gouvernance des données dans Real-Time CDP, y compris l’utilisation de cas d’utilisation marketing sur les destinations et d’exemples de processus pour différents scénarios :

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)

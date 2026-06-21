---
keywords: gouvernance des données rtcdp;gouvernance des données rtcdp;gouvernance des données profil client en temps réel
title: Présentation de la gouvernance des données
description: La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données.
feature: Get Started, Data Governance
exl-id: eb501d85-cabd-4667-a1cd-2210ec83fb71
TQID: https://experienceleague.adobe.com/N4ACtqYycPiJntA0uAwVTnKSg4hpxkjIgNy-m-85da8
product_v2:
  - id: fdddec33-c9cb-4459-b8b6-2664395a6f10
feature_v2:
  - id: ba929a52-9339-4154-9487-317dc875a3c7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 7d565f9c521069c68836119ed6f991dc9eab4def
workflow-type: tm+mt
source-wordcount: 703
ht-degree: 30%

---

# Gouvernance des données dans Real-Time CDP

[!DNL Adobe Real-Time Customer Data Platform] (Real-Time CDP) rassemble des données issues de plusieurs systèmes d’entreprise, ce qui permet aux professionnels du marketing de mieux identifier, comprendre et interagir avec leurs clients. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Par conséquent, il est important de s’assurer que Real-Time CDP respecte les politiques d’utilisation lors de la gestion de vos données.

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Il joue un rôle essentiel dans Real-Time CDP. Il vous permet de définir des politiques d’utilisation, de classer vos données en fonction de ces politiques et de vérifier les violations de politique lors de l’exécution de certaines actions marketing.

Real-Time CDP repose sur Adobe Experience Platform. La plupart des fonctionnalités de gouvernance des données sont donc abordées dans la documentation [!DNL Experience Platform]. Ce document est destiné à compléter la [présentation de la gouvernance des données](../../data-governance/home.md) par [!DNL Experience Platform] et décrit les fonctionnalités de gouvernance disponibles dans Real-Time CDP. Les sujets suivants sont abordés :

* [Application des libellés d’utilisation aux données](#labels)
* [Gestion des politiques d’utilisation des données](#policies)
* [Appliquer des stratégies d’utilisation des données](#enforce)

## Application des libellés d’utilisation aux données {#labels}

La gouvernance des données vous permet d’appliquer des libellés d’utilisation aux données, soit au niveau du jeu de données, soit au niveau du champ du jeu de données. Les libellés d’utilisation des données vous permettent de classer les données en fonction des politiques d’utilisation qui s’appliquent à celles-ci.

Pour plus d’informations sur l’utilisation des libellés d’utilisation des données, consultez le [Guide d’utilisation des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour Adobe Experience Platform.

## Configuration des actions marketing pour les destinations {#destinations}

Vous pouvez définir des restrictions d’utilisation des données sur une destination en définissant des actions marketing (également appelées cas d’utilisation marketing) pour cette destination. Une action marketing pour une destination indique l’intention des données qui seront exportées vers cette destination.

>[!NOTE]
>
>Pour plus d’informations sur les actions marketing et leur utilisation dans les politiques d’utilisation des données, consultez la [&#x200B; présentation des politiques d’utilisation des données &#x200B;](../../data-governance/policies/overview.md) dans la documentation de [!DNL Experience Platform].

La définition d’actions marketing sur les destinations vous permet de vous assurer que tous les profils ou audiences envoyés vers ces destinations sont conformes aux politiques d’utilisation des données. Vous devez donc ajouter des actions marketing appropriées à vos destinations en fonction des besoins de votre organisation pour appliquer des restrictions de politique sur l’activation.

Les actions marketing ne peuvent être sélectionnées que lors de la première configuration d’une destination. Selon le type de destination que vous utilisez, l’opportunité de configurer des actions marketing s’affiche à différents points du workflow de configuration. Consultez la [documentation sur les destinations](../destinations/overview.md) pour savoir comment configurer une destination spécifique.

## Gestion des politiques d’utilisation des données {#policies}

Les politiques d’utilisation des données doivent être définies et activées pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé ou non à effectuer sur des données dans Real-Time CDP. Pour plus d’informations, consultez la section « Politiques d’utilisation des données » dans la [!DNL Experience Platform] [présentation de la gouvernance des données](../../data-governance/home.md).

Adobe Experience Platform fournit plusieurs politiques de base pour les cas d’utilisation courants de l’expérience client. Il est possible d’afficher ces politiques dans l’interface utilisateur en accédant à l’espace de travail **[!UICONTROL Politiques]** et en sélectionnant l’onglet **[!UICONTROL Parcourir]**. Consultez le [guide d’utilisation des politiques](../../data-governance/policies/user-guide.md) dans la documentation [!DNL Experience Platform] pour obtenir des instructions plus détaillées sur l’utilisation des politiques dans l’interface utilisateur, notamment sur la création de vos propres politiques personnalisées.

## Appliquer des stratégies d’utilisation des données {#enforce}

Une fois que les données sont étiquetées et que les politiques d’utilisation sont définies, vous pouvez appliquer les politiques d’utilisation des données. Lors de l’activation des audiences vers les destinations dans Real-Time CDP, la gouvernance des données applique automatiquement les politiques d’utilisation en cas de violation.

Pour plus d’informations, consultez le document sur l’[application automatique des politiques](../../data-governance/enforcement/auto-enforcement.md).

## Étapes suivantes

Maintenant que vous avez découvert les principales fonctionnalités de gouvernance des données sur Real-Time CDP et la manière dont [!DNL Experience Platform] les active, reportez-vous à la documentation [&#x200B; relative à la gouvernance des données sur Adobe Experience Platform](../../data-governance/home.md). Cette documentation présente les principaux concepts de la gouvernance des données, ainsi que les processus détaillés de gestion des libellés et des politiques d’utilisation des données.

La vidéo suivante présente un aperçu de la gouvernance des données dans Real-Time CDP, y compris l’utilisation de cas d’utilisation marketing sur les destinations et d’exemples de workflows pour différents scénarios :

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)

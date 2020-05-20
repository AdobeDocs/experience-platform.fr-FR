---
title: Présentation de la gouvernance des données
seo-title: Gouvernance des données sur la plateforme des données clients en temps réel
description: 'La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. '
seo-description: 'La gouvernance des données vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. '
translation-type: tm+mt
source-git-commit: e21cf6794e6c9ee522482cd9ccb95d66b06d330a
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 100%

---


# Gouvernance des données sur la plateforme des données clients en temps réel

La plateforme des données clients en temps réel rassemble les données de plusieurs systèmes d’entreprise, ce qui permet aux marketeurs de mieux identifier leurs clients, de les comprendre et d’interagir avec eux. Ces données peuvent être soumises à des restrictions d’utilisation définies par votre organisation ou par des réglementations juridiques. Il est donc important de s’assurer que la plateforme des données clients en temps réel est conforme aux politiques d’utilisation lors de la gestion de vos données.

La gouvernance des données dans Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle essentiel dans la plateforme des données clients en temps réel, ce qui vous permet de définir des politiques d’utilisation, de classer vos données en fonction de ces politiques et de rechercher les violations de politiques lors de l’exécution de certaines actions marketing.

La plateforme des données clients en temps réel repose sur Adobe Experience Platform. La plupart des fonctionnalités de gouvernance des données sont donc abordées dans la documentation d’Experience Platform. Ce document est destiné à compléter la [présentation de la gouvernance des données](../../data-governance/home.md) pour Experience Platform et décrit les fonctionnalités de gouvernance disponibles dans la plateforme des données clients en temps réel. Les sujets suivants sont abordés :

* [Application des libellés d’utilisation aux données](#labels)
* [Gestion des politiques d’utilisation des données](#policies)
* [Application de la conformité de l’utilisation des données](#enforcement)

## Application des libellés d’utilisation aux données {#labels}

La gouvernance des données vous permet d’appliquer des libellés d’utilisation aux données, soit au niveau du jeu de données, soit au niveau du champ du jeu de données. Les libellés d’utilisation des données vous permettent de classer les données en fonction des politiques d’utilisation qui s’appliquent à celles-ci.

Pour plus d’informations sur l’utilisation des libellés d’utilisation des données, consultez le [Guide de l’utilisateur des libellés d’utilisation des données](../../data-governance/labels/overview.md) pour Adobe Experience Platform.

## Définition de restrictions sur les destinations

Vous pouvez définir des restrictions d’utilisation des données sur une destination en définissant des cas d’utilisation marketing pour cette destination. La définition de cas d’utilisation pour les destinations vous permet de rechercher des violations de la politique d’utilisation et de vous assurer que les profils ou segments envoyés vers cette destination sont compatibles avec les règles de gouvernance des données.

Les cas d’utilisation marketing peuvent être définis pendant la phase de _configuration_ pour le processus _Modifier la destination_. Pour plus d’informations, consultez la documentation sur les destinations.


## Gestion des politiques d’utilisation des données {#policies}

Les politiques d’utilisation des données doivent être définies et activées pour que les libellés d’utilisation des données prennent en charge efficacement la conformité des données. Les politiques d’utilisation des données sont des règles qui décrivent les types d’actions marketing que vous êtes autorisé, ou non, à effectuer sur des données de la plateforme des données clients en temps réel. Pour plus d’informations, consultez la section « Politiques d’utilisation des données » dans la [présentation de la gouvernance des données](../../data-governance/home.md) d’Experience Platform.

Adobe Experience Platform propose plusieurs **politiques fondamentales** pour les cas d’utilisation courants de l’expérience client. Il est possible de consulter ces politiques en adressant une requête à l’[API DULE Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml), comme illustré dans la section « Répertorier toutes les politiques » du [Guide du développeur de Policy Service](../../data-governance/policies/overview.md). Vous pouvez également créer vos propres **politiques personnalisées** pour modéliser des restrictions d’utilisation personnalisées, comme illustré dans la section « Créer une politique » du guide du développeur.

## (Version bêta) Application de la conformité de l’utilisation des données {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Cette fonctionnalité est actuellement en version bêta et n’est pas disponible pour tous les utilisateurs. Elle peut être activée sur demande. La documentation et les fonctionnalités peuvent changer.

Une fois que les données sont étiquetées et que les stratégies d’utilisation sont définies, vous pouvez appliquer les stratégies d’utilisation des données. Lors de l’activation des segments d’audience vers des destinations dans la plateforme des données clients en temps réel, la gouvernance des données applique automatiquement les politiques d’utilisation en cas de violation.

Le diagramme suivant illustre la procédure d’intégration des politiques dans le flux de données de l’activation des segments :

![](assets/enforcement-flow.png)

Lorsqu’un segment est activé pour la première fois, DULE Policy Service vérifie les violations de politique en fonction des facteurs suivants :

* Les libellés d’utilisation des données ont été appliquées aux champs et aux jeux de données du segment à activer.
* Objectif marketing de la destination.

### Messages de violation de politique {#enforcement}

Si une violation de politique se produit lors de la tentative d’activation d’un segment (ou de la [modification d’un segment déjà activé](#policy-enforcement-for-activated-segments)), l’action est bloquée et une fenêtre contextuelle s’affiche indiquant qu’une ou plusieurs politiques ont été violées. Sélectionnez une violation de politique dans la colonne de gauche de la fenêtre contextuelle pour afficher les détails de celle-ci.

![](assets/violation-popover.png)

L’onglet *Détails* de la fenêtre contextuelle indique l’action qui a déclenché la violation, la raison pour laquelle la violation s’est produite et fournit des suggestions pour résoudre le problème.

Cliquez sur **Liaison des données** pour effectuer le suivi des destinations, des segments, des politiques de fusion ou des jeux de données dont le ou les libellés de données ont déclenché la violation.

![](assets/data-lineage.png)

Une fois qu’une violation a été déclenchée, le bouton **Enregistrer** est désactivé pour l’activation jusqu’à ce que les composants appropriés soient mis à jour pour se conformer aux politiques d’utilisation des données.

### Application des politiques pour les segments activés {#policy-enforcement-for-activated-segments}

L’application de la politique s’applique toujours aux segments une fois qu’ils ont été activés, ce qui limite toute modification apportée à un segment ou à sa destination qui entraînerait une violation de la politique. En raison des nombreux composants impliqués dans l’activation des segments vers les destinations, l’une des actions suivantes peut potentiellement déclencher une violation :

* Mise à jour des libellés d’utilisation des données
* Modification des jeux de données d’un segment
* Modification des prédicats de segment
* Modification des configurations de destination

Si l’une des actions ci-dessus déclenche une violation, l’enregistrement de cette action est bloquée et un message de violation de politique s’affiche, ce qui vous permet de vérifier que les segments que vous avez activés continuent à respecter les politiques d’utilisation des données lors de leur modification.

## Étapes suivantes

Maintenant que vous avez découvert les principales fonctionnalités de gouvernance des données sur la plateforme des données clients en temps réel et la méthode utilisée par Experience Platform pour les activer, reportez-vous à la [documentation sur la gouvernance des données sur Adobe Experience Platform](../../data-governance/home.md). Cette documentation présente les principaux concepts de la gouvernance des données, ainsi que les processus détaillés de gestion des libellés et des politiques d’utilisation des données.
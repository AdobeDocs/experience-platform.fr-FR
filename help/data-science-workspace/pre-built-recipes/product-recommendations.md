---
keywords: Experience Platform;recette de recommandation de produit;Data Science Workspace;rubriques populaires;recettes;recette de précréation
solution: Experience Platform
title: Recette des recommandations de produits
description: La recette des recommandations de produits vous permet d’apporter à vos clients des recommandations de produits personnalisées et adaptées à leurs besoins et à leurs intérêts. Grâce à une modélisation prédictive précise, l’historique des achats d’un client peut vous fournir des informations sur les produits susceptibles de l’intéresser.
exl-id: 508d55af-c33b-4f1d-b1b6-f00ed5d12bf9
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 90%

---

# Recette des recommandations de produits

La recette des recommandations de produits vous permet d’apporter à vos clients des recommandations de produits personnalisées et adaptées à leurs besoins et à leurs intérêts. Grâce à une modélisation prédictive précise, l’historique des achats d’un client peut vous fournir des informations sur les produits susceptibles de l’intéresser.

## Pour qui cette recette a-t-elle été créée ?

De nos jours, un détaillant peut proposer à ses clients un large choix de produits, ce qui peut s’avérer être une gêne pour leurs recherches. En raison des contraintes de temps et d’effort, les clients peuvent ne pas trouver le produit qu’ils désirent, ce qui se traduit par des achats avec un niveau élevé de dissonance cognitive ou par aucun achat du tout.

## Comment fonctionne cette recette ?

La recette des recommandations de produits utilise le machine learning pour analyser les interactions d’un client avec des produits dans le passé et générer une liste personnalisée de recommandations de produits rapidement et sans effort. Cela optimise le processus de découverte de produits et évite à vos clients des recherches longues, improductives et hors sujet. En conséquence, la recette des recommandations de produits peut améliorer l’expérience d’achat globale d’un client, ce qui entraîne un engagement plus important et une plus grande fidélité à la marque.

## Démarrage

Pour commencer, suivez le tutoriel de l’atelier d’Adobe Experience Platform (voir le lien vers l’atelier ci-dessous). Ce tutoriel vous explique comment créer la recette Recommendations de produit dans un notebook Jupyter en suivant le workflow [notebook vers recette](../jupyterlab/create-a-model.md) et en implémentant la recette dans [!DNL Experience Platform] [!DNL Data Science Workspace].

* [Atelier : Prédire l’avenir avec l’espace de travail de science des données](https://expleague.azureedge.net/labs/L777/index.html)
* [Ressources de l’atelier](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Schéma des données

Cette recette utilise des schémas [XDM](../../xdm/schema/field-dictionary.md) personnalisés pour modéliser les données d’entrée et de sortie :

### Schéma des données d’entrée

| Nom du champ | Type |
| --- | --- |
| itemId | Chaîne |
| interactionType | Chaîne |
| timestamp | Chaîne |
| userId | Chaîne |

### Schéma des données de sortie

| Nom du champ | Type |
| --- | --- |
| recommendations | Chaîne |
| userId | Entier |

## Algorithme

La recette des recommandations de produits utilise le filtrage collaboratif pour générer une liste personnalisée de recommandations de produits pour vos clients. Contrairement à une approche basée sur le contenu, le filtrage collaboratif ne nécessite pas d’informations sur un produit spécifique, mais utilise plutôt les préférences historiques d’un client sur un ensemble de produits. Cette puissante technique de recommandation repose sur deux hypothèses simples :
* Il existe des clients ayant des intérêts similaires et ils peuvent être regroupés en comparant leurs comportements d’achat et de navigation.
* Un client est plus susceptible d’être intéressé par une recommandation basée sur des clients similaires en termes de comportement d’achat et de navigation.

Ce processus est divisé en deux étapes principales. Tout d’abord, il faut définir un sous-ensemble de clients similaires. Puis, dans ce jeu, identifier des fonctionnalités similaires parmi ces clients afin de renvoyer une recommandation pour le client.

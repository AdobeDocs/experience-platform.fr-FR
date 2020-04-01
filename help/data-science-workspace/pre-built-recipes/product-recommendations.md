---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Recette de recommandation de produit
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Recette de recommandation de produit

La recette de recommandations de produits vous permet de fournir des recommandations de produits personnalisées et adaptées aux besoins et aux intérêts de vos clients. Grâce à un modèle de prédiction précis, l’historique des achats d’un client peut vous donner des informations sur les produits qui l’intéressent.

## Pour qui est construite cette recette ?

De nos jours, un détaillant peut  d&#39;une multitude de produits, ce qui donne à ses clients un grand choix qui peut aussi entraver la recherche de leurs clients. En raison des contraintes de temps et d&#39;effort, les clients peuvent ne pas trouver le produit qu&#39;ils désirent, ce qui se traduit par des achats avec un niveau élevé de dissonance cognitive ou par aucun achat.

## Que fait cette recette ?

La recette de recommandations de produits utilise l’apprentissage automatique pour analyser les interactions d’un client avec des produits dans le passé et générer un personnalisé de recommandations de produits rapidement et sans effort. Cela optimise le processus de découverte de produits et élimine les recherches longues, improductives et hors sujet pour vos clients. En conséquence, la recette du module Recommendations produit peut améliorer l’expérience d’achat globale d’un client, ce qui entraîne un engagement plus important et une plus grande fidélité à la marque.

## Comment démarrer ?

Pour commencer, suivez le didacticiel du laboratoire d’Adobe Experience Platform (voir le lien Lab ci-dessous). Ce didacticiel vous explique comment créer la recette de recommandations de produits dans un bloc-notes Jupyter en suivant le processus [du bloc-notes vers la recette](../jupyterlab/create-a-recipe.md) et en implémentant la recette dans Experience Platform Data Science Workspace.

* [Lab : Prédire l’avenir avec Data Science Workspace](https://expleague.azureedge.net/labs/L777/index.html)
* [Ressources Lab](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Data schema

Cette recette utilise un [XDM personnalisé](../../xdm/schema/field-dictionary.md) pour modéliser les données d’entrée et de sortie :

### de données d’entrée

| Nom du champ | Type |
--- | ---
| itemId | Chaîne |
| interactionType | Chaîne |
| timestamp | Chaîne |
| userId | Chaîne |

###  de données de sortie

| Nom du champ | Type |
--- | ---
| recommandations | Chaîne |
| userId | Entier |

## Algorithme

La recette de recommandations de produits utilise le filtrage collaboratif pour générer un personnalisé de recommandations de produits pour vos clients. Contrairement à une approche basée sur le contenu, le filtrage collaboratif ne nécessite pas d’informations sur un produit spécifique, mais utilise plutôt les préférences historiques d’un client sur un ensemble de produits. Cette puissante technique de recommandation repose sur deux hypothèses simples :
* Il existe des clients ayant des intérêts similaires et ils peuvent être regroupés en comparant leurs comportements d’achat et de navigation.
* Un client est plus susceptible d’être intéressé par une recommandation basée sur des clients similaires en termes de comportement d’achat et de navigation.

Ce processus est divisé en deux étapes principales. Tout d’abord, définissez un sous-ensemble de clients similaires. Ensuite, dans ce jeu, identifiez des fonctionnalités similaires parmi ces clients afin de renvoyer une recommandation pour le client .
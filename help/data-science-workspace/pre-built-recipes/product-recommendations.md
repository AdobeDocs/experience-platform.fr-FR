---
keywords: Experience Platform;product recommendation recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Recette de recommandation de produit
topic: overview
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 5%

---


# Recette de recommandation de produit

La recette de recommandations de produits vous permet de fournir des recommandations de produits personnalisées, adaptées aux besoins et intérêts de vos clients. Grâce à un modèle de prédiction précis, l&#39;historique des achats d&#39;un client peut vous fournir des informations sur les produits qui l&#39;intéressent.

## Pour qui est construite cette recette ?

Aujourd&#39;hui, un détaillant peut offre une multitude de produits, offrant à ses clients de nombreux choix qui peuvent également entraver la recherche de ses clients. En raison des contraintes de temps et d&#39;effort, les clients peuvent ne pas trouver le produit qu&#39;ils désirent, ce qui se traduit par des achats avec un niveau élevé de dissonance cognitive ou sans achat du tout.

## Que fait cette recette ?

La recette de recommandations de produits utilise l&#39;apprentissage automatique pour analyser les interactions d&#39;un client avec des produits dans le passé et générer une liste personnalisée de recommandations de produits rapidement et sans effort. Cela optimise le processus de découverte de produits et élimine les recherches longues, improductives et sans rapport avec les clients. En conséquence, la recette de recommandations de produits peut améliorer l&#39;expérience d&#39;achat globale d&#39;un client, ce qui entraîne un engagement plus important et une plus grande fidélité à la marque.

## Comment démarrer ?

Pour commencer, suivez le didacticiel Adobe Experience Platform Lab (voir le lien Lab ci-dessous). Ce didacticiel vous explique comment créer la recette de recommandations de produits dans un bloc-notes Jupyter en suivant le processus de création de recettes [du](../jupyterlab/create-a-recipe.md) bloc-notes et en implémentant la recette dans l’espace de travail des données de la plateforme d’expérience.

* [Lab : Prédire l&#39;avenir avec l&#39;espace de travail Data Science](https://expleague.azureedge.net/labs/L777/index.html)
* [Ressources Lab](https://github.com/adobe/experience-platform-dsw-reference/tree/master/Summit/2019/resources)

## Data schema

Cette recette utilise des schémas [](../../xdm/schema/field-dictionary.md) XDM personnalisés pour modéliser les données d&#39;entrée et de sortie :

### schéma de données d’entrée

| Nom du champ | Type |
--- | ---
| itemId | Chaîne |
| interactionType | Chaîne |
| timestamp | Chaîne |
| userId | Chaîne |

### schéma de données de sortie

| Nom du champ | Type |
--- | ---
| recommandations | Chaîne |
| userId | Entier |

## Algorithme

La recette de recommandations de produits utilise le filtrage collaboratif pour générer une liste personnalisée de recommandations de produits pour vos clients. Contrairement à une approche basée sur le contenu, le filtrage collaboratif ne nécessite pas d’informations sur un produit spécifique, mais utilise plutôt les préférences historiques d’un client sur un ensemble de produits. Cette puissante technique de recommandation repose sur deux hypothèses simples :
* Il existe des clients ayant des intérêts similaires et ils peuvent être regroupés en comparant leurs comportements d’achat et de navigation.
* Un client est plus susceptible d’être intéressé par une recommandation basée sur des clients similaires en termes de comportement d’achat et de navigation.

Ce processus se divise en deux étapes principales. Tout d’abord, définissez un sous-ensemble de clients similaires. Ensuite, dans ce jeu, identifiez des fonctionnalités similaires parmi ces clients afin de renvoyer une recommandation pour le client de la cible.
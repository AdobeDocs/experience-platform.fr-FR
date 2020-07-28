---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Présentation d’Attribution AI
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 94%

---


# Présentation d’Attribution AI

Dans le cadre d’Intelligent Services, Attribution AI est un service d’attribution algorithmique à plusieurs canaux qui calcule l’influence et l’impact incrémentiel des interactions des clients par rapport à des résultats spécifiés. Grâce à Attribution AI, les professionnels du marketing peuvent mesurer et optimiser les dépenses publicitaires et marketing en comprenant l’impact de chaque interaction client sur chaque phase du parcours des clients.

## Fonctionnement d’Attribution AI

Attribution AI est utilisé pour attribuer des crédits aux points de contact qui génèrent des événements de conversion. Il peut aider les spécialistes du marketing à quantifier l’impact publicitaire de chaque point de contact marketing sur le parcours client. Les impressions de publicités affichées, les envois de courriers électroniques, les ouvertures de courriers électroniques ainsi que les clics de référencement payants sont autant d’exemples de points de contact.

Les résultats d’Attribution AI peuvent être répartis dans plusieurs dimensions et utilisés à différentes étapes du parcours client. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en problèmes d’apprentissage automatique, ou de choisir des modèles d’algorithmes, de formation ou de déploiement.

Attribution AI data can be from Adobe (e.g. [!DNL Analytics]) or non-Adobe data sources.

Attribution AI prend en charge deux catégories de scores : les scores algorithmiques et les scores basés sur des règles. Les scores algorithmiques incluent les scores incrémentiels et influencés. Première touche, Dernière touche, Linéaire, En forme de U et Décroissance temporelle sont compris parmi les scores basés sur des règles.

La vidéo suivante est conçue pour vous aider à comprendre l&#39;Attribution AI.

>[!VIDEO](https://video.tv.adobe.com/v/32667?learn=on&quality=12)

## Scores algorithmiques d’Attribution AI

Attribution AI prend en charge deux catégories de scores d’attribution : les scores algorithmiques et les scores basés sur des règles.

Attribution AI produit deux types différents de scores algorithmiques : les scores incrémentiels et les scores influencés. Un score influencé représente la fraction de la conversion dont chaque point de contact marketing est à l’origine. Un score incrémentiel représente le degré d’impact marginal directement causé par le point de contact marketing. La principale différence entre le score incrémentiel et le score influencé est que le score incrémentiel prend en compte l’effet de base. Il ne présume pas qu’une conversion est provoquée uniquement par les points de contact marketing précédents.

Consultez le tableau ci-dessous pour plus de détails sur chacun de ces scores d’attribution :

| Scores d’attribution | Description |
| ----- | ----------- |
| Première touche | Score d’attribution basé sur des règles qui attribue tous les crédits au point de contact initial d’un chemin de conversion. |
| Dernière touche | Score d’attribution basé sur des règles qui attribue tous les crédits au point de contact le plus proche de la conversion. |
| Linéaire | Score d’attribution basé sur des règles qui répartit de manière égale les crédits entre chaque point de contact d’un chemin de conversion. |
| En forme de U | Score d’attribution basé sur des règles qui attribue 40 % des crédits au premier point de contact et 40 % des crédits au dernier point de contact. Les autres points de contact se partagent de manière égale les 20 % restants. |
| Décroissance temporelle | Score d’attribution basé sur des règles qui attribue plus de crédits aux points de contact les plus proches de la conversion par rapport aux points de contact plus éloignés dans le temps de la conversion. |
| Influencé (algorithmique) | Le score influencé représente la fraction de la conversion dont chaque point de contact marketing est à l’origine. |
| Incrémentiel (algorithmique) | Le score incrémentiel représente le degré d’impact marginal directement causé par un point de contact marketing. |

## Exemples de cas d’utilisation commerciale

Attribution AI peut fournir une assistance pour les cas d’utilisation suivants :

- **Rapport à la direction** : permettre aux cadres de comprendre l’impact incrémentiel réel du marketing, tant dans son ensemble que par canal, par région, par SKU, etc.
- **Allocation budgétaire** : faire part des décisions d’allocation du budget sur les différents canaux marketing.
- **Optimisation des campagnes** : déterminer au sein de chaque canal quels sont les éléments créatifs, les mots-clés et les campagnes qui fonctionnent le mieux pour quels SKU ou Géo. Cela vous permet d’examiner chaque canal afin que l’équipe marketing puisse optimiser ses tactiques.
- **Attribution d’entonnoir rempli** : comprendre l’impact du marketing sur l’ensemble du parcours client. Par exemple, d’une création gratuite de compte à une conversion payante et au-delà.
- **Évaluations des partenaires** : évaluer l’efficacité des organismes et des partenaires en fonction des résultats d’attribution.

### Fonctionnalités supplémentaires

Attribution AI also offers integration with other Adobe solutions such as [!DNL Adobe Analytics]. Vous pouvez ainsi utiliser ces solutions pour vous servir du modèle algorithmique personnalisable afin d’évaluer les performances du média et de fournir des informations analytiques.

## Étapes suivantes

Vous pouvez commencer par suivre le guide de [prise en main](./getting-started.md). Ce guide vous accompagne dans la configuration de l’ensemble des prérequêtes nécessaires pour Attribution AI. Si vous disposez déjà de vos informations d’identification et de vos données, consultez le [guide d’utilisation d’Attribution AI](./user-guide.md). Ce guide vous accompagne dans la création d’une instance et son envoi pour formation et notation.
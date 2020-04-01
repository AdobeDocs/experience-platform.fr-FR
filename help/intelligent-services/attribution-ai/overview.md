---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Présentation de l’API d’attribution
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Présentation de l’API d’attribution

Attribution AI, dans le cadre d’Intelligent Services, est un service d’attribution algorithmique à plusieurs qui calcule l’influence et l’impact incrémentiel des interactions client par rapport à des résultats spécifiés. Grâce à l’API d’attribution, les marketeurs peuvent mesurer et optimiser les dépenses publicitaires et marketing en comprenant l’impact de chaque interaction client sur chaque phase du parcours des clients.

## Présentation de l’API d’attribution

L’attribut AI est utilisé pour attribuer des crédits aux points de contact qui génèrent des  de conversion. Les marketeurs peuvent l’utiliser pour quantifier l’impact marketing de chaque point de contact marketing sur les voyages des clients. Parmi les points de contact, citons les impressions d’annonce, les envois par courrier électronique, les ouvertures de courrier électronique et les clics sur les recherches payantes.

Les sorties d’IA d’attribution peuvent être réparties dans différentes dimensions et peuvent être utilisées à différentes étapes du parcours du client. Cela s&#39;effectue sans qu&#39;il faille traduire les besoins des entreprises en problèmes d&#39;apprentissage automatique, en sélectionnant des algorithmes, des formations ou en déployant des modèles.

Les données d’identification d’attribution peuvent provenir de sources de données Adobe (Analytics, par exemple) ou non.

Attribution AI prend en charge deux  de scores, algorithmique et basée sur des règles. Les scores algorithmiques incluent les scores incrémentiels et influencés. Les scores basés sur des règles incluent Première touche, Dernière touche, Linéaire, En forme de U et Décalage temporel.

## Attribution de scores algorithmiques AI

Attribution AI prend en charge deux  de scores d’attribution, les scores algorithmiques et basés sur des règles.

L’attribut AI produit deux types différents de scores algorithmiques, incrémentiels et influencés. Un score influencé est la fraction de la conversion dont est responsable chaque point de contact marketing. Un score incrémentiel est le degré d’impact marginal directement causé par le point de contact marketing. La principale différence entre le score incrémentiel et le score influencé est que le score incrémentiel prend en compte l’effet de ligne de base. Il ne présume pas qu’une conversion est provoquée uniquement par les points de contact marketing précédents.

Consultez le tableau ci-dessous pour plus d’informations sur chacun de ces scores d’attribution :

| Scores d’attribution | Description |
| ----- | ----------- |
| Première touche | Score d’attribution basé sur des règles qui affecte tous les crédits au point de contact initial sur un chemin de conversion. |
| Dernière touche | Score d’attribution basé sur des règles qui attribue tout le crédit au point de contact le plus proche de la conversion. |
| Linéaire | Score d’attribution basé sur des règles qui attribue un crédit égal à chaque point de contact sur un chemin de conversion. |
| En forme de U | Score d’attribution basé sur des règles qui affecte 40 % du crédit au premier point de contact et 40 % du crédit au dernier point de contact, les autres points de contact divisant les 20 % restants de manière égale. |
| Décroissance temporelle | Score d’attribution basé sur des règles où les points de contact plus proches de la conversion reçoivent plus de crédit que les points de contact plus éloignés dans le temps de la conversion. |
| Influencé (algorithmique) | Le score influencé est la fraction de la conversion dont est responsable chaque point de contact marketing. |
| Incrémentiel (algorithmique) | Le score incrémentiel est le degré d’impact marginal directement provoqué par un point de contact marketing. |

## Exemples de cas d’utilisation commerciale

L’attribut AI peut être utilisé pour faciliter l’utilisation des cas d’utilisation suivants :

- **** de l&#39;exécutif : Permettre aux cadres de comprendre l&#39;impact incrémentiel réel du marketing, tant dans son ensemble que par , région, UGS, etc.
- **Allocation** budgétaire : Informer les décisions d’affectation du budget sur les  marketing.
- **Optimisation** Campaign : Dans chaque , déterminez les campagnes, les éléments créatifs et les mots-clés qui fonctionnent le mieux avec les SKU ou les Géo. Cela vous permet d’examiner chaque  afin que l’équipe marketing puisse optimiser ses tactiques.
- **Attribution** d’entonnoir complet : Comprendre l&#39;impact du marketing sur l&#39;ensemble du parcours des clients. Par exemple, l’abonnement gratuit au compte pour la conversion payante et au-delà.
- **Évaluations** partenaires : Évaluer l&#39;efficacité des organismes et des partenaires en fonction des résultats d&#39;attribution.

### Autres fonctionnalités

L’API d’attribution  également l’intégration  des avec d’autres solutions Adobe, telles qu’Adobe Analytics. Vous pouvez ainsi utiliser ces solutions pour utiliser le modèle algorithmique personnalisable afin d’évaluer les performances du média et de fournir des informations analytiques.

## Étapes suivantes

Vous pouvez commencer par suivre le guide de [prise en main](./getting-started.md) . Ce guide vous guide tout au long de la configuration de toutes les pré-requêtes requises pour l’API d’attribution. Si vos informations d’identification et vos données sont déjà prêtes, consultez le guide [de l’utilisateur](./user-guide.md)Attribution AI. Ce guide vous guide tout au long de la création d’une instance et de son envoi pour formation et score.
---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Présentation de l’API d’attribution
topic: Attribution AI
translation-type: tm+mt
source-git-commit: ec0de4c8775367be9e6016529471254ad9f8f453

---


# Présentation de l’API d’attribution

Attribution AI, dans le cadre d&#39;Intelligent Services, est un service d&#39;attribution algorithmique à plusieurs canaux qui calcule l&#39;influence et l&#39;impact incrémentiel des interactions client par rapport à des résultats spécifiés. Grâce à l’API d’attribution, les spécialistes du marketing peuvent mesurer et optimiser les dépenses marketing et publicitaires en comprenant l’impact de chaque interaction client individuelle sur chaque phase du parcours des clients.

## Comprendre l&#39;IA de l&#39;attribution

L’IA de l’attribution est utilisée pour attribuer des crédits aux points de contact menant à des événements de conversion. Les spécialistes du marketing peuvent l’utiliser pour aider à quantifier l’impact marketing de chaque point de contact marketing individuel sur le parcours des clients. Parmi les exemples de points de contact, citons les impressions d’annonces affichées, les envois de courriers électroniques, les ouvertures de courriels et les clics de recherche payante.

Les extrants de l’IA d’attribution peuvent être répartis en différentes dimensions et peuvent être utilisés à différentes étapes du parcours du client. Pour ce faire, il n&#39;est pas nécessaire de traduire les besoins des entreprises en problèmes d&#39;apprentissage automatique, de choisir des algorithmes, des formations ou de déployer des modèles.

Les données de l’API d’attribution peuvent provenir de sources de données Adobe (Analytics, par exemple) ou non.

Attribution AI prend en charge deux catégories de scores, algorithmique et basée sur des règles. Les scores algorithmiques incluent les scores incrémentiels et influencés. Les scores basés sur des règles sont les suivants : Première touche, Dernière touche, Linéaire, En forme de U et Décalage temporel.

La vidéo suivante est conçue pour vous aider à comprendre l&#39;IA de l&#39;attribution.

>[!VIDEO](https://video.tv.adobe.com/v/32667?learn=on&quality=12)

## Attribution de scores algorithmiques AI

Attribution AI prend en charge deux catégories de scores d’attribution, les scores algorithmiques et basés sur des règles.

L’attribut AI produit deux types différents de scores algorithmiques, incrémentiels et influencés. Un score influencé est la fraction de la conversion dont est responsable chaque point de contact marketing. Un score incrémentiel correspond à l’impact marginal directement causé par le point de contact marketing. La principale différence entre le score incrémentiel et le score influencé est que le score incrémentiel prend en compte l’effet de base. Il ne suppose pas qu’une conversion soit provoquée uniquement par les points de contact marketing précédents.

Consultez le tableau ci-dessous pour plus d’informations sur chacun de ces scores d’attribution :

| Scores d’attribution | Description |
| ----- | ----------- |
| Première touche | Score d’attribution basé sur des règles qui affecte tous les crédits au point de contact initial sur un chemin de conversion. |
| Dernière touche | Score d’attribution basé sur des règles qui attribue tout le crédit au point de contact le plus proche de la conversion. |
| Linéaire | Score d’attribution basé sur des règles qui attribue un crédit égal à chaque point de contact sur un chemin de conversion. |
| En forme de U | Score d’attribution basé sur des règles qui attribue 40 % du crédit au premier point de contact et 40 % du crédit au dernier point de contact, les autres points de contact divisant les 20 % restants de manière égale. |
| Décroissance temporelle | Score d’attribution basé sur des règles où les points de contact plus proches de la conversion reçoivent plus de crédit que les points de contact plus éloignés dans le temps de la conversion. |
| Influencé (algorithmique) | Le score influencé correspond à la fraction de la conversion dont est responsable chaque point de contact marketing. |
| Incrémentiel (algorithmique) | Le score incrémentiel est le degré d’impact marginal directement provoqué par un point de contact marketing. |

## Exemples de cas d’utilisation commerciale

L’API d’attribution peut être utilisée pour aider les cas d’utilisation suivants :

- **rapports** exécutif : Permettre aux cadres de comprendre l&#39;impact incrémentiel réel du marketing, à la fois dans son ensemble et par canal, région, UGS, etc.
- **Allocation** budgétaire : Informer les décisions d’affectation du budget sur l’ensemble du canal marketing.
- **Optimisation** de Campaign : Dans chaque canal, identifiez les campagnes, les éléments créatifs et les mots-clés qui fonctionnent le mieux avec les SKU ou les Géo. Cela vous permet d’examiner chaque canal afin que l’équipe marketing puisse optimiser ses tactiques.
- **Attribution** d’entonnoir complet : Comprendre l’impact du marketing sur l’ensemble du parcours des clients. Par exemple, l’abonnement gratuit à un compte pour la conversion payante et au-delà.
- **Évaluations** des partenaires : Évaluer l&#39;efficacité des organismes et des partenaires en fonction des résultats d&#39;attribution.

### Autres fonctionnalités

Attribution AI offre également l’intégration à d’autres solutions Adobe, telles qu’Adobe Analytics. Vous pouvez ainsi utiliser ces solutions pour utiliser le modèle algorithmique personnalisable afin d’évaluer les performances des médias et de fournir des informations analytiques.

## Étapes suivantes

Vous pouvez commencer par suivre le guide de [prise en main](./getting-started.md) . Ce guide vous guide tout au long de la configuration de toutes les pré-requêtes requises pour l’API d’attribution. Si vos informations d’identification et vos données sont déjà prêtes, consultez le Guide [d’utilisation de l’API](./user-guide.md)d’attribution. Ce guide vous guide tout au long des étapes nécessaires pour créer une instance et l’envoyer pour formation et score.
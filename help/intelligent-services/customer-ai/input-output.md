---
keywords: Experience Platform;getting started;customer ai;popular topics;customer ai input;customer ai output
solution: Experience Platform
title: Entrée et sortie de l’IA client
topic: Getting started
description: Le document suivant décrit les différentes entrées et sorties utilisées dans l’IA du client.
translation-type: tm+mt
source-git-commit: c30bbaead775e68f869b080e24e18d4a23cda973
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 33%

---


# Entrée et sortie de l’IA client

Le document suivant décrit les différentes entrées et sorties utilisées dans l’IA du client.

## Données d’entrée d’API client

L’IA du client utilise les données du Événement d’expérience du client pour calculer les scores de propension. Pour plus d’informations sur le Événement d’expérience utilisateur, reportez-vous à la section [Préparer les données à utiliser dans la documentation](../data-preparation.md)d’Intelligent Services.

### Données historiques

L’IA du client requiert des données historiques pour la formation au modèle, mais la quantité de données requise est basée sur deux éléments clés : fenêtre de résultats et population admissible.

Par défaut, l’API du client recherche un utilisateur qui a eu activité au cours des 120 derniers jours si aucune définition de population éligible n’est fournie lors de la configuration de l’application. Outre la quantité minimale de données du Événement d’expérience du client requise, l’API du client a également besoin d’un nombre minimum de événements de réussite basés sur une définition d’objectif prévue. Actuellement, l’API du client nécessite un minimum de 500 événements de réussite.

Les exemples suivants fournis utilisent une formule simple pour vous aider à déterminer la quantité minimale de données requise. Si vous avez plus que les exigences minimales, votre modèle est susceptible de fournir des résultats plus précis. Si vous disposez de moins de la quantité minimale requise, le modèle échoue car il n&#39;y a pas une quantité suffisante de données pour la formation au modèle.

**Formule**:

Longueur minimale des données requises = population admissible + fenêtre de résultat

>[!NOTE]
>
> 30 est le nombre minimum de jours requis pour la population admissible. Si ce n’est pas le cas, la valeur par défaut est de 120 jours.

Exemples :

- Vous souhaitez prédire si un client est susceptible d’acheter une montre dans les 30 prochains jours. Vous souhaitez également noter les utilisateurs qui ont une certaine activité Web au cours des 60 derniers jours. Dans ce cas, la longueur minimale des données est de 60 jours + 30 jours. La population éligible est de 60 jours et la fenêtre de résultats est de 30 jours pour un total de 90 jours.

- Vous souhaitez prédire si l’utilisateur est susceptible d’acheter une montre dans les 7 prochains jours. Dans ce cas, la longueur minimale des données est de 120 jours + 7 jours. La population éligible est définie par défaut sur 120 jours et la fenêtre de résultats est de 7 jours pour un total de 127 jours.

- Vous souhaitez prédire si le client est susceptible d’acheter une montre dans les 7 prochains jours. Vous souhaitez également noter les utilisateurs qui ont une certaine activité Web au cours des 7 derniers jours. Dans ce cas, la longueur minimale des données est de 30 jours + 7 jours. La population admissible a besoin d&#39;un minimum de 30 jours et la fenêtre de résultats est de 7 jours pour un total de 37 jours.

Outre les données minimales requises, l’API du client fonctionne également mieux avec les données récentes. Dans ce cas d’utilisation, l’API du client effectue une prévision pour l’avenir en fonction des données comportementales récentes d’un utilisateur. En d&#39;autres termes, des données plus récentes sont susceptibles de produire une prévision plus précise.

## Données de sortie de Customer AI

Customer AI génère plusieurs attributs pour les profils individuels supposés éligibles. Il existe deux façons de consommer le score en fonction de ce que vous avez mis en service. Si le Profil client en temps réel est activé pour votre jeu de données, vous pouvez l’utiliser via le Profil client en temps réel. Si vous n’avez pas de Profil client en temps réel, vous pouvez télécharger le jeu de données de sortie de l’IA du client disponible sur le lac de données.

>[!NOTE]
>
>Les valeurs de sortie sont utilisées par le Profil client en temps réel qui peut être utilisé pour créer et définir des segments.

Le tableau ci-dessous décrit les différents attributs trouvés dans les sorties de Customer AI :

| Attribut | Description |
| ----- | ----------- |
| Score | La probabilité relative qu’un client atteigne l’objectif prévu au cours de la période définie. Cette valeur ne doit pas être considérée comme un pourcentage de probabilité, mais plutôt comme la probabilité d’un individu par rapport à la population totale. Ce score est compris entre 0 et 100. |
| Probabilité | Cet attribut est la probabilité réelle qu’un profil atteigne l’objectif prévu au cours de la période définie. Si vous comparez les sorties en fonction d’objectifs différents, nous vous recommandons de prendre en compte le percentile ou le score de probabilité. Vous devez toujours utiliser la probabilité lorsque vous essayez de déterminer la probabilité moyenne sur la population éligible, car la probabilité a tendance à être basse pour les événements qui ne se produisent pas fréquemment. Les valeurs des probabilités sont comprises entre 0 et 1. |
| Percentile | Cette valeur fournit des informations concernant la performance d’un profil par rapport à d’autres profils aux notes similaires. Par exemple, un profil dont le rang de percentile est de 99 pour l’attrition indique qu’il y a une forte chance d’attrition par rapport à 99 % des autres profils évalués. Les percentiles sont compris entre 1 et 100. |
| Type de propension | Le type de propension sélectionné. |
| Date de la note | Date à laquelle la notation a eu lieu. |
| Facteurs d’influence | Raisons prévues de la probabilité de conversion ou d’attrition d’un profil. Les facteurs se composent des attributs suivants :<ul><li>Code : le profil ou l’attribut comportemental qui influencent positivement le score prévu d’un profil. </li><li>Valeur : la valeur du profil ou de l’attribut comportemental.</li><li>Importance : indique le poids que le profil ou l’attribut comportemental a sur le score prévu (faible, moyen, élevé)</li></ul> |

## Étapes suivantes {#next-steps}

Une fois vos données préparées et vos informations d’identification et schémas en place, début en suivant le guide [Configurer une instance](./user-guide/configure.md) d’API client. Ce guide vous guide tout au long de la création d’une instance pour l’IA du client.
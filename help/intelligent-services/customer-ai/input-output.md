---
keywords: Experience Platform;getting started;customer ai;popular topics
solution: Experience Platform
title: Prise en main de l’API client
topic: Getting started
translation-type: tm+mt
source-git-commit: 3146442ed0638559ddd68452fd42cc5731b4dc8a

---


# Entrée et sortie IA client

Le suivant  décrit les différentes entrées et sorties utilisées dans l’IA du client.

## Données d’entrée AI du client

L’IA du client utilise les données du d’expérience du client pour calculer les scores de propension. Pour plus d’informations sur les  d’expérience utilisateur, reportez-vous à la section [Préparer les données en vue de les utiliser dans la documentation](../data-preparation.md)d’Intelligent Services.

## Données de sortie AI client

L’IA du client génère plusieurs attributs pour les  individuels qui sont considérés comme éligibles. Il existe deux manières de consommer le score en fonction de ce que vous avez mis en service. Si le  Client en temps réel est activé pour votre jeu de données, vous pouvez le consommer via le Client en temps réel . Si vous n’avez pas de Client en temps réel, vous pouvez télécharger le jeu de données de sortie de l’IA du Client disponible sur le lac de données.

>[!NOTE]
>Les valeurs de sortie sont utilisées par les de clients en temps réel qui peuvent être utilisées pour créer et définir des segments.

Le tableau ci-dessous décrit les différents attributs trouvés dans la sortie de l’API du client :

| Attribut | Description |
| ----- | ----------- |
| Score | probabilité relative pour un client d’atteindre l’objectif prévu dans le délai défini. Cette valeur ne doit pas être traitée comme un pourcentage de probabilité, mais plutôt comme la probabilité d&#39;un individu par rapport à la population globale. Ce score est compris entre 0 et 100. |
| Probabilité | Cet attribut est la probabilité réelle d’un d’atteindre l’objectif prévu dans le délai défini. Lors de la comparaison de sorties entre différents objectifs, il est recommandé de prendre en compte la probabilité par rapport au percentile ou au score. La probabilité doit toujours être utilisée pour déterminer la probabilité moyenne dans la population admissible, car la probabilité tend à être la plus faible pour les  qui ne se produisent pas fréquemment. Les valeurs de probabilité sont comprises entre 0 et 1. |
| Percentile | Cette valeur fournit des informations sur les performances d’un  par rapport à d’autres  de ayant obtenu les mêmes scores. Par exemple, un dont le rang de percentile est de 99 pour l’églises indique qu’il est plus susceptible de se produire que 99 % de tous les autres  qui ont été notés. Les centiles vont de 1 à 100. |
| Type de propension | Type de propension sélectionné. |
| Date de note | Date à laquelle la notation a eu lieu. |
| Facteurs influents | Raisons anticipées de la probabilité de conversion ou d’exécution d’un . Les facteurs comprennent les attributs suivants :<ul><li>Code : Attribut  ou comportemental qui influence positivement un  score prédit. </li><li>Valeur : Valeur de l’attribut  ou comportemental.</li><li>Importance : Indique le  de l’attribut de ou de comportement a sur le score prédit (faible, moyen, élevé)</li></ul> |

## Étapes suivantes {#next-steps}

Une fois que vous avez préparé vos données et que vous avez mis en place toutes vos informations d’identification et vos  de,  en suivant le guide [Configurer une instance](./user-guide/configure.md) d’API client. Ce guide vous guide tout au long de la création d’une instance pour l’API client.
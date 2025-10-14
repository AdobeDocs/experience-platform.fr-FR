---
title: Bonnes pratiques relatives à la gestion avancée du cycle de vie des données
description: Découvrez comment gérer efficacement les demandes d’hygiène des données dans Adobe Experience Platform à l’aide de l’interface utilisateur de gestion avancée du cycle de vie des données et de l’API Data Hygiene. Ce guide couvre les bonnes pratiques telles que la maximisation des identités par requête, la spécification de jeux de données individuels et la limitation de l’API pour éviter les ralentissements. Le document comprend des instructions pour configurer le nettoyage automatique des jeux de données, comment surveiller les statuts des ordres de travail et des méthodes détaillées de récupération des réponses. Suivez ces pratiques pour rationaliser le traitement de vos demandes et optimiser les temps de réponse.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# Bonnes pratiques relatives à la gestion avancée du cycle de vie des données

Utilisez l’interface utilisateur de gestion avancée du cycle de vie des données et l’API Data Hygiene pour gérer efficacement les requêtes de nettoyage et supprimer les données des services Adobe Experience Platform. Suivez ces bonnes pratiques pour rationaliser le traitement de vos demandes et optimiser les temps de réponse d’achèvement.

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique de l’espace de travail du cycle de vie des données et de l’[API Data Hygiene](./api/overview.md). Avant de poursuivre ce document, familiarisez-vous avec les guides sur [la gestion avancée du cycle de vie des données](./home.md) et [la création de demandes de suppression d’enregistrements](./ui/record-delete.md) ou [l’expiration des jeux de données dans l’interface utilisateur](./ui/dataset-expiration.md) ou via l’API.

## Instructions de création d’ordres de travail {#work-order-creation-guidelines}

Vous pouvez utiliser le point d’entrée `/workorder` dans l’API Data Hygiene pour gérer par programmation les requêtes de suppression d’enregistrements dans Experience Platform. Avec ce point d’entrée, vous pouvez créer une requête de suppression, vérifier son statut ou mettre à jour une requête existante. Consultez le document [&#x200B; Point d’entrée d’ordre de travail &#x200B;](./api/workorder.md) pour savoir comment effectuer ces actions à l’aide de l’API.

>[!TIP]
>
>Un ordre de travail est une requête structurée qui effectue des opérations de gestion des données spécifiques, telles que le nettoyage ou la transformation des données, pour assurer un traitement efficace et systématique.

Suivez ces instructions pour optimiser les envois de demandes de nettoyage :

1. **Maximiser les identités par requête :** incluez jusqu’à 100 000 identités par requête de nettoyage pour améliorer l’efficacité. Le traitement par lots de plusieurs identités en une seule demande permet de réduire la fréquence des appels API et de minimiser le risque de problèmes de performances dus à un nombre excessif de demandes à identité unique. Envoyez les demandes avec un nombre maximal d’identités pour accélérer le traitement, car les ordres de travail sont regroupés par lots pour plus d’efficacité.
2. **Spécifier des jeux de données individuels :** pour une efficacité maximale, spécifiez le jeu de données individuel à traiter.
3. **Considérations relatives à la limitation des API :** gardez à l’esprit la limitation des API pour éviter les ralentissements. Les demandes plus petites (&lt; 100 identifiants) à des fréquences plus élevées peuvent donner lieu à 429 réponses et nécessiter une nouvelle soumission à des taux acceptables.

### Gérer les erreurs 429 {#manage-429-errors}

Si vous recevez une erreur 429, cela indique que vous avez dépassé le nombre autorisé de requêtes au cours d’une période donnée. Suivez ces bonnes pratiques pour gérer efficacement les erreurs 429 :

- **Lisez l’en-tête « Retry-After »** : lorsqu’une erreur 429 est renvoyée, vérifiez l’en-tête de réponse « Retry-After ». Cet en-tête spécifie le temps d’attente avant de retenter la requête.
- **Implémenter la logique de reprise** : utilisez la valeur &#39;Retry-After&#39; pour implémenter la logique de reprise dans votre application, en vous assurant que les reprises sont tentées après l’heure spécifiée pour éviter les erreurs 429 suivantes.
- **Traitement par lots des requêtes** : évitez d’envoyer de nombreuses petites requêtes en succession rapide. Au lieu de cela, regroupez plusieurs identités en une seule demande afin de réduire la fréquence des appels et de minimiser le risque d’atteindre les limites de débit.

## Expiration du jeu de données {#dataset-expiration}

Configurez le nettoyage automatique des jeux de données pour les données de courte durée. Utilisez le point d’entrée `/ttl` de l’API Data Hygiene pour planifier des dates d’expiration pour les jeux de données à nettoyer en fonction d’une heure ou d’une date spécifiée. Consultez le Guide du point d’entrée d’expiration du jeu de données pour savoir comment [créer une expiration de jeu de données](./api/dataset-expiration.md) et les [paramètres de requête acceptés](./api/dataset-expiration.md#query-params).

## Surveiller l’ordre de travail et le statut d’expiration du jeu de données {#monitor}

Vous pouvez surveiller efficacement la progression de la gestion du cycle de vie des données à l’aide d’événements **I/O**. Un événement d’E/S est un mécanisme permettant de recevoir des notifications en temps réel sur les modifications ou les mises à jour dans divers services d’Experience Platform.

Les alertes d’événements I/O peuvent être envoyées à un webhook configuré pour permettre l’automatisation de la surveillance des activités. Pour recevoir des alertes par le biais d’un webhook, vous devez enregistrer les alertes Experience Platform dans le Adobe Developer Console. Pour obtenir des instructions détaillées, consultez le guide sur [l’abonnement aux notifications d’événement d’Adobe I/O](../observability/alerts/subscribe.md).

Utilisez les méthodes et directives de cycle de vie des données suivantes pour récupérer et surveiller efficacement les statuts des tâches :

### Événements I/O {#io-events}

Pour surveiller efficacement la progression de vos tâches du cycle de vie des données, configurez et utilisez les événements I/O en procédant comme suit :

- Configurez les webhooks pour recevoir des notifications push concernant les changements de statut.
- Utilisez des notifications pour surveiller la progression et recevoir des mises à jour à la fin de l’opération.
- Évitez d’implémenter des mécanismes d’interrogation pour minimiser le trafic API.

### Récupérer des réponses détaillées pour un seul ordre de travail {#retrieve-detailed-work-order-response}

Pour obtenir des informations détaillées sur des ordres de travail individuels, utilisez l’approche suivante :

- Envoyez une requête GET au point d’entrée `/workorder/{work_order_id}` pour obtenir des données de réponse détaillées.
- Récupérez les réponses et les messages de succès spécifiques au produit.
- Évitez d’utiliser cette méthode pour les activités d’interrogation régulières.

En adhérant à ces bonnes pratiques, vous pouvez gérer efficacement les requêtes de nettoyage et optimiser les temps de réponse dans la gestion avancée du cycle de vie des données.

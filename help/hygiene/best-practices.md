---
title: Bonnes pratiques relatives à la gestion avancée du cycle de vie des données
description: Découvrez comment gérer efficacement les demandes d’hygiène des données dans Adobe Experience Platform à l’aide de l’interface utilisateur avancée de Data Lifecycle Management et de l’API Data Hygiene. Ce guide couvre les bonnes pratiques, telles que l’optimisation des identités par requête, la spécification de jeux de données individuels et la prise en compte du ralentissement de l’API pour éviter les ralentissements. Le document comprend des instructions pour la configuration du nettoyage automatique des jeux de données, la manière de surveiller les statuts des ordres de travail et les méthodes détaillées de récupération des réponses. Suivez ces pratiques pour rationaliser le traitement de vos requêtes et optimiser les temps de réponse.
exl-id: 75e2a97b-ce6c-4ebd-8fc8-597887f77037
source-git-commit: 5174529d606ac0186ff3193790ada70a46c7e274
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# Bonnes pratiques relatives à la gestion avancée du cycle de vie des données

Utilisez l’interface utilisateur Advanced Data Lifecycle Management et l’API Data Hygiene pour gérer efficacement les demandes de nettoyage et supprimer des données des services Adobe Experience Platform. Suivez ces bonnes pratiques pour rationaliser le traitement de vos demandes et optimiser les temps de réponse d’achèvement.

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique de l’espace de travail du cycle de vie des données et de l’ [ API d’hygiène des données](./api/overview.md). Avant de poursuivre ce document, familiarisez-vous avec les guides sur la [gestion avancée du cycle de vie des données](./home.md) et la [création de requêtes de suppression d’enregistrement](./ui/record-delete.md) ou les [expirations de jeux de données dans l’interface utilisateur](./ui/dataset-expiration.md) ou via l’API.

## Instructions de création d’un ordre de travail {#work-order-creation-guidelines}

Vous pouvez utiliser le point d’entrée `/workorder` dans l’API Data Hygiene pour gérer par programmation les demandes de suppression d’enregistrements dans Experience Platform. Avec ce point de terminaison, vous pouvez créer une requête de suppression, vérifier son état ou mettre à jour une requête existante. Consultez le [ document Point d’entrée de l’ordre de travail](./api/workorder.md) pour savoir comment effectuer ces actions à l’aide de l’API.

>[!TIP]
>
>Un ordre de travail est une requête structurée qui effectue des opérations de gestion de données spécifiques, telles que le nettoyage ou la transformation des données, pour assurer un traitement efficace et systématique.

Suivez ces instructions pour optimiser les envois de requêtes de nettoyage :

1. **Maximiser les identités par requête :** Incluez jusqu’à 100 000 identités par requête de nettoyage pour améliorer l’efficacité. Le regroupement de plusieurs identités en une seule requête permet de réduire la fréquence des appels d’API et de minimiser le risque de problèmes de performances en raison d’un nombre excessif de demandes d’identité unique. Envoyez des demandes avec un nombre maximal d’identités pour accélérer le traitement, car les ordres de travail sont traités par lots pour plus d’efficacité.
2. **Spécifiez des jeux de données individuels :** Pour une efficacité maximale, spécifiez le jeu de données individuel à traiter.
3. **Considérations relatives au ralentissement de l’API :** Tenez compte du ralentissement de l’API pour éviter les ralentissements. Des demandes plus petites (&lt; 100 ID) à des fréquences plus élevées peuvent donner lieu à 429 réponses et nécessiter un renvoi à des taux acceptables.

### Gestion des erreurs 429 {#manage-429-errors}

Si vous recevez une erreur 429, elle indique que vous avez dépassé le nombre autorisé de requêtes au cours d’une période donnée. Suivez ces bonnes pratiques pour gérer efficacement les erreurs 429 :

- **Lisez l’en-tête &#39;Retry-After&#39;** : lorsqu’une erreur 429 est renvoyée, vérifiez l’en-tête de réponse &#39;Retry-After&#39;. Cet en-tête indique le temps d’attente avant de retenter la requête.
- **Implémentation de la logique de nouvelle tentative** : utilisez la valeur &quot;Retry-After&quot; pour implémenter la logique de nouvelle tentative dans votre application, en veillant à ce que les tentatives soient effectuées après le délai spécifié afin d’éviter les erreurs 429 suivantes.
- **Lancer vos requêtes** : évitez d’envoyer de nombreuses petites requêtes l’une après l’autre. Vous pouvez plutôt regrouper plusieurs identités dans une seule requête afin de réduire la fréquence des appels et de minimiser le risque d’atteindre les limites de taux.

## Expiration du jeu de données {#dataset-expiration}

Configurez le nettoyage automatique des jeux de données pour les données de courte durée. Utilisez le point de terminaison `/ttl` de l’API Data Hygiene pour planifier des dates d’expiration pour les jeux de données à nettoyer en fonction d’une heure ou d’une date spécifiées. Consultez le guide du point de terminaison d’expiration du jeu de données pour savoir comment [créer une expiration de jeu de données](./api/dataset-expiration.md) et les [paramètres de requête acceptés](./api/dataset-expiration.md#query-params).

## Surveillance de l’ordre de travail et de l’état d’expiration du jeu de données {#monitor}

Vous pouvez surveiller efficacement la progression de la gestion de votre cycle de vie des données à l’aide des **événements I/O**. Un événement d’E/S est un mécanisme permettant de recevoir des notifications en temps réel sur les modifications ou mises à jour de divers services de Platform.

Les alertes d’événement d’E/S peuvent être envoyées à un webhook configuré pour permettre l’automatisation de la surveillance des activités. Pour recevoir des alertes via webhook, vous devez enregistrer votre webhook pour les alertes Platform dans Adobe Developer Console. Pour obtenir des instructions détaillées, reportez-vous au guide sur l’ [abonnement aux notifications d’événement d’Adobe I/O](../observability/alerts/subscribe.md) .

Utilisez les méthodes et directives de cycle de vie des données suivantes pour récupérer et surveiller efficacement les états des tâches :

### Événements I/O {#io-events}

Pour surveiller efficacement la progression de vos tâches de cycle de vie des données, configurez et utilisez des événements I/O en procédant comme suit :

- Configurez des webhooks pour recevoir des notifications push pour les modifications d’état.
- Utilisez les notifications pour surveiller la progression et recevoir des mises à jour une fois l’opération terminée.
- Évitez d’implémenter des mécanismes d’interrogation pour réduire le trafic API.

### Récupération de réponses détaillées pour un seul ordre de travail {#retrieve-detailed-work-order-response}

Pour obtenir des informations détaillées sur les différents ordres de travail, utilisez l’approche suivante :

- Effectuez une requête de GET au point de terminaison `/workorder/{work_order_id}` pour obtenir des données de réponse détaillées.
- Récupérez des réponses et des messages de succès spécifiques à un produit.
- Évitez d’utiliser cette méthode pour des activités d’interrogation régulières.

En adhérant à ces bonnes pratiques, vous pouvez gérer efficacement les demandes de nettoyage et optimiser les temps de réponse dans la gestion avancée du cycle de vie des données.

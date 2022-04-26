---
description: Découvrez comment Experience Platform gère les différents types d’erreurs renvoyés par les destinations en continu et comment il tente à nouveau d’envoyer des données à la plateforme de destination.
title: Limitation de débit et stratégie de reprise pour les destinations de diffusion en continu créées avec Destination SDK
source-git-commit: ec50608f6454dd619c30b6337f454561844183ba
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 4%

---

# Limitation de débit et stratégie de reprise pour les destinations de diffusion en continu créées avec Destination SDK

## Présentation {#overview}

Les destinations créées par des partenaires peuvent renvoyer diverses erreurs et avoir des stratégies de limitation de débit différentes. Cette page explique comment Experience Platform gère les différents types d’erreurs renvoyés par les destinations de diffusion en continu.

Lors de la configuration d’une destination à l’aide de Destination SDK, vous pouvez choisir entre deux types d’agrégation : [agrégation des meilleurs efforts](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation) et [agrégation configurable](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation). Selon le type d’agrégation que vous sélectionnez, lisez ci-dessous la manière dont Experience Platform gère les erreurs et les limites de taux.

## Agrégation des meilleurs efforts {#best-effort-aggregation}

Pour tout appel HTTP vers votre destination qui échoue, l’Experience Platform tente d’effectuer à nouveau l’appel une fois immédiatement après le premier appel. Si l’appel échoue toujours lors de la deuxième tentative, l’Experience Platform annule l’appel et ne le renouvelle pas une troisième fois.

## Agrégation configurable {#configurable-aggregation}

Dans le cas des plateformes de destination configurées avec une agrégation configurable, Experience Platform fait la distinction entre le type d’erreur renvoyé par votre plateforme :

* Erreurs dans lesquelles l’Experience Platform tente à nouveau d’envoyer les données à votre plateforme :
   * Codes de réponse HTTP 420 et 429
   * Codes de réponse HTTP supérieurs à 500
* Erreurs dans lesquelles Experience Platform *ne fait pas* réessayer d&#39;envoyer les données à votre plateforme : tous les autres renvoyés par votre plateforme

### Approche de reprise décrite {#retry-approach}

L’approche Experience Platform de l’agrégation configurable est décrite ci-dessous. Cet exemple suppose que l’Experience Platform envoie des données à une plateforme de destination qui commence à renvoyer des codes d’erreur 429 s’il reçoit plus de 50 000 demandes par minute :

* Minute 1 : Experience Platform regroupe 40 000 lots avec des profils à envoyer à votre plateforme de destination. Experience Platform effectue 40 000 requêtes HTTP et toutes les requêtes sont réussies.
* Minute 2 : Experience Platform agrège 70 000 lots avec des profils à envoyer à votre plateforme de destination. Experience Platform effectue 70 000 requêtes HTTP et 50 000 requêtes. Les autres 20 000 reçoivent une erreur de limitation de débit de votre point de terminaison et seront retentées dans 30 minutes.
* Minute 3 : Experience Platform agrège 30 000 lots avec des profils à envoyer à votre plateforme de destination. Experience Platform effectue 30 000 requêtes HTTP et toutes sont réussies.
* ...
* ...
* Minute 32 : Experience Platform tente à nouveau d’envoyer les 20 000 lots qui ont échoué à la minute 2. Tous les appels sont réussis.

## Étapes suivantes {#next-steps}

Vous savez maintenant comment Experience Platform gère les erreurs et la limitation de débit à partir des plateformes de destination, en fonction de la stratégie d’agrégation que vous avez sélectionnée lors de la configuration de votre destination de diffusion en continu. Vous pouvez ensuite consulter la documentation suivante :

* [Tester la configuration de votre destination](/help/destinations/destination-sdk/test-destination.md)
* [Envoyer pour révision une destination créée dans Destination SDK](/help/destinations/destination-sdk/submit-destination.md)

---
description: Découvrez comment le système Experience Platform gère les différents types d’erreurs renvoyés par les destinations de diffusion en streaming et comment il tente à nouveau d’envoyer des données à la plateforme de destination.
title: Politique de limitation du débit et de nouvelle tentative pour les destinations de diffusion en streaming créées avec Destination SDK
exl-id: aad10039-9957-4e9e-a0b7-7bf65eb3eaa9
source-git-commit: 75bee8fde648101335df7a66eae1907b267b4eb6
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 81%

---

# Politique de limitation du débit et de nouvelle tentative pour les destinations de diffusion en streaming créées avec Destination SDK

Les destinations créées par des partenaires peuvent renvoyer diverses erreurs et avoir des politiques de limitation de débit différentes. Cette page explique comment Experience Platform gère les différents types d’erreurs renvoyés par les destinations de diffusion en streaming.

Pendant la configuration d’une destination à l’aide de Destination SDK, vous pouvez choisir entre deux types d’agrégations : [agrégation des meilleurs efforts](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) et [agrégation configurable](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). Selon le type d’agrégation que vous sélectionnez, découvrez ci-dessous la manière dont Experience Platform gère les erreurs et les limites de taux.

## Agrégation des meilleurs efforts {#best-effort-aggregation}

Experience Platform relance les appels qui renvoient les codes de réponse HTTP suivants : **403, 408, 409, 429, 500, 502, 503, 504**. Deux reprises sont effectuées aux intervalles suivants :

* Première tentative : après 15 secondes
* Deuxième tentative : après 30 secondes

Experience Platform ne relance *pas* les appels qui renvoient d’autres codes de réponse HTTP, tels que 400 (Bad Request). Si l’appel échoue toujours après les deux nouvelles tentatives, Experience Platform interrompt l’activation et ne la tente pas à nouveau.

Vous pouvez demander une politique de reprise différente pour des flux de données spécifiques en contactant le service clientèle.

## Agrégation configurable {#configurable-aggregation}

Dans le cas des plateformes de destination configurées avec une agrégation configurable, Experience Platform fait la distinction entre le type d’erreur renvoyé par votre plateforme :

* Erreurs pour lesquelles Experience Platform essaie à nouveau d’envoyer les données à votre plateforme :
   * Codes de réponse HTTP 420 et 429
   * Codes de réponse HTTP supérieurs à 500
* Erreurs pour lesquelles Experience Platform *n’essaie pas* de renvoyer les données à votre plateforme : toutes les autres erreurs renvoyées par votre plateforme

### Nouvelle approche décrite {#retry-approach}

L’approche Experience Platform de l’agrégation configurable est décrite ci-dessous. Cet exemple suppose qu’Experience Platform envoie des données à une plateforme de destination qui commence à renvoyer des codes d’erreur 429 s’il reçoit plus de 50 000 requêtes par minute :

* Première minute : Experience Platform regroupe 40 000 lots avec des profils à envoyer à votre plateforme de destination. Experience Platform effectue 40 000 requêtes HTTP et toutes les requêtes ont abouti.
* Deuxième minute : Experience Platform regroupe 70 000 lots avec des profils à envoyer à votre plateforme de destination. Experience Platform effectue 70 000 requêtes HTTP et 50 000 ont abouti. Les 20 000 autres reçoivent une erreur de limitation de débit de votre point d’entrée et feront l’objet d’une nouvelle tentative au bout de 30 minutes.
* Troisième minute : Experience Platform regroupe 30 000 lots avec des profils à envoyer à votre plateforme de destination. Experience Platform effectue 30 000 requêtes HTTP et toutes les requêtes ont abouti.
* …
* …
* 32e minute : Experience Platform tente à nouveau d’envoyer les 20 000 lots qui ont échoué à la deuxième minute. Tous les appels ont abouti.

## Étapes suivantes {#next-steps}

Vous savez à présent comment Experience Platform gère les erreurs et la limitation de débit à partir des plateformes de destination, en fonction de la politique d’agrégation que vous avez sélectionnée au moment de la configuration de la destination de diffusion en streaming. Vous pouvez désormais consulter la documentation suivante :

* [Test de la configuration de la destination](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Envoi pour révision d’une destination créée dans Destination SDK](../guides/submit-destination.md)

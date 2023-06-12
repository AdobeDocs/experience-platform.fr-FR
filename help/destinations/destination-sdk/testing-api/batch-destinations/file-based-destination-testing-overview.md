---
description: Découvrez comment utiliser l’API de test de destination basée sur des fichiers pour valider la configuration de vos destinations basées sur des fichiers créés avec Destination SDK.
title: API de test de destination basée sur les fichiers
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 100%

---


# Présentation de l’API de test de destination basée sur des fichiers

L’API de test de destination basée sur des fichiers est un ensemble de points d’entrée que vous pouvez utiliser pour valider la configuration de vos destinations basées sur des fichiers créés avec Destination SDK.

Nous vous recommandons d’utiliser ces outils pour valider votre configuration avant l’[envoi](../../guides/submit-destination.md) de la destination pour révision à Adobe.

Pour obtenir de meilleurs résultats de test, nous vous recommandons d’utiliser cette API en fonction du diagramme de flux ci-dessous.

![Diagramme affichant le flux de test de destination recommandé](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

Consultez les sections ci-dessous pour avoir une vue d’ensemble des fonctionnalités offertes par chaque point d’entrée.

## Génération de profils types {#generate-sample-profiles}

Utilisez le point d’entrée `/sample-profiles` de l’API pour générer des profils types en fonction de votre schéma source existant.

Les profils types peuvent vous aider à comprendre la structure JSON d’un profil. En outre, ils vous donnent une valeur par défaut que vous pouvez personnaliser avec vos propres données de profil pour d’autres tests de destination.

Pour découvrir comment générer des profils types, consultez la [documentation dédiée](file-based-sample-profile-generation-api.md).

## Test de la configuration de destination {#test-destination-configuration}

Utilisez le point d’entrée `/testing/destinationInstance` de l’API pour tester si la destination basée sur des fichiers est configurée correctement et pour vérifier l’intégrité des flux de données vers la destination configurée.

Vous pouvez envoyer des requêtes au point d’entrée de test avec ou sans ajouter de [profils types](file-based-sample-profile-generation-api.md) à l’appel. Si vous n’envoyez aucun profil à la requête, l’API génère automatiquement un profil type et l’ajoute à la requête.

Pour découvrir comment tester la configuration de destination avec des profils types, consultez la [documentation dédiée](file-based-destination-testing-api.md).

## Consulter les résultats détaillés de l’activation {#view-detailed-activation-results}

Utilisez le point d’entrée `/testing/destinationInstance` de l’API pour afficher les détails complets de vos résultats de tests des destinations basés sur des fichiers.

Ce point d’entrée de l’API renvoie le même résultat que celui obtenu lors de l’utilisation de l’[API Flow Service](../../../api/update-destination-dataflows.md) pour surveiller les flux de données.

Pour découvrir comment afficher les résultats détaillés de l’activation, consultez la [documentation dédiée](file-based-destination-results-api.md).

## Rendu des champs de données clients {#render-customer-data-fields}

Utilisez le point d’entrée `/authoring/testing/template/render` de l’API pour visualiser à quoi les [champs de données client](../../functionality/destination-configuration/customer-data-fields.md) modélisés définis dans votre configuration de destination ressembleraient.

Le point d’entrée de l’API génère des valeurs aléatoires pour vos champs de données client et les renvoie dans la réponse. Cela vous permet de valider la structure sémantique des champs de données client, tels que les noms de compartiment ou les chemins d’accès au dossier.

Pour découvrir comment générer et visualiser des valeurs pour vos champs de données client, consultez la [documentation dédiée](file-based-render-template-api.md).

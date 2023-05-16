---
description: Découvrez comment utiliser l’API de test de destination basée sur les fichiers pour valider la configuration de vos destinations basées sur des fichiers créées via la Destination SDK.
title: API de test de destination basée sur les fichiers
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---


# Présentation de l’API de test de destination basée sur des fichiers

L’API de test de destination basée sur les fichiers est un ensemble de points de terminaison que vous pouvez utiliser pour valider la configuration de vos destinations basées sur des fichiers créées via la Destination SDK.

Nous vous recommandons d’utiliser ces outils pour valider votre configuration avant [envoi](../../guides/submit-destination.md) votre destination pour la révision à Adobe.

Pour obtenir les meilleurs résultats de test, nous vous recommandons d’utiliser cette API en fonction du diagramme de flux ci-dessous.

![Diagramme affichant le flux de test de destination recommandé](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

Consultez les sections ci-dessous pour un bref aperçu de ce que chaque point de terminaison peut faire.

## Générer des exemples de profils {#generate-sample-profiles}

Utilisez la variable `/sample-profiles` Point d’entrée d’API pour générer des exemples de profils en fonction de votre schéma source existant.

Les exemples de profils peuvent vous aider à comprendre la structure JSON d’un profil. En outre, ils vous donnent une valeur par défaut que vous pouvez personnaliser avec vos propres données de profil, pour d’autres tests de destination.

Voir [documentation dédiée](file-based-sample-profile-generation-api.md) pour savoir comment générer des profils d’exemple.

## Test de la configuration de la destination {#test-destination-configuration}

Utilisez la variable `/testing/destinationInstance` Point de terminaison d’API pour tester si votre destination basée sur des fichiers est configurée correctement et pour vérifier l’intégrité des flux de données vers votre destination configurée.

Vous pouvez envoyer des requêtes au point de terminaison de test avec ou sans ajouter [exemples de profils](file-based-sample-profile-generation-api.md) à l’appel . Si vous n’envoyez aucun profil à la requête, l’API génère automatiquement un exemple de profil et l’ajoute à la requête.

Voir [documentation dédiée](file-based-destination-testing-api.md) pour savoir comment tester votre configuration de destination avec des exemples de profils.

## Consulter les résultats détaillés de l’activation {#view-detailed-activation-results}

Utilisez la variable `/testing/destinationInstance` Le point de terminaison de l’API vous permet d’afficher les détails complets de vos résultats de test de destination basés sur des fichiers.

Ce point de terminaison API renvoie le même résultat que vous obtiendriez lors de l’utilisation de la variable [API de service de flux](../../../api/update-destination-dataflows.md) pour surveiller les flux de données.

Voir [documentation dédiée](file-based-destination-results-api.md) pour savoir comment afficher des résultats d’activation détaillés.

## Rendu des champs de données client {#render-customer-data-fields}

Utilisez la variable `/authoring/testing/template/render` Point d’entrée de l’API pour visualiser la manière dont le modèle est [Champs de données client](../../functionality/destination-configuration/customer-data-fields.md) défini dans votre configuration de destination ressemblerait à ce qui suit.

Le point de terminaison de l’API génère des valeurs aléatoires pour vos champs de données client et les renvoie dans la réponse . Cela vous permet de valider la structure sémantique des champs de données client, tels que les noms de compartiment ou les chemins d’accès aux dossiers.

Voir [documentation dédiée](file-based-render-template-api.md) pour savoir comment générer et visualiser des valeurs pour vos champs de données client.

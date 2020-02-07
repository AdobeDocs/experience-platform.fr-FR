---
title: Présentation de l’API client (alpha)
seo-title: Présentation de l’API client (alpha)
description: Ce document présente un aperçu des statistiques Sensei - Customer AI (Alpha)
seo-description: Ce document présente un aperçu des statistiques Sensei - Customer AI (Alpha)
index: false
translation-type: tm+mt
source-git-commit: fde2bb7af91dbcb0c701397c878b63044cb27a4d

---


# Présentation de l’API client (alpha)

>[!NOTE]
>La fonctionnalité d’IA du client décrite dans ce document est en alpha. La documentation et la fonctionnalité peuvent être modifiées.

L’API du client dans Adobe Experience Platform permet aux spécialistes du marketing de tirer parti d’Adobe Sensei pour anticiper ce que leurs clients feront ensuite grâce à l’apprentissage automatique.

## À quoi sert-il ?

L’IA du client est utilisée pour générer des scores de propension personnalisés tels que l’exécution et la conversion pour des profils individuels à l’échelle. Cela s’effectue sans avoir à transformer les besoins de l’entreprise en un problème d’apprentissage automatique, en choisissant un algorithme, une formation ou un déploiement.

L’API client est conçue pour :

- Améliorez le profil du client en temps réel grâce aux scores de propension des clients, tels que le taux d’activité et de conversion.
- Améliorer les profils du client avec les codes de motif pour les scores de propension.
- Créez des segments de clients en fonction des scores de propension et des facteurs influents.

Le client n’est pas conçu pour :

- Prévoyez le prix d&#39;achat des produits.
- Prévoyez quels produits précédemment achetés seront dans la prochaine commande d’un client.
- Générer des recommandations de produit à l’échelle.
- Déterminer l&#39;étape du parcours d&#39;achat du client
- Prévoyez le prochain total de départ d’un client.

## Comment ça marche ?

L’IA du client procède à l’analyse des données existantes de l’événement d’expérience du client afin de prévoir les scores de tendance de génération ou de conversion. Adobe se rend compte que la définition de la génération et de la conversion n’est pas uniforme dans tous les cas d’utilisation. C’est pourquoi vous pouvez définir des objectifs de ciblage personnalisés comme un ensemble de conditions. Vous pouvez configurer l’objectif prévu tant que l’événement d’intérêt est présent dans les données d’événement d’expérience de consommation saisies.

## Comment démarrer ?

Pour commencer, suivez le didacticiel [Prévoyez les scores de propension des clients à l’aide de l’IA](./customer-ai-tutorial.md)du client. Il décrit les étapes à suivre pour utiliser l’IA du client et montre la création de segments de client à l’aide de scores de propension.
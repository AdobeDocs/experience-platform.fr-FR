---
title: Présentation de Customer AI (alpha)
seo-title: Présentation de Customer AI (alpha)
description: Ce document présente Sensei Insights — Customer AI (alpha)
seo-description: Ce document présente Sensei Insights — Customer AI (alpha)
index: false
translation-type: ht
source-git-commit: fde2bb7af91dbcb0c701397c878b63044cb27a4d

---


# Présentation de Customer AI (alpha)

>[!NOTE]
>Ce document décrit la version alpha de la fonctionnalité Customer AI. La documentation et la fonctionnalité peuvent changer.

Dans Adobe Experience Platform, Customer AI permet aux spécialistes marketing de tirer parti d’Adobe Sensei pour anticiper, grâce à l’apprentissage automatique, les actions de leurs clients.

## À quoi sert la fonctionnalité ?

Customer AI est utilisée pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique, en choisissant un algorithme, une formation ou un déploiement.

Customer AI est conçue pour :

- améliorer le profil client en temps réel grâce aux scores de propension des clients, comme les taux d’attrition et de conversion ;
- améliorer les profils client avec des codes de motif pour les scores de propension ;
- créer des segments de clientèle en fonction des scores de propension et des facteurs décisifs.

Customer AI n’est pas conçue pour :

- prédire le prix d’achat des produits ;
- prédire quels produits déjà achetés seront dans la prochaine commande d’un client ;
- générer des recommandations de produits à grande échelle ;
- déterminer l’étape du parcours d’achat du client ;
- prévoir le prochain total d’achat d’un client.

## Comment fonctionne-t-elle ?

Customer AI analyse les données d’événement d’expérience existantes pour le client afin de prévoir les taux d’attrition ou de conversion. Adobe sait que les définitions de l’attrition et de la conversion ne sont pas uniformes dans tous les cas d’utilisation. Pour cette raison, il est possible de définir des objectifs personnalisés comme ensemble de conditions. L’utilisateur peut configurer l’objectif prévu tant que l’événement d’intérêt est présent dans les données d’événement d’expérience client saisies.

## Comment démarrer ?

Pour commencer, suivez le tutoriel [Prévoir les scores de propension des clients à l’aide de Customer AI](./customer-ai-tutorial.md). Ce tutoriel décrit les étapes à suivre pour utiliser Customer AI et explique comment créer des segments client à l’aide de scores de propension.
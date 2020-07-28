---
keywords: Experience Platform;overview;customer ai;popular topics
solution: Experience Platform
title: Présentation de Customer AI
topic: Customer AI overview
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 85%

---


# Présentation de Customer AI

En tant que composant des services intelligents, Customer AI permet aux professionnel du marketing de générer des prédictions client au niveau individuel avec des explications.

À l’aide de facteurs d’influence, Customer AI peut vous indiquer ce qu’un client est susceptible de faire et pourquoi. De plus, les professionnels du marketing peuvent tirer parti des prédictions et des informations de Customer AI pour personnaliser les expériences client en diffusant les offres et les messages les plus appropriés.

## Fonctionnement de Customer AI

Customer AI est utilisé pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Cette opération s’effectue sans qu’il soit nécessaire de transformer les besoins professionnels en un problème d’apprentissage automatique ou d’avoir recours à un algorithme, à une formation ou à un déploiement.

Customer AI est conçu pour :

- proposer des modèles de propension des clients à haute précision pour une segmentation et un ciblage plus forts ;
- faciliter la compréhension des facteurs d’influence et la probabilité derrière certains comportements des clients ;
- offrir des options personnalisables pour les cas d’utilisation et les données uniques de votre entreprise ;
- améliorer Real-time Customer Profile grâce aux scores de propension des clients, comme les taux d’attrition et de conversion ;
- améliorer les profils client avec des facteurs d’influence pour les scores de propension ;
- créer des segments de clientèle en fonction de facteurs d’influence et de scores de propension.

Customer AI n’est pas conçu pour certaines utilisations :

- Customer AI ne doit pas être utilisé pour prédire la tarification dynamique, ni le prix auquel le client va effectuer un achat.
- Customer AI ne peut pas déterminer si une offre va inciter un client à acheter un article. Bien que vous puissiez décider d’envoyer des réductions basées sur des scores de propension, cela n’est pas nécessairement la meilleure façon de convertir ces clients.
- Customer AI n’est pas un outil de recommandation de produits. If you have thousands of SKUs, do not use Customer AI as a proxy for a real product recommendations solution like [!DNL Adobe Target].
- Customer AI ne peut pas déterminer à quel stade du parcours d’achat se trouve le client, par exemple s’il est en phase de « sensibilisation », de « considération », d’« achat » ou de « rétention ».
- N’utilisez pas Customer AI pour identifier les clients susceptibles d’acheter un produit qui sera lancé ultérieurement. Certains événement de succès doivent s’être produits pour que Customer AI puisse correctement former l’algorithme d’apprentissage automatique sur vos données.

La vidéo suivante est conçue pour vous aider à comprendre l’IA du client.

>[!VIDEO](https://video.tv.adobe.com/v/32664?learn=on&quality=12)

## Comment fonctionne-t-il ?

Customer AI analyse les données d’événement d’expérience existantes pour le client afin de prévoir les taux d’attrition ou de conversion. Adobe sait que les définitions de l’attrition et de la conversion ne sont pas uniformes dans tous les cas d’utilisation. Pour cette raison, il est possible de définir des objectifs personnalisés comme ensemble de conditions. L’utilisateur peut configurer l’objectif prévu tant que l’événement d’intérêt est présent dans les données d’événement d’expérience client saisies.

## Étapes suivantes

Vous pouvez commencer par suivre le [guide de prise en main](./getting-started.md). Ce guide vous guide tout au long de la configuration de toutes les conditions préalables requises pour l’IA du client. If you already have all your credentials and data ready, visit  [configuring a Customer AI instance](./user-guide/configure.md). Il décrit les étapes à suivre pour utiliser l’IA du client.
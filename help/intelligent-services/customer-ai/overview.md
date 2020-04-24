---
keywords: Experience Platform;overview;customer ai;popular topics
solution: Experience Platform
title: Présentation de Customer AI
topic: Customer AI overview
translation-type: tm+mt
source-git-commit: f4deee30f0f03b75dc7ee02152ceb6c519858c7c

---


# Présentation de Customer AI

L’API du client, dans le cadre d’Intelligent Services, permet aux spécialistes du marketing de générer des prévisions client au niveau individuel avec des explications.

Avec l’aide de facteurs influents, l’IA du client peut vous dire ce qu’un client est susceptible de faire et pourquoi. En outre, les spécialistes du marketing peuvent tirer parti des prédictions et des informations sur l’IA du client pour personnaliser les expériences du client en diffusant les  et les messages  les plus appropriés.

## Compréhension de l’IA du client

Customer AI est utilisée pour générer des scores de propension personnalisés tels que les taux d’attrition et de conversion de profils individuels à grande échelle. Pour ce faire, il n’est pas nécessaire de transformer les besoins de l’entreprise en un problème d’apprentissage automatique, de choisir un algorithme, de le former ou de le déployer.

Customer AI est conçue pour :

- Proposez des modèles de propension des clients à haute précision pour une segmentation et un ciblage plus forts.
- Aidez-nous à comprendre les facteurs influents et la probabilité derrière certains comportements des clients.
- Proposez des options personnalisables pour les cas d’utilisation et les données uniques de votre .
- améliorer le profil client en temps réel grâce aux scores de propension des clients, comme les taux d’attrition et de conversion ;
- Améliorez les  des clients grâce à des facteurs influents pour les scores de propension.
- Créez des segments de clients en fonction de facteurs influents et de scores de propension.

Customer AI n’est pas conçue pour :

- L’IA du client ne doit pas être utilisée pour prédire la tarification dynamique, ni le point de prix auquel le client va faire un achat.
- L’IA du client ne peut pas déterminer si le fait de donner un   à un client rend ce dernier plus susceptible d’acheter un article. Bien que vous puissiez décider d’envoyer des  de réduction  en fonction des scores de propension, ce n’est pas nécessairement la meilleure façon de convertir ces clients.
- L’IA du client n’est pas un outil de recommandation de produit. Si vous disposez de milliers de SKU, n’utilisez pas l’API du client comme proxy pour une solution de recommandations de produit réelle, telle qu’Adobe .
- L’IA du client ne peut pas prédire à quel stade du voyage d’achat se trouve le client, par exemple, s’il est en phase de &quot;sensibilisation&quot;, de &quot;considération&quot;, d’&quot;achat&quot; ou de &quot;rétention&quot;.
- N’utilisez pas l’IA du client pour déterminer les clients qui achèteront probablement un produit qui sera lancé ultérieurement. Pour ce faire, certains de réussite doivent être présents dans le passé pour que l’API du client puisse correctement former l’algorithme d’apprentissage automatique sur vos données.

## Comment fonctionne-t-elle ?

Customer AI analyse les données d’événement d’expérience existantes pour le client afin de prévoir les taux d’attrition ou de conversion. Adobe sait que les définitions de l’attrition et de la conversion ne sont pas uniformes dans tous les cas d’utilisation. Pour cette raison, il est possible de définir des objectifs personnalisés comme ensemble de conditions. L’utilisateur peut configurer l’objectif prévu tant que l’événement d’intérêt est présent dans les données d’événement d’expérience client saisies.

## Étapes suivantes

Vous pouvez commencer par suivre le guide de [prise en main](./getting-started.md) . Ce guide vous guide tout au long de la configuration de toutes les conditions préalables requises pour l’API du client. Si vous disposez déjà de toutes vos informations d’identification et données, consultez la [configuration d’une instance](./user-guide/configure.md)d’API client. Il décrit les étapes à suivre pour utiliser l’API du client.
---
keywords: personnalisation de la cible ; destination; destination de la cible de la plateforme d’expérience;destination adobe target;
title: Connexion Adobe Target
description: Adobe Target est une application qui fournit des fonctionnalités de personnalisation et d’expérimentation optimisées par l’IA en temps réel dans toutes les interactions client entrantes entre sites web, applications mobiles, etc.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: fb79d0697244518cc713efeada7d017d64ce6214
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 8%

---

# Connexion Adobe Target {#adobe-target-connection}

## Présentation {#overview}

Adobe Target est une application qui fournit des fonctionnalités de personnalisation et d’expérimentation optimisées par l’IA en temps réel dans toutes les interactions client entrantes entre sites web, applications mobiles, etc.

Adobe Target est une connexion de personnalisation dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Cette intégration est optimisée par la fonction [SDK Web Adobe Experience Platform](../../../edge/home.md). Vous devez utiliser ce SDK pour utiliser cette destination.

## Type d&#39;export {#export-type}

**Requête de profil** - vous demandez tous les segments mappés dans la destination Adobe Target pour un profil unique.

## Cas dʼutilisation {#use-cases}

**Personnaliser une bannière de page d&#39;accueil**

Une société de location et de vente d’habitations souhaite personnaliser sa page d’accueil avec une bannière, en fonction des qualifications de segment client dans Adobe Experience Platform. L’entreprise peut sélectionner les audiences qui doivent bénéficier d’une expérience personnalisée et les envoyer à Adobe Target en tant que critères de ciblage pour son offre Target.

## Connexion à la destination {#connect}

>[!IMPORTANT]
>
>Avant de créer un [!DNL Adobe Target] connexion, nous vous recommandons de lire notre guide sur la façon de [configuration des destinations de personnalisation pour la personnalisation de la même page et de la page suivante](../../ui/configure-personalization-destinations.md). Ce guide vous guide tout au long des étapes de configuration requises pour les cas d’utilisation de la personnalisation de la même page et de la page suivante, sur plusieurs composants Experience Platform.

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="À propos des identifiants de flux de données"
>abstract="Cette option détermine dans quel jeu de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Vous devez configurer un flux de données avant de pouvoir configurer votre destination."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Découvrez comment configurer un flux de données."

Pour vous connecter à cette destination, procédez comme décrit dans la section [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Adobe Experience Platform se connecte automatiquement à l’instance Adobe Target de votre entreprise. Aucune authentification n’est requise.

### Paramètres de connexion {#parameters}

while [configuration](../../ui/connect-destination.md) Pour cette destination, vous devez fournir les informations suivantes :

* **Nom** : renseignez le nom de votre choix pour cette destination.
* **Description** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **Identifiant du flux de données**: Cela détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configuration d’un flux de données](../../../edge/fundamentals/datastreams.md) pour plus d’informations.

## Activation des segments vers cette destination {#activate}

Lecture [Activation des profils et des segments vers les destinations de requête de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Adobe Target lit les données de profil du réseau Adobe Experience Platform Edge, de sorte qu’aucune donnée n’est exportée.

## Utilisation et gouvernance des données {#data-usage-governance}

Tous [!DNL Adobe Experience Platform] Les destinations sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour obtenir des informations détaillées sur la manière dont [!DNL Adobe Experience Platform] applique la gouvernance des données, lisez la section [Présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

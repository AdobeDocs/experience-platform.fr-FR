---
keywords: personnalisation de la cible ; destination; destination de la cible de la plateforme d’expérience;destination adobe target;
title: Connexion Adobe Target (bêta)
description: Adobe Target est une application qui fournit une personnalisation et une expérimentation optimisées par l’intelligence artificielle, en temps réel et 1:1 dans toutes les interactions client entrantes entre sites web, applications mobiles, etc.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: ba27484655438df654a1e062309ddd30638f62a5
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 11%

---

# Connexion Adobe Target (bêta) {#adobe-target-connection}

## Présentation {#overview}

>[!IMPORTANT]
>
>La connexion Adobe Target dans Adobe Experience Platform est actuellement en version bêta. La documentation et la fonctionnalité peuvent changer.

Adobe Target est une application qui fournit une personnalisation et une expérimentation en temps réel, 1:1, optimisées par l’IA, dans toutes les interactions client entrantes entre sites web, applications mobiles, etc.

Adobe Target est une connexion de personnalisation dans Adobe Experience Platform.

## Conditions préalables {#prerequisites}

Cette intégration est optimisée par le [SDK Web Adobe Experience Platform](../../../edge/home.md). Vous devez utiliser ce SDK pour utiliser cette destination.

## Type d&#39;export {#export-type}

**Requête de profil**  : vous demandez tous les segments mappés dans la destination Adobe Target pour un seul profil.

## Cas d&#39;utilisation {#use-cases}

**Personnaliser une bannière de page d&#39;accueil**

Une société de location et de vente d’habitations souhaite personnaliser sa page d’accueil avec une bannière, en fonction des qualifications de segment client dans Adobe Experience Platform. L’entreprise peut sélectionner les audiences qui doivent bénéficier d’une expérience personnalisée et les envoyer à Adobe Target en tant que critères de ciblage pour son offre Target.

## Connexion à la destination {#connect}

Pour vous connecter à cette destination, suivez les étapes décrites dans le [tutoriel sur la configuration des destinations](../../ui/connect-destination.md).

Adobe Experience Platform se connecte automatiquement à l’instance Adobe Target de votre entreprise. Aucune authentification n’est requise.

### Paramètres de connexion {#parameters}

Lors de la configuration de [](../../ui/connect-destination.md) cette destination, vous devez fournir les informations suivantes :

* **Nom** : renseignez le nom de votre choix pour cette destination.
* **Description** : saisissez une description pour votre destination. Vous pouvez, par exemple, mentionner la campagne pour laquelle vous utilisez cette destination. Ce champ est facultatif.
* **Identifiant** de la banque de données : Cela détermine dans quel flux de données de collecte de données les segments seront inclus dans la réponse à la page. Le menu déroulant affiche uniquement les flux de données pour lesquels la configuration de destination est activée. Voir [Configuration d’un flux de données](../../../edge/fundamentals/datastreams.md) pour plus d’informations.

## Activation des segments vers cette destination {#activate}

Voir [Activation des profils et des segments vers les destinations de demande de profil](../../ui/activate-profile-request-destinations.md) pour obtenir des instructions sur l’activation des segments d’audience vers cette destination.

## Données exportées {#exported-data}

Adobe Target lit les données de profil du réseau Adobe Experience Platform Edge, de sorte qu’aucune donnée n’est exportée.

## Utilisation et gouvernance des données {#data-usage-governance}

Toutes les destinations [!DNL Adobe Experience Platform] sont conformes aux politiques d’utilisation des données lors de la gestion de vos données. Pour plus d’informations sur la façon dont [!DNL Adobe Experience Platform] applique la gouvernance des données, consultez la [présentation de la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

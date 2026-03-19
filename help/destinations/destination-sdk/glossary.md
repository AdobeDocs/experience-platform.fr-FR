---
solution: Experience Platform
title: Glossaire Adobe Experience Platform Destination SDK
description: comprendre la terminologie importante lors de la création d’une destination à l’aide d’Experience Platform Destination SDK ;
exl-id: d65f390a-a980-49b8-9570-840f03534553
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 3%

---

# Glossaire Adobe Experience Platform Destination SDK

Reportez-vous à ce glossaire pour connaître la définition des termes utilisés dans Destination SDK. Pour d’autres termes Adobe Experience Platform, reportez-vous au glossaire [Experience Platform](/help/landing/glossary.md).

## A {#a}

**Politique d’agrégation** : lors de la configuration de la manière dont les données doivent être exportées vers votre destination de diffusion en continu en temps réel, vous pouvez définir la manière dont les données de profil sont agrégées avant d’être envoyées à votre plateforme de destination. Cela permet d’optimiser la diffusion des données en regroupant les enregistrements de données en fonction de critères spécifiques, en réduisant la fréquence des appels API et en améliorant l’efficacité globale. Différentes politiques peuvent être configurées pour répondre aux différentes exigences de destination, afin de s’assurer que les données sont compilées et diffusées de la manière la plus efficace possible. [En savoir plus](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Configuration des métadonnées d’audience** : une configuration de métadonnées d’audience fait référence à la configuration structurée et aux paramètres définis dans Adobe Experience Platform qui permettent la création, la mise à jour et la suppression par programmation de segments d’audience dans une destination spécifiée. Cette configuration utilise des modèles de métadonnées d’audience pour s’aligner sur les spécifications de l’API marketing de la plateforme de destination. En savoir plus sur la [configuration des métadonnées d’audience](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) et les [macros disponibles](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D {#d}

**Point d’entrée de configuration de destination** : un point d’entrée de configuration de destination dans Adobe Experience Platform, en particulier le point d’entrée de l’API `/authoring/destinations`, est utilisé pour créer, récupérer, mettre à jour et supprimer des configurations pour les destinations. Ces configurations définissent la manière dont les données de Adobe Experience Platform sont diffusées à divers systèmes ou destinations externes, tels que des plateformes marketing, des services de stockage dans le cloud ou d’autres points d’entrée de traitement des données. Lisez davantage sur les [options de configuration disponibles](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) et consultez la [documentation de référence](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Instance de destination** : configuration spécifique d’une configuration de destination dans Adobe Experience Platform, créée et gérée via l’interface utilisateur Experience Platform. Elle comprend tous les paramètres et informations d’identification nécessaires pour connecter et envoyer des données à la destination . Après avoir établi la connexion à la destination, vous pouvez obtenir l’identifiant d’instance de destination lors de l’[exploration d’une connexion avec la destination](/help/destinations/ui/destination-details-page.md).

![Image de l’interface illustrant comment obtenir l’identifiant d’instance de destination](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P {#p}

**[!DNL Pebble]modèle** : un modèle de [!DNL Pebble] est utilisé pour transformer les données exportées depuis Adobe Experience Platform au format requis par la plateforme de destination. Il utilise le langage de modèle [!DNL Pebble], qui permet la transformation dynamique des données par le biais de fonctions telles que `filter`, `for`, `if` et `set`. Adobe Experience Platform comprend d’autres fonctions personnalisées telles que `addedSegments` et `removedSegments`. Ces modèles permettent de formater les éléments de données, tels que les horodatages et les appartenances à l’audience, pour répondre aux spécifications de la destination. En savoir plus [ici](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) et [ici](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Destination privée** : intégrations personnalisées créées par des clients Adobe Experience Platform individuels. Ils sont adaptés aux besoins spécifiques de l’entreprise et ne sont accessibles qu’au sein de l’organisation du client, offrant ainsi une flexibilité dans les configurations d’exportation de données. Les destinations privées sont disponibles uniquement pour les clients Real-Time CDP Ultimate. [En savoir plus](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Destination publique** : intégration accessible au public dans le catalogue Adobe Experience Platform. Ces destinations sont normalisées, de marque et simplifient la configuration des clients en fournissant des paramètres préconfigurés. Ils sont accessibles à tous les clients qui utilisent Adobe Experience Platform. [En savoir plus](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S {#s}

**Modèle de documentation en libre-service** : le modèle de documentation en libre-service fournit un format structuré que vous pouvez utiliser pour documenter la destination. Elle comprend des sections pour une présentation, les cas d’utilisation, les conditions préalables, les identités prises en charge, les audiences, les types d’exportation et la fréquence, ainsi que les étapes de connexion à la destination, d’activation des audiences et de mappage des attributs. Utilisez ce modèle pour garantir une documentation complète et cohérente, ce qui permet aux clients de commencer rapidement à utiliser votre destination et de comprendre les cas d’utilisation fournis. En savoir plus sur [comment documenter la destination](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [télécharger le dernier modèle de documentation en libre-service](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip) et [en afficher le rendu](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T {#t}

**Spécifications de modèle et stratégies de modèle** : les spécifications de modèle sont des configurations utilisées pour formater les requêtes HTTP envoyées de Adobe Experience Platform vers une destination. Ils transforment les champs d’attribut de profil du schéma XDM en un format pris en charge par la plateforme de destination. En utilisant un langage de modèle similaire à [!DNL Jinja], ces spécifications permettent des transformations de données dynamiques basées sur des règles spécifiques et des données d’entrée. [En savoir plus](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**API de test** : l’API de test vous permet de valider les configurations de destination avant d’envoyer une demande de publication. Il fournit des outils pour générer des profils types et tester le flux de données, en s’assurant que la configuration correspond aux exigences de la destination. L’API prend en charge les destinations en flux continu et basées sur des fichiers (par lots), offrant un moyen de simuler les données et de résoudre les problèmes potentiels dans le processus de configuration. En savoir plus sur l’API de test pour les destinations [en flux continu](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) et [basées sur des fichiers](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Modèle de transformation** : un modèle de transformation personnalise le format des données du schéma XDM d’Adobe au format attendu de la destination. [En savoir plus](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).

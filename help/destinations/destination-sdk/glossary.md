---
solution: Experience Platform
title: Glossaire Adobe Experience Platform Destination SDK
description: Découvrez la terminologie importante lorsque vous créez une destination à l’aide de la Destination SDK Experience Platform.
source-git-commit: 3dae91fbe46dc3e23c6ac0cfb10c25ac8473876a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 3%

---


# Glossaire Adobe Experience Platform Destination SDK

Reportez-vous à ce glossaire pour connaître la définition des termes utilisés dans Destination SDK. Pour les autres termes Adobe Experience Platform, reportez-vous à la section [Glossaire Experience Platform](/help/landing/glossary.md).

## A

**Stratégie d’agrégation**: lors de la configuration de la manière dont les données doivent être exportées vers votre destination de diffusion en continu en temps réel, vous pouvez définir la manière dont les données de profil sont agrégées avant d’être envoyées à votre plateforme de destination. Cela permet d’optimiser la remise des données en regroupant les enregistrements de données selon des critères spécifiques, en réduisant la fréquence des appels API et en améliorant l’efficacité globale. Différentes stratégies peuvent être configurées pour répondre à diverses exigences de destination, en veillant à ce que les données soient empaquetées et diffusées de la manière la plus efficace possible. [En savoir plus](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Configuration des métadonnées d’audience**: une configuration de métadonnées d’audience fait référence à la configuration structurée et aux paramètres définis dans Adobe Experience Platform qui permettent la création, la mise à jour et la suppression programmatiques de segments d’audience dans une destination spécifiée. Cette configuration utilise des modèles de métadonnées d’audience pour s’aligner sur les spécifications de l’API marketing de la plateforme de destination. En savoir plus sur les [configuration des métadonnées d’audience](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) et [macros disponibles](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Point d’entrée de configuration de la destination**: un point de terminaison de configuration de destination dans Adobe Experience Platform, en particulier la variable `/authoring/destinations` Le point de terminaison de l’API est utilisé pour créer, récupérer, mettre à jour et supprimer des configurations pour les destinations. Ces configurations définissent la manière dont les données de Adobe Experience Platform sont diffusées à divers systèmes ou destinations externes, tels que les plateformes marketing, les services de stockage dans le cloud ou d’autres points de terminaison de traitement des données. En savoir plus sur [options de configuration disponibles](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) et affichez le [documentation de référence](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Instance de destination**: configuration spécifique d’une configuration de destination dans Adobe Experience Platform, créée et gérée via l’interface utilisateur Experience Platform. Il comprend tous les paramètres et informations d’identification nécessaires pour se connecter et envoyer des données à la destination. Après avoir établi la connexion à votre destination, vous pouvez obtenir l’ID d’instance de destination lorsque [parcourir une connexion avec votre destination ;](/help/destinations/ui/destination-details-page.md).

![Image de l’interface illustrant comment obtenir l’identifiant d’instance de destination](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]modèle**: A [!DNL Pebble] est utilisé pour transformer les données exportées à partir de Adobe Experience Platform au format requis par la plateforme de destination. Elle emploie le [!DNL Pebble] langage de modèle, qui permet une transformation dynamique des données par le biais de fonctions telles que `filter`, `for`, `if`, et `set`. Adobe Experience Platform inclut d’autres fonctions personnalisées, telles que `addedSegments` et `removedSegments`. Ces modèles permettent de formater des éléments de données, tels que les horodatages et les appartenances à l’audience, afin de répondre aux spécifications de la destination. En savoir plus [here](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) et [here](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Destination privée**: intégrations personnalisées créées par des clients Adobe Experience Platform individuels. Elles sont adaptées aux besoins spécifiques de l’entreprise et ne sont accessibles que par l’entreprise du client, ce qui offre une certaine souplesse dans les configurations d’exportation des données. Les destinations privées sont disponibles uniquement pour les clients Real-Time CDP Ultimate. [En savoir plus](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Destination publique**: intégration disponible publiquement dans le catalogue Adobe Experience Platform. Ces destinations sont normalisées, marquées et simplifient la configuration client en fournissant des paramètres préconfigurés. Ils sont accessibles à tous les clients qui utilisent Adobe Experience Platform. [En savoir plus](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Modèle de documentation en libre-service**: le modèle de documentation en libre-service fournit un format structuré que vous pouvez utiliser pour documenter votre destination. Elle comprend des sections pour un aperçu, des cas d’utilisation, des conditions préalables, des identités prises en charge, des audiences, des types d’exportation et de la fréquence, ainsi que des étapes pour se connecter à la destination, activer des audiences et mapper des attributs. Utilisez ce modèle pour garantir une documentation complète et cohérente, ce qui permet aux clients de commencer rapidement à utiliser votre destination et de comprendre les cas d’utilisation fournis. En savoir plus sur [Comment documenter votre destination](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [télécharger le dernier modèle de documentation en libre-service](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip), et [afficher le mode de rendu ;](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Spécifications des modèles et stratégies de création de modèles**: les spécifications de modèle sont des configurations utilisées pour formater les requêtes HTTP envoyées de Adobe Experience Platform vers une destination. Ils transforment les champs d’attribut de profil du schéma XDM en un format pris en charge par la plateforme de destination. Utilisation d’un langage de modèle similaire à [!DNL Jinja], ces spécifications permettent des transformations de données dynamiques basées sur des règles spécifiques et des données d’entrée. [En savoir plus](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Test de l’API**: l’API de test vous permet de valider vos configurations de destination avant d’envoyer une demande de publication. Il fournit des outils pour générer des exemples de profils et tester le flux de données, en s’assurant que la configuration correspond aux exigences de la destination. L’API prend en charge les destinations (par lot) basées sur des fichiers et sur des diffusions en continu, ce qui permet de simuler les données et de résoudre les problèmes potentiels du processus de configuration. En savoir plus sur l’API de test pour [flux continu](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) et [destinations basées sur des fichiers](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Modèle de transformation**: un modèle de transformation personnalise le format des données du schéma XDM Adobe au format attendu de la destination. [En savoir plus](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).
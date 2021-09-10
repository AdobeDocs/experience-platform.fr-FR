---
description: Le service de destinations dans Adobe Experience Platform utilise des modèles de configuration pour plusieurs composants qui créent la fonctionnalité de destinations. Combinés, ces composants permettent à l’Experience Platform de se connecter à des partenaires de destination, d’envoyer des messages personnalisés et d’activer des données de profil dans l’écosystème numérique.
seo-description: The destinations service in Adobe Experience Platform uses configuration templates for several components that build up the destinations functionality. Combined, these components allow Experience Platform to connect to destination partners, send custom messages, and activate profile data across the digital ecosystem.
seo-title: Configuration options in Destination SDK
title: Options de configuration dans le SDK de destination
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# Options de configuration dans le SDK de destination

## Présentation {#overview}

Le service de destinations dans Adobe Experience Platform utilise des modèles de configuration pour plusieurs composants qui créent la fonctionnalité de destinations. Combinés, ces composants permettent à l’Experience Platform de se connecter à des partenaires de destination, d’envoyer des messages personnalisés et d’activer des données de profil dans l’écosystème numérique. Les modèles utilisés dans Adobe Experience Platform sont les suivants :

* **Configuration** de la destination : Contient des informations de base sur votre destination. Cette configuration inclut les types d’identité que votre destination peut prendre en charge, ainsi que divers attributs d’interface utilisateur pour votre carte de destination dans l’interface utilisateur de Adobe Experience Platform.
* **Spécifications du serveur et des modèles** : Associe les informations sur les spécifications de votre serveur et le modèle utilisé par Adobe pour diffuser les payloads vers votre destination.
   * **Spécifications** du serveur : Un modèle qui stocke les détails de votre point de terminaison.
   * **Spécifications des modèles** : Dans ce modèle, vous pouvez définir comment transformer les champs d’attribut de profil entre le schéma XDM et le format pris en charge par votre plateforme. Pour plus d’informations sur les langues de modèle prises en charge, les formats de message et les informations requises par Adobe pour configurer l’intégration avec votre plateforme, consultez [Format du message](./message-format.md).
* **Configuration** d’authentification : Ces paramètres définissent la manière dont les utilisateurs de Adobe Experience Platform se connectent à votre destination.
* **Configuration** des métadonnées d’audience : Ce modèle vous permet de configurer la manière dont les audiences/segments sont créés, mis à jour ou supprimés par programmation dans votre destination.

![Modèles et configurations du SDK de destination](./assets/self-service-configuration.png)

## Liens connexes {#related-links}

Les pages ci-dessous fournissent plus de détails sur les fonctionnalités et les options de configuration disponibles dans le SDK de destination, ainsi que sur les opérations API correspondantes que vous pouvez effectuer.

| Description des fonctionnalités | Référence d’API |
|--- |--- |
| [Configuration de la destination](./destination-configuration.md) | [Opérations de point d’entrée de l’API Destinations](./destination-configuration-api.md) |
| [Spécifications du serveur et des modèles](./server-and-template-configuration.md) | [Opérations de point d’entrée de l’API des serveurs de destination](./destination-server-api.md) |
| [Configuration de l’authentification](./credentials-configuration.md) | [Opérations de l’API du point d’entrée des informations d’identification](./credentials-configuration-api.md) |
| [Gestion des métadonnées d’audience](./audience-metadata-management.md) | [Opérations de l’API de point d’entrée des métadonnées d’audience](./audience-metadata-api.md) |
| [Configuration OAuth 2](./oauth2-authentication.md) | Configurez à l’aide du paramètre `customerAuthenticationConfigurations` dans le point d’entrée de l’API [/destinations](./destination-configuration-api.md). |
| [Format du message](./message-format.md) | - |
| [Test de destination](./test-destination.md) | [Opérations de l’API de test de destination](./destination-testing-api.md) |
| [Publication de destination](./configure-destination-instructions.md#publish-destination) | [Opérations de l’API de publication de destination](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}

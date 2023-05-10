---
description: Le service de destinations dans Adobe Experience Platform utilise des points de terminaison de configuration pour plusieurs composants qui créent la fonctionnalité de destinations. Combinés, ces composants permettent à l’Experience Platform de se connecter à des partenaires de destination, d’envoyer des messages personnalisés et d’activer des données de profil dans l’écosystème numérique.
title: Options de configuration dans Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 7%

---

# Options de configuration dans Destination SDK

## Présentation {#overview}

Le service de destinations dans Adobe Experience Platform utilise des points de terminaison de configuration pour plusieurs composants qui créent la fonctionnalité de destinations. Combinés, ces composants permettent à l’Experience Platform de se connecter aux plateformes de destination, d’envoyer des messages personnalisés, d’exporter des fichiers personnalisés et d’activer des données de profil dans l’écosystème numérique. Les configurations utilisées en Adobe Experience Platform Destination SDK sont les suivantes :

* **Configuration de la destination**: Contient des informations de base sur votre destination. Cette configuration comprend les types d’identité que votre destination peut prendre en charge, le format souhaité des fichiers exportés (pour les destinations basées sur des fichiers) et divers attributs d’interface utilisateur pour votre carte de destination dans l’interface utilisateur de Adobe Experience Platform.
* **Spécifications relatives au serveur, au fichier et au modèle**: Associe les informations sur les spécifications de votre serveur et le modèle utilisé par Adobe pour diffuser les payloads vers votre destination. Pour les destinations basées sur des fichiers, cette configuration inclut également les formats de formatage et de compression de fichiers pris en charge pour votre destination.
   * **Spécifications du serveur**: Un modèle de configuration contenant des informations sur l’emplacement de stockage ou le point de terminaison HTTP vers lequel les données sont envoyées.&quot;
   * **Spécifications de fichier**: Un modèle de configuration qui inclut les options de formatage et de compression de fichiers pour votre destination de lot.
   * **Spécifications des modèles**: Dans ce modèle, vous pouvez définir comment transformer les champs d’attribut de profil entre le schéma XDM et le format pris en charge par votre plateforme. Pour plus d’informations sur les langues de modèle prises en charge, les formats de message et les informations requises par Adobe pour configurer l’intégration avec votre plateforme, consultez la rubrique [Format du message](./message-format.md).
* **Configuration de l’authentification**: Ces paramètres définissent la manière dont les utilisateurs de Adobe Experience Platform se connectent à votre destination.
* **Configuration des métadonnées d’audience**: Ce point de terminaison de configuration vous permet de configurer la manière dont les audiences/segments sont créés, mis à jour ou supprimés par programmation dans votre destination. Pour les destinations par lot, il vous permet de configurer une notification chaque fois que les fichiers sont correctement diffusés vers votre destination.

![Diagramme montrant les points de terminaison de la configuration de la Destination SDK et leur utilisation conjointe.](./assets/self-service-configuration.png)

## Liens connexes {#related-links}

Les pages ci-dessous fournissent plus de détails sur la fonctionnalité et les options de configuration disponibles dans Destination SDK, ainsi que sur les opérations API correspondantes que vous pouvez effectuer.

| Description des fonctionnalités (destinations de diffusion en continu) | Description des fonctionnalités (destinations par lots) | Référence d’API |
|--- |--- |--- |
| [Options de configuration des destinations](./destination-configuration.md) | [Options de configuration des destinations basées sur des fichiers](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [Opérations de point d’entrée de l’API Destinations](./destination-configuration-api.md) |
| [Spécifications du serveur et des modèles](./server-and-template-configuration.md) | [Spécifications relatives à la configuration du serveur et des fichiers](/help/destinations/destination-sdk/server-and-file-configuration.md) | [Opérations de point d’entrée de l’API des serveurs de destination](./destination-server-api.md) |
| [Configuration de l’authentification](./authentication-configuration.md) | Identique aux destinations de diffusion en continu. | Vous pouvez configurer les informations d’authentification pour votre destination via les paramètres `customerAuthenticationConfigurations` du point d’entrée `/destinations`. Plus d’informations pour [diffusion en continu](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) et [batch](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) destinations. |
| [Gérer les métadonnées d’audience](./audience-metadata-management.md) | Comme pour la diffusion en continu. Voir [exemple basé sur les fichiers](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) pour comprendre comment les métadonnées d’audience peuvent être utilisées dans un contexte de destination par lots. | [Opérations de l’API du point d’entrée des métadonnées d’audience](./audience-metadata-api.md) |
| [Configuration OAuth 2](./oauth2-authentication.md) | Identique à pour les destinations de diffusion en continu | Configurez à l’aide de la fonction `customerAuthenticationConfigurations` du paramètre [Point d’entrée de l’API /destinations](./destination-configuration-api.md). |
| [Format des messages](./message-format.md) | - | - |
| [Outils de test pour les destinations de diffusion en continu](./test-destination.md) | [Outils de test pour les destinations basées sur des fichiers](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [Opérations de l’API pour les tests de destination](./destination-testing-api.md) |
| [Publication de destination](./configure-destination-instructions.md#publish-destination) | Identique à pour les destinations de diffusion en continu | [Opérations de l’API de publication de destination](./destination-publish-api.md) |

{style="table-layout:auto"}

## Étapes suivantes {#next-steps}

En lisant cet article, vous disposez désormais d’un aperçu général des fonctionnalités de Destination SDK et des pages à lire pour plus d’informations sur les configurations spécifiques. Vous pouvez ensuite lire les guides qui incluent toutes les étapes pour [configuration d’une diffusion en continu](/help/destinations/destination-sdk/configure-destination-instructions.md) ou [destination basée sur les fichiers](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) en utilisant Destination SDK.

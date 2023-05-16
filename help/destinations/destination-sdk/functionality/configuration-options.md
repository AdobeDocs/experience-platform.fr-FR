---
description: Le service de destinations dans Adobe Experience Platform utilise des points de terminaison de configuration pour plusieurs composants qui créent la fonctionnalité de destinations. Découvrez comment ces composants combinés permettent à l’Experience Platform de se connecter à des partenaires de destination, d’envoyer des messages personnalisés et d’activer des données de profil dans l’écosystème numérique.
title: Options de configuration dans Destination SDK
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Options de configuration dans Destination SDK

Le service de destinations dans Adobe Experience Platform utilise des points de terminaison de configuration pour plusieurs composants qui créent la fonctionnalité de destinations.

Combinés, ces composants permettent à l’Experience Platform de se connecter aux plateformes de destination, d’envoyer des messages personnalisés, d’exporter des fichiers personnalisés et d’activer des données de profil dans l’écosystème numérique.

Le diagramme ci-dessous présente un aperçu général des composants que vous pouvez configurer via Destination SDK pour créer votre propre destination. Ces composants sont décrits plus loin ci-dessous.

![Diagramme présentant les composants de Destination SDK, les points de terminaison de configuration et les opérations pris en charge par ceux-ci.](../assets/functionality/destination-sdk-components-diagram.png)

## Configuration du serveur {#server-configuration}

La configuration du serveur de destination associe les informations sur les spécifications de votre serveur et le modèle utilisé par Adobe pour diffuser les payloads vers votre destination.

Par exemple, c’est là que vous spécifiez les points de terminaison d’API de votre côté auxquels l’Experience Platform doit se connecter, ainsi que les en-têtes et le format des appels d’API que Platform effectuera.

Pour les destinations basées sur des fichiers, cette configuration inclut également les formats de formatage et de compression de fichiers pris en charge pour votre destination. Vous pouvez configurer les fonctionnalités décrites ci-dessous à l’aide du [point d’entrée destination-servers](../authoring-api/destination-server/create-destination-server.md).

* [Spécifications du serveur](destination-server/server-specs.md): Un modèle de configuration contenant des informations sur l’emplacement de stockage ou le point de terminaison HTTP vers lequel les données sont envoyées.
* [Spécifications des modèles](destination-server/templating-specs.md): Dans ce modèle, vous pouvez définir comment structurer la requête d’API HTTP sur votre point de terminaison, y compris comment transformer les champs d’attribut de profil entre le schéma XDM et le format pris en charge par votre plateforme. Utilisez ces informations avec la variable [format du message](destination-server/message-format.md) documentation.
* [Format du message](destination-server/message-format.md): Cette section traite des informations détaillées sur les langues de modèle prises en charge, les formats de message et les informations requises par Adobe pour configurer l’intégration à votre plateforme. Utilisez ces informations avec la variable [spécifications des modèles](destination-server/templating-specs.md) documentation.
* [Spécifications de fichier](destination-server/file-formatting.md): Un modèle de configuration qui inclut les options de formatage et de compression de fichiers pour votre destination de lot.

## Configuration de la destination {#destination-configuration}

Ce point de terminaison de configuration contient des informations de base et avancées sur votre destination. Par exemple, c’est là que vous spécifiez les types d’identité que votre destination peut prendre en charge, le format souhaité des fichiers exportés (pour les destinations basées sur des fichiers) et divers attributs d’interface utilisateur pour votre carte de destination dans l’interface utilisateur de Adobe Experience Platform.

Consultez la documentation ci-dessous pour plus d’informations sur chacun des composants de configuration de destination. Vous pouvez configurer les fonctionnalités décrites ci-dessous à l’aide du [point d’entrée des destinations](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuration de l’authentification du client](destination-configuration/customer-authentication.md): Sélectionnez le mécanisme d’authentification que l’Experience Platform doit utiliser pour se connecter à votre destination. Cette configuration génère la variable [Configuration d’une nouvelle destination](../../ui/connect-destination.md) dans l’interface utilisateur de l’Experience Platform, où les utilisateurs se connectent Experience Platform aux comptes qu’ils possèdent avec votre destination.
* [Authentification OAuth2](destination-configuration/oauth2-authentication.md): En savoir plus sur tous les [!DNL OAuth2] flux d’authentification pris en charge par Destination SDK et obtention d’instructions pour la configuration [!DNL OAuth2] l’authentification pour votre destination.
* [Champs de données client](destination-configuration/customer-data-fields.md): Découvrez comment créer des champs de saisie dans l’interface utilisateur de l’Experience Platform qui permettent à vos utilisateurs de spécifier diverses informations relatives à la connexion et à l’exportation des données vers votre destination.
* [Attributs de l’interface utilisateur](destination-configuration/ui-attributes.md): Découvrez comment configurer les attributs de l’interface utilisateur, tels que le lien de documentation, la catégorie de carte de destination, ainsi que le type et la fréquence de connexion à la destination, pour les destinations créées avec Destination SDK.
* [Configuration du schéma](destination-configuration/schema-configuration.md): Découvrez comment définir le schéma cible de votre destination vers lequel les utilisateurs peuvent mapper les attributs et les identités de profil.
* [Configuration de l’espace de noms d’identité](destination-configuration/identity-namespace-configuration.md): Découvrez comment configurer les identités prises en charge par votre destination. Cette configuration renseigne les identités de la cible dans la variable [étape de mappage](../../ui/activate-segment-streaming-destinations.md#mapping) de l’interface utilisateur de l’Experience Platform, où les utilisateurs mappent les identités et les attributs de leurs schémas XDM au schéma de votre destination.
* [Diffusion de destination](destination-configuration/destination-delivery.md): Découvrez comment configurer l’emplacement exact des données exportées et la règle d’authentification utilisée à l’emplacement d’entrée des données.
* [Configuration des métadonnées d’audience](destination-configuration/audience-metadata-configuration.md): Découvrez comment les métadonnées de segment telles que les noms de segment ou les identifiants doivent être partagées entre l’Experience Platform et votre destination.
* [Stratégie d’agrégation](destination-configuration/aggregation-policy.md): Découvrez comment configurer une stratégie d’agrégation pour déterminer comment les requêtes HTTP vers votre destination doivent être groupées et regroupées par lot.
* [Configuration par lots](destination-configuration/batch-configuration.md): Configurez divers paramètres de dénomination de fichier et de planification de l’exportation disponibles pour les utilisateurs lors de la connexion à votre destination dans l’interface utilisateur de l’Experience Platform.
* [Qualifications des profils historiques](destination-configuration/historical-profile-qualifications.md): Découvrez les qualifications de profil historiques prises en charge par les destinations créées avec Destination SDK.

## Configuration des métadonnées d’audience {#audience-metadata-configuration}

Ce composant vous permet de configurer la manière dont les audiences/segments sont créés, mis à jour ou supprimés par programmation dans votre destination. Pour les destinations basées sur des fichiers, il vous permet de configurer une notification chaque fois que les fichiers sont correctement diffusés vers votre destination. Vous pouvez configurer cette fonctionnalité à partir du [point d’entrée audience-templates](../metadata-api/create-audience-template.md).

## Étapes suivantes {#next-steps}

En lisant cet article, vous disposez désormais d’un aperçu général des fonctionnalités de Destination SDK et des pages à lire pour plus d’informations sur les configurations spécifiques. Vous pouvez ensuite lire les guides qui incluent toutes les étapes pour [configuration d’une diffusion en continu](../guides/configure-destination-instructions.md) ou [destination basée sur les fichiers](../guides/configure-file-based-destination-instructions.md) en utilisant Destination SDK.

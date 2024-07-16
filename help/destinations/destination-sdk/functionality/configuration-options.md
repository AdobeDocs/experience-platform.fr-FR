---
description: Le service de destinations dans Adobe Experience Platform utilise des points d’entrée de configuration pour plusieurs composants qui créent la fonctionnalité de destinations. Découvrez comment ces composants combinés permettent à Experience Platform de se connecter à des partenaires de destination, d’envoyer des messages personnalisés et d’activer des données de profil dans l’écosystème numérique.
title: Options de configuration dans Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 97%

---

# Options de configuration dans Destination SDK

Le service de destinations dans Adobe Experience Platform utilise des points d’entrée de configuration pour plusieurs composants qui créent la fonctionnalité de destinations.

Combinés, ces composants permettent à Experience Platform de se connecter à des plateformes de destination, d’envoyer des messages personnalisés, d’exporter des fichiers personnalisés et d’activer des données de profil dans l’écosystème numérique.

Le diagramme ci-dessous donne une vue d’ensemble sur les composants que vous pouvez configurer avec Destination SDK pour créer votre propre destination. Ces composants sont décrits plus en détail ci-après.

![Diagramme présentant les composants de Destination SDK, les points d’entrée de configuration et les opérations pris en charge par ceux-ci.](../assets/functionality/destination-sdk-components-diagram.png)

## Configuration du serveur {#server-configuration}

La configuration du serveur de destination associe les informations sur les spécifications de votre serveur et le modèle utilisé par Adobe pour diffuser les payloads vers la destination.

Par exemple, c’est là que vous spécifiez les points d’entrée API de votre côté auxquels Experience Platform doit se connecter, ainsi que les en-têtes et le format des appels API que Platform effectuera.

Pour les destinations basées sur des fichiers, cette configuration inclut également les formats de formatage et de compression de fichiers pris en charge pour la destination. Vous pouvez configurer les fonctionnalités décrites ci-dessous via le [point d’entrée destination-serveur](../authoring-api/destination-server/create-destination-server.md).

* [Spécifications du serveur](destination-server/server-specs.md) : un modèle de configuration contenant des informations sur l’emplacement de stockage ou le point d’entrée HTTP vers lequel les données sont envoyées.
* [Spécifications du modèle](destination-server/templating-specs.md) : dans ce modèle, vous pouvez définir comment structurer la requête API HTTP sur le point d’entrée, notamment comment transformer les champs d’attribut de profil entre le schéma XDM et le format pris en charge par votre plateforme. Utilisez ces informations avec la documentation du [format du message](destination-server/message-format.md).
* [Format du message](destination-server/message-format.md) : cette section traite des informations détaillées sur les langues de modèle prises en charge, les formats de message et les informations demandées par Adobe pour configurer l’intégration à la plateforme. Utilisez ces informations avec la documentation des [spécifications du modèle](destination-server/templating-specs.md).
* [Spécifications du fichier](destination-server/file-formatting.md) : un modèle de configuration qui inclut les options de formatage et de compression de fichiers pour la destination par lots.

## Configuration de la destination {#destination-configuration}

Ce point d’entrée de configuration contient des informations de base et avancées sur la destination. Par exemple, c’est là que vous spécifiez les types d’identité que la destination peut prendre en charge, le format souhaité des fichiers exportés (pour les destinations basées sur des fichiers) et divers attributs d’interface utilisateur pour la carte de destination dans l’interface utilisateur d’Adobe Experience Platform.

Pour en savoir plus sur chacun des composants de configuration de destination, consultez la documentation ci-dessous. Vous pouvez configurer les fonctionnalités décrites ci-dessous via le [point d’entrée des destinations](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuration de l’authentification du client](destination-configuration/customer-authentication.md) : sélectionnez le mécanisme d’authentification qu’Experience Platform doit utiliser pour se connecter à la destination. Cette configuration génère la page [Configurer une nouvelle destination](../../ui/connect-destination.md) dans l’interface utilisateur d’Experience Platform, où les utilisateurs connectent Experience Platform aux comptes qu’ils possèdent avec la destination.
* [Autorisation OAuth2](destination-configuration/oauth2-authorization.md) : découvrez tous les flux d’authentification [!DNL OAuth2] pris en charge par Destination SDK et obtenez des instructions pour configurer l’authentification [!DNL OAuth2] pour votre destination.
* [Champs de données client](destination-configuration/customer-data-fields.md) : découvrez comment créer des champs d’entrée dans l’interface utilisateur d’Experience Platform qui permettent à vos utilisateurs de spécifier diverses informations relatives à la connexion et à l’exportation des données vers la destination.
* [Attributs de l’interface utilisateur](destination-configuration/ui-attributes.md) : découvrez comment configurer les attributs de l’interface utilisateur, tels que le lien de documentation, la catégorie de carte de destination, ainsi que le type et la fréquence de connexion à la destination, pour les destinations créées avec Destination SDK.
* [Configuration du schéma](destination-configuration/schema-configuration.md) : découvrez comment définir le schéma cible de la destination vers lequel les utilisateurs peuvent mapper les attributs et les identités de profil.
* [Configuration de l’espace de noms d’identité](destination-configuration/identity-namespace-configuration.md) : découvrez comment configurer les identités prises en charge par la destination. Cette configuration renseigne les identités cibles dans l’[étape de mappage](../../ui/activate-segment-streaming-destinations.md#mapping) de l’interface utilisateur d’Experience Platform, où les utilisateurs mappent les identités et les attributs de leurs schémas XDM au schéma de la destination.
* [Diffusion de destination](destination-configuration/destination-delivery.md) : découvrez comment configurer l’emplacement exact des données exportées et la règle d’authentification utilisée à l’emplacement d’entrée des données.
* [Configuration des métadonnées d’audience](destination-configuration/audience-metadata-configuration.md) : découvrez comment les métadonnées d’audience, telles que les noms d’audience ou les identifiants, doivent être partagées entre Experience Platform et la destination.
* [Politique d’agrégation](destination-configuration/aggregation-policy.md) : découvrez comment configurer une politique d’agrégation pour déterminer comment les requêtes HTTP vers la destination doivent être groupées et regroupées par lot.
* [Configuration par lots](destination-configuration/batch-configuration.md) : configurez divers paramètres de dénomination de fichiers et de planification de l’exportation disponibles pour les utilisateurs au moment de la connexion à la destination dans l’interface utilisateur d’Experience Platform.
* [Qualifications des profils historiques](destination-configuration/historical-profile-qualifications.md) : découvrez les qualifications de profil historiques prises en charge par les destinations créées avec Destination SDK.

## Configuration des métadonnées d’audience {#audience-metadata-configuration}

Ce composant vous permet de configurer la manière dont les audiences sont créées, mises à jour ou supprimées par programmation dans la destination. Pour les destinations basées sur des fichiers, il vous permet de configurer une notification chaque fois que les fichiers sont correctement diffusés vers la destination. Vous pouvez configurer cette fonctionnalité via le [point d’entrée audience-modèles](../metadata-api/create-audience-template.md).

## Étapes suivantes {#next-steps}

Grâce à cet article, vous disposez désormais d’une vue d’ensemble sur les fonctionnalités de Destination SDK et des pages à lire pour plus d’informations sur les configurations spécifiques. Vous pouvez à présent lire les guides qui détaillent toutes les étapes pour [configurer une diffusion en streaming](../guides/configure-destination-instructions.md) ou une [destination basée sur les fichiers](../guides/configure-file-based-destination-instructions.md) à l’aide de Destination SDK.

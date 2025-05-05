---
description: Adobe Experience Platform Destination SDK est un ensemble d’API de configuration qui vous permet de configurer des modèles d’intégration de destination pour qu’Experience Platform diffuse des données d’audience et de profil vers votre point de terminaison ou emplacement de stockage, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 9c59f6edd51c61c1fe2ff69e0adea49e6efb8745
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 22%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK est une suite d’API de configuration qui vous permet de configurer des modèles d’intégration de destination pour qu’Experience Platform diffuse des données d’audience et de profil vers votre point de terminaison ou emplacement de stockage, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.

La documentation sur les Destinations SDK vous explique comment utiliser le Adobe Experience Platform Destination SDK pour configurer, tester et publier une intégration de destination productisée avec Adobe Experience Platform et faire en sorte que votre destination soit intégrée au catalogue des destinations en constante augmentation. En utilisant Destination SDK, vous pouvez également créer votre propre destination privée personnalisée pour exporter des données adaptées à vos besoins.

![Capture d’écran de l’interface utilisateur Experience Platform affichant le catalogue des destinations.](assets/destinations-catalog-overview.png)

## Démarrage rapide : découvrez les informations essentielles {#quick-start}

Consultez la documentation dans les liens ci-dessous pour commencer rapidement à configurer et envoyer votre destination via Destination SDK.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Pages de configuration</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">Toutes les options de configuration expliquées</a></li>
                <li> Configuration du serveur de destination - <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">spécifications du serveur</a> et <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">spécifications du modèle</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">Champs de données client et autres composants de configuration de destination</a></li>
                <li><a href="https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Modèles et macros</a></li>
            </ul>
        </td>
        <td>
            <p><b>Guides</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">Processus d’intégration de haut niveau</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Configurer une destination de diffusion en continu</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Configuration d’une destination basée sur des fichiers</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">Configuration d’une destination pour l’exportation de profils de prospect</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">Envoyer la destination pour publication</a></li>
            </ul>
        </td>
                <td>
            <p><b>Références API</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">Référence de l’API du point d’entrée du serveur de destination</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">Référence de l’API de point d’entrée de destination</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">Référence de l’API de métadonnées d’audience</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">Référence de l’API de test</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">Référence de l’API de publication de destination</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Configuration d’une destination de diffusion en continu - Aide-mémoire</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Configuration d’un guide de bout en bout de destination de diffusion en continu</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">Comprendre la transformation des données par le biais de modèles de bulle</a> et <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">afficher les fonctions de modèle prises en charge</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">Présentation des stratégies d’agrégation de données</a></li>
                <li><a href="https://experienceleague.adobe.com/fr/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Exemple de configuration en direct</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">Test de votre destination de diffusion en continu</a></li>
            </ul>
        </td>
        <td>
            <p><b>Configuration d’une destination basée sur des fichiers - Aide-mémoire</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Configuration d’un guide de bout en bout basé sur les fichiers</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">Configuration des formats de fichiers pour les fichiers exportés</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Exemple de configuration en direct pour une destination Amazon S3</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">Configuration de lot</a> pour la planification de l’exportation de fichiers et l’attribution de noms aux fichiers</li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">Test de votre destination basée sur des fichiers</a></li>
            </ul>
        </td>
        <td>
            <p><b>Autres informations essentielles</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">Obtention des informations d’authentification requises pour utiliser l’API</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">Conditions préalables à l’intégration</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Glossaire des termes de Destination SDK</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">Limites de taux et stratégie de reprise</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">Modèle en libre-service pour documenter votre destination</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## Intégrations standardisées et personnalisées {#productized-custom-integrations}

>[!IMPORTANT]
>
> Cette fonctionnalité de création de destinations personnalisées privées est disponible uniquement pour les clients [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html).

En tant que partenaire du Destination SDK, l’ajout de votre destination personnalisée au [Catalogue Experience Platform](../catalog/overview.md) vous permet de bénéficier des avantages suivants :

1. Standardisez les configurations d’intégration entre les clients avec des paramètres préconfigurés et simplifiez l’expérience de configuration pour les clients.
2. Représentez votre destination sous forme de carte personnalisée dans le catalogue des destinations dʼExperience Platform, pour une visibilité et une configuration en toute facilité.
3. Être présenté comme une intégration de destination productisée avec Adobe Experience Platform et Adobe Real-Time Customer Data Platform.

En tant que client Experience Platform, vous pouvez également créer votre propre destination personnalisée privée, qui peut mieux répondre à vos besoins d’activation.

![ Diagramme de présentation montrant comment les développeurs de destinations interagissent avec Destination SDK et comment les clients Real-Time CDP bénéficient de destinations privées et de production.](assets/destination-sdk-visual.png)

## Types d’intégration pris en charge {#supported-integration-types}

### Intégrations en temps réel (streaming) {#real-time-integrations}

Grâce à Destination SDK, Adobe Experience Platform prend en charge les intégrations en temps réel (également appelées flux) avec les destinations qui disposent d’un point d’entrée API REST. L’intégration en temps réel à Experience Platform prend en charge des fonctionnalités telles que :

* Transformation et agrégation des messages
* Renvoi des profils
* Intégration de métadonnées configurable pour initialiser la configuration de l’audience et le transfert de données
* Authentification configurable
* Suite d’API de test et de validation permettant de tester et d’itérer les configurations de destination

### Intégrations basées sur des fichiers {#file-based-integrations}

Grâce à Destination SDK, vous pouvez également configurer des intégrations pour exporter régulièrement des fichiers vers l’emplacement de stockage de votre choix. L’intégration basée sur les fichiers avec Experience Platform prend en charge des fonctionnalités telles que :

* Exportation de fichiers dans plusieurs formats pris en charge (CSV, Parquet, JSON)
* Options de formatage de fichier configurables, qui vous permettent de structurer le format des fichiers exportés pour répondre à vos besoins en aval.

Lisez les exigences techniques du côté des destinations dans l’article [ sur les conditions préalables à l’intégration ](integration-prerequisites.md) et découvrez toutes les configurations prises en charge dans l’article [options de configuration](functionality/configuration-options.md) .

## Accéder à Destination SDK {#get-access}

L’accès aux Destinations SDK varie en fonction de votre statut de partenaire ou d’Experience Platform, client Real-Time CDP. Pour plus d’informations, consultez le tableau ci-dessous.

| Type de partenaire ou de client | Accéder à Destination SDK |
---------|----------|
| Fournisseur de logiciels indépendant (ISV) | Rejoignez le [Programme de partenaire technologique Adobe](https://partners.adobe.com/technologyprogram/experiencecloud.html) et demandez à un environnement de test Experience Platform d’être configuré pour accéder à Destination SDK. |
| Intégrateur système (SI) | Vous devez être au niveau Gold ou Platine dans le [Programme partenaire en solution Adobe](https://solutionpartners.adobe.com/home.html) pour qu’un environnement de test Experience Platform soit configuré et que vous ayez accès à Destination SDK. |
| Client Experience Platform sur le [package Real-Time CDP Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) | Par défaut, vous avez accès aux environnements de test et à la Destination SDK Experience Platform, ce qui vous permet de créer des destinations privées pour votre organisation. |

{style="table-layout:auto"}

## Aperçu général de la configuration {#process}

Pour configurer votre destination dans Experience Platform, procédez comme suit :

1. Si vous êtes un logiciel de distribution d&#39;informations ou un logiciel de distribution d&#39;informations, reportez-vous à la section [Obtention de l&#39;accès](#get-access) de la section ci-dessus. Les clients [Real-Time CDP Ultimate package](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) peuvent ignorer cette étape.
2. [Faites la demande dʼun sandbox Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) et activez l’autorisation de création de destination.
3. Créez votre intégration. Suivez les instructions de la documentation du produit pour configurer les [destinations de diffusion en continu](guides/configure-destination-instructions.md) ou les [ destinations basées sur des fichiers](guides/configure-file-based-destination-instructions.md).
4. Testez votre intégration. Suivez les instructions de la documentation du produit pour tester les [destinations de diffusion en continu](testing-api/streaming-destinations/streaming-destination-testing-overview.md) ou les [ destinations basées sur des fichiers](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Si vous êtes un logiciel de développement logiciel ou si vous créez une [intégration productisée](./overview.md#productized-custom-integrations), [envoyez votre intégration](guides/submit-destination.md) pour la révision de l’Adobe (le temps de réponse standard est de cinq jours ouvrés).
6. Si vous êtes un logiciel de développement logiciel (ISV) ou si vous créez une intégration productisée, utilisez le [processus de documentation en libre-service](docs-framework/documentation-instructions.md) pour créer une page de documentation du produit sur l’Experience League pour votre destination.
7. Pour les intégrations productives, une fois approuvées par Adobe, votre intégration s’affichera dans le [catalogue Experience Platform](../catalog/overview.md).
8. Si vous souhaitez mettre à jour votre intégration, procédez de la même manière.

## Référence {#reference}

Adobe recommande de lire et de comprendre la documentation dʼExperience Platform suivante :

* [Présentation des destinations d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=fr)
* [Principes de base de la composition des schémas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr)
* [Présentation des espaces de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

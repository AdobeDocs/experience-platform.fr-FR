---
description: Adobe Experience Platform Destination SDK est un ensemble d’API de configuration qui vous permet de configurer des modèles d’intégration de destination pour qu’Experience Platform diffuse des données d’audience et de profil vers votre point de terminaison ou emplacement de stockage, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 42%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK est une suite d’API de configuration qui vous permet de configurer des modèles d’intégration de destination pour qu’Experience Platform diffuse des données d’audience et de profil vers votre point de terminaison ou emplacement de stockage, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.

La documentation du Destination SDK fournit des instructions pour utiliser Adobe Experience Platform Destination SDK afin de configurer, de tester et de publier une intégration de destination personnalisée avec Adobe Experience Platform. Votre destination pourra ensuite rejoindre le catalogue des destinations en constante évolution. En utilisant Destination SDK, vous pouvez également créer votre propre destination privée personnalisée pour exporter des données adaptées à vos besoins.

![Capture d’écran de l’interface utilisateur Experience Platform affichant le catalogue des destinations](assets/destinations-catalog-overview.png)

## Intégrations standardisées et personnalisées {#productized-custom-integrations}

>[!IMPORTANT]
>
> Cette fonctionnalité de création de destinations personnalisées privées est disponible uniquement pour [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) clients.

En tant que partenaire du Destination SDK, l’ajout de votre destination personnalisée au [Catalogue Experience Platform](../catalog/overview.md) vous permet de bénéficier des avantages suivants :

1. Standardisez les configurations d’intégration entre les clients avec des paramètres préconfigurés et simplifiez l’expérience de configuration pour les clients.
2. Représentez votre destination sous forme de carte personnalisée dans le catalogue des destinations dʼExperience Platform, pour une visibilité et une configuration en toute facilité.
3. Être présenté comme une intégration de destination productisée avec Adobe Experience Platform et Adobe Real-time Customer Data Platform.

En tant que client Experience Platform, vous pouvez également créer votre propre destination personnalisée privée, qui peut mieux répondre à vos besoins d’activation.

![Diagramme d’aperçu montrant comment les développeurs de destinations interagissent avec Destination SDK et comment les clients Real-Time CDP bénéficient de destinations privées et de production.](assets/destination-sdk-visual.png)

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

Découvrez les exigences techniques du côté des destinations dans la section [conditions préalables à l’intégration](integration-prerequisites.md) et découvrez toutes les configurations prises en charge dans la section [options de configuration](functionality/configuration-options.md) article

## Accéder à Destination SDK {#get-access}

L’accès aux Destinations SDK varie en fonction de votre statut de partenaire ou d’Experience Platform, client Real-Time CDP. Pour plus d’informations, consultez le tableau ci-dessous.

| Type de partenaire ou de client | Accéder à Destination SDK |
---------|----------|
| Fournisseur de logiciels indépendant (ISV) | Rejoindre le [Programme Partenaires en technologie Adobe](https://partners.adobe.com/technologyprogram/experiencecloud.html) et demandez à obtenir un environnement de test Experience Platform configuré pour accéder à Destination SDK. |
| Intégrateur système (SI) | Vous devez être au niveau Or ou Platine dans le [Programme Partenaires en solutions Adobe](https://solutionpartners.adobe.com/home.html) pour obtenir un sandbox Experience Platform configuré ainsi quʼun accès à Destination SDK. |
| Client Experience Platform sur la [Package Real-Time CDP Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) | Par défaut, vous avez accès aux environnements de test et à la Destination SDK Experience Platform, ce qui vous permet de créer des destinations privées pour votre organisation. |

{style="table-layout:auto"}

## Aperçu général de la configuration {#process}

Pour configurer votre destination dans Experience Platform, procédez comme suit :

1. Si vous êtes un fichier ISV ou SI, reportez-vous à la section [accès](#get-access) informations de la section ci-dessus. [Package Real-Time CDP Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) les clients peuvent ignorer cette étape.
2. [Faites la demande dʼun sandbox Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) et activez l’autorisation de création de destination.
3. Créez votre intégration. Suivez les instructions de la documentation du produit pour configurer [destinations de diffusion en continu](guides/configure-destination-instructions.md) ou [destinations basées sur des fichiers](guides/configure-file-based-destination-instructions.md).
4. Testez votre intégration. Suivez les instructions de la documentation du produit pour tester [destinations de diffusion en continu](testing-api/streaming-destinations/streaming-destination-testing-overview.md) ou [destinations basées sur des fichiers](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Si vous êtes un logiciel de développement logiciel ou si vous créez une [intégration productive](./overview.md#productized-custom-integrations), [soumettre votre intégration](guides/submit-destination.md) pour la révision par l’Adobe (le temps de réponse standard est de cinq jours ouvrables).
6. Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une intégration personnalisée, utilisez le [processus de documentation en libre-service](docs-framework/documentation-instructions.md) pour créer une page de documentation du produit sur Experience League pour votre destination.
7. Pour les intégrations productives, une fois approuvées par Adobe, votre intégration s’affichera dans la variable [Catalogue des Experience Platform](../catalog/overview.md).
8. Si vous souhaitez mettre à jour votre intégration, procédez de la même manière.

## Référence {#reference}

Adobe recommande de lire et de comprendre la documentation dʼExperience Platform suivante :

* [Présentation des destinations d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=fr)
* [Principes de base de la composition des schémas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr)
* [Présentation des espaces de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

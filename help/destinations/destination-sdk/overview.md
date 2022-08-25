---
description: Adobe Experience Platform Destination SDK est un ensemble dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données d’audience et de profil à votre point d’entrée, selon les formats de données et d’authentification choisis. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 2e2ed880650ad6823b60819e36081540a35ab727
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 83%

---

# Adobe Experience Platform Destination SDK

## Présentation {#destinations-sdk}

Le SDK Destination Adobe Experience Platform est un ensemble dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.

La documentation du Destination SDK fournit des instructions pour utiliser Adobe Experience Platform Destination SDK afin de configurer, de tester et de publier une intégration de destination personnalisée avec Adobe Experience Platform. Votre destination pourra ensuite rejoindre le catalogue des destinations en constante évolution.

![Présentation du catalogue des destinations](./assets/destinations-catalog-overview.png)

## Intégrations standardisées et personnalisées {#productized-custom-integrations}

En tant que partenaire du Destination SDK, l’ajout de votre destination personnalisée au [Catalogue Experience Platform](/help/destinations/catalog/overview.md) vous permet de bénéficier des avantages suivants :
1. Standardisez les configurations d’intégration entre les clients avec des paramètres préconfigurés et simplifiez l’expérience de configuration pour les clients.
2. Représentez votre destination sous forme de carte personnalisée dans le catalogue des destinations dʼExperience Platform, pour une visibilité et une configuration en toute facilité.
3. Recevez le statut dʼintégration de destination standardisée pour Adobe Experience Platform et Real-time Customer Data Platform.

En tant que client Experience Platform, vous pouvez créer votre propre destination personnalisée et privée, afin de mieux répondre à vos besoins d’activation.

![Diagramme visuel du Destination SDK](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Types d’intégrations pris en charge {#supported-integration-types}

Grâce au Destination SDK, Adobe Experience Platform prend en charge les intégrations en temps réel aux destinations qui ont un point dʼentrée API REST. L’intégration en temps réel à Experience Platform prend en charge des fonctionnalités telles que :
* Transformation et agrégation des messages
* Renvoi des profils
* Intégration de métadonnées configurable pour initialiser la configuration de l’audience et le transfert de données
* Authentification configurable
* Suite d’API de test et de validation permettant de tester et d’itérer les configurations de destination

Découvrez les exigences techniques du côté des destinations dans la section [Conditions préalables à l’intégration](./integration-prerequisites.md).

## Accéder à Destination SDK {#get-access}

L’accès aux Destinations SDK varie en fonction de votre statut de partenaire ou d’Experience Platform, client Real-Time CDP. Pour plus d’informations, consultez le tableau ci-dessous :


| Type de partenaire ou de client | Accéder à Destination SDK |
---------|----------|
| Fournisseur de logiciels indépendant (ISV) | Rejoignez le [Programme Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud.html) et sollicitez une sandbox Experience Platform configurée pour accéder à Destination SDK. |
| Intégrateur système (SI) | Vous devez être au niveau Or ou Platine dans le [Programme Partenaires en solutions Adobe](https://solutionpartners.adobe.com/home.html) pour obtenir une sandbox Experience Platform configurée ainsi quʼun accès à Destination SDK. |
| Client Experience Platform sur le [Package d’activation](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-experience-platform0.html) ou [Package Real-Time CDP Ultimate](https://helpx.adobe.com/fr/legal/product-descriptions/real-time-customer-data-platform.html) | Par défaut, vous avez accès aux environnements de test et à la Destination SDK Experience Platform, ce qui vous permet de créer des destinations privées pour votre organisation. |

{style=&quot;table-layout:auto&quot;}

## Aperçu général de la configuration {#process}

Pour configurer votre destination dans Experience Platform, procédez comme suit :

1. Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI), consultez la section ci-dessus relative à l’obtention des informations d’accès. Les clients [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) peuvent passer cette étape.
2. [Faites la demande dʼune sandbox Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) et activez l’autorisation de création de destination.
3. Créez votre intégration. Suivez les instructions de la documentation du produit pour configurer [destinations de diffusion en continu](./configure-destination-instructions.md) ou [Destinations basées sur des fichiers (version bêta)](./configure-file-based-destination-instructions.md).
4. Testez votre intégration. Suivez les instructions de la documentation du produit pour tester [destinations de diffusion en continu](./test-destination.md) ou [Destinations basées sur des fichiers (version bêta)](./file-based-destination-testing-overview.md).
5. Si vous êtes un logiciel de développement logiciel ou si vous créez une [intégration productive](./overview.md#productized-custom-integrations), [soumettre votre intégration](./submit-destination.md) pour la révision d’Adobe (le temps de réponse standard est de cinq jours ouvrables).
6. Si vous êtes un fournisseur de logiciels indépendant (ISV) ou un intégrateur de système (SI) créant une intégration personnalisée, utilisez le [processus de documentation en libre-service](./docs-framework/documentation-instructions.md) pour créer une page de documentation du produit sur Experience League pour votre destination.
7. Pour les intégrations productives, une fois approuvées par Adobe, votre intégration s’affichera dans la variable [Catalogue des Experience Platform](/help/destinations/catalog/overview.md).
8. Pour mettre à jour votre intégration, vous devez effectuer la même procédure.

## Référence {#reference}

Adobe recommande de lire et de comprendre la documentation dʼExperience Platform suivante :

* [Présentation des destinations d’Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=fr)
* [Principes de base de la composition des schémas XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr)
* [Présentation des espaces de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

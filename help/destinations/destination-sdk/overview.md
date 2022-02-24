---
description: L’Adobe Experience Platform Destination SDK est un ensemble d’API de configuration qui vous permet de configurer des modèles d’intégration de destination pour qu’Experience Platform diffuse des données d’audience et de profil à votre point de terminaison, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 85b308b3f92a734fed0c885a574b71fa05684bb4
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 14%

---

# Adobe Experience Platform Destination SDK

## Présentation {#destinations-sdk}

Le SDK Destination Adobe Experience Platform est un ensemble dʼAPI de configuration permettant de configurer des modèles dʼintégration de destination, afin quʼExperience Platform puisse envoyer des données dʼaudience et de profil à votre point dʼentrée, selon les formats de données et dʼauthentification choisis. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via lʼAPI pour des mises à jour supplémentaires.

La documentation sur les Destinations SDK vous explique comment utiliser l’Adobe Experience Platform Destination SDK pour configurer, tester et publier une intégration de destination productisée avec Adobe Experience Platform et faire en sorte que votre destination soit intégrée au catalogue des destinations en constante augmentation.

![Présentation du catalogue des destinations](./assets/destinations-catalog-overview.png)

## Intégrations personnalisées et productives {#productized-custom-integrations}

En tant que partenaire de Destination SDK, vous pouvez bénéficier de l’ajout de votre destination productisée au [Catalogue des Experience Platform](/help/destinations/catalog/overview.md):
1. Normalisez les configurations d’intégration entre les clients avec des paramètres préconfigurés et simplifiez l’expérience de configuration pour les clients.
2. Introduisez une carte de destination de marque dans le catalogue des destinations Experience Platform pour simplifier la configuration et la sensibilisation des clients.
3. Être présenté comme une intégration de destination productisée avec Adobe Experience Platform et Real-time Customer Data Platform.

En tant que client Experience Platform, vous pouvez créer une destination personnalisée privée qui répond le mieux à vos besoins d’activation.

![Diagramme visuel de Destination SDK](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Types d’intégration pris en charge {#supported-integration-types}

Grâce à Destination SDK, Adobe Experience Platform prend en charge les intégrations en temps réel avec les destinations qui ont un point de terminaison API REST. L’intégration en temps réel avec Experience Platform prend en charge des fonctionnalités telles que :
* Transformation et agrégation des messages
* Renvoi de profil
* Intégration de métadonnées configurable pour initialiser la configuration de l’audience et le transfert de données
* Authentification configurable
* Suite d’API de test et de validation permettant de tester et d’itérer les configurations de destination

Découvrez les exigences techniques du côté des destinations dans la section [conditions préalables à l’intégration](./integration-prerequisites.md) article.


## Accès à Destination SDK {#get-access}

L’accès aux Destinations SDK varie en fonction de votre statut de partenaire ou de client Experience Platform. Pour plus d’informations, veuillez consulter le tableau ci-dessous.


| Type de partenaire ou de client | Accès à Destination SDK |
---------|----------|
| Fournisseur de logiciels indépendant (ISV) | Rejoindre le [Programme Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud.html) et demandez à obtenir un environnement de test Experience Platform configuré pour accéder à Destination SDK. |
| Intégrateur système (SI) | Vous devez être au niveau Or ou Platine dans le [Programme Partenaires en solutions Adobe](https://solutionpartners.adobe.com/home.html)et vous obtiendrez un environnement de test Experience Platform configuré et un accès à Destination SDK. |
| Client Experience Platform sur la [Package d’activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | Par défaut, vous avez accès aux environnements de test et à la Destination SDK Experience Platform. |
| Client Experience Platform sur la [Package CDP en temps réel](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Vous n’avez pas accès à Destination SDK, mais vous avez accès à toutes les destinations productisées configurées par d’autres sociétés à l’aide de Destination SDK et publiées dans toutes les organisations Experience Platform. |

{style=&quot;table-layout:auto&quot;}

## Processus de haut niveau {#process}

Le processus de configuration de votre destination en Experience Platform est décrit ci-dessous :

1. Si vous êtes un logiciel de gestion de l&#39;information (ISV) ou un logiciel de gestion de l&#39;information (SI), reportez-vous à la section relative à l&#39;obtention des informations d&#39;accès dans la section ci-dessus. [Activation de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) les clients peuvent ignorer cette étape.
2. [Demande de configuration d’un environnement de test Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) et activez l’autorisation de création de destination.
3. [Créer votre intégration](./configure-destination-instructions.md) suivez la documentation du produit.
4. [Test de votre intégration](./test-destination.md) suivez la documentation du produit.
5. [Envoyer votre intégration](./submit-destination.md) pour la révision d’Adobe (le temps de réponse standard est de 5 jours ouvrables).
6. Si vous êtes un logiciel de développement logiciel ou si vous créez une [intégration productive](./overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](./docs-framework/documentation-instructions.md) pour créer une page de documentation du produit sur Experience League pour votre destination.
7. Une fois votre intégration approuvée par Adobe, elle s’affiche dans la variable [Catalogue des Experience Platform](/help/destinations/catalog/overview.md).
8. Si vous souhaitez mettre à jour votre intégration, procédez de la même manière.

## Référence {#reference}

Adobe vous recommande de lire et de comprendre la documentation Experience Platform suivante :

* [Présentation des destinations Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base de la composition du schéma XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr)
* [Présentation des espaces de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

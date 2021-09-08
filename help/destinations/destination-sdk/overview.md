---
description: Le SDK de destination Adobe Experience Platform est un ensemble d’API de configuration qui vous permettent de configurer des modèles d’intégration de destination pour que l’Experience Platform puisse fournir des données d’audience et de profil à votre point de terminaison, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via l’API pour des mises à jour supplémentaires.
title: SDK de destination Adobe Experience Platform
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 4%

---

# SDK de destination Adobe Experience Platform

## Présentation {#destinations-sdk}

Le SDK de destination Adobe Experience Platform est une suite d’API de configuration qui vous permet de configurer des modèles d’intégration de destination pour que l’Experience Platform puisse fournir des données d’audience et de profil à votre point de terminaison, en fonction des données et des formats d’authentification de votre choix. Les configurations sont stockées dans Experience Platform et peuvent être récupérées via l’API pour des mises à jour supplémentaires.

La documentation du SDK de destination fournit des instructions pour vous permettre d’utiliser le SDK de destination Adobe Experience Platform pour configurer, tester et publier une intégration de destination productisée avec Adobe Experience Platform et faire en sorte que votre destination soit intégrée au catalogue de destinations en constante augmentation.

![Présentation du catalogue des destinations](./assets/destinations-catalog-overview.png)

## Intégrations personnalisées et productives {#productized-custom-integrations}

En tant que partenaire du SDK de destination, vous pouvez bénéficier de l’ajout de votre destination productisée au [catalogue Experience Platform](/help/destinations/catalog/overview.md) :
1. Normalisez les configurations d’intégration entre les clients avec des paramètres préconfigurés et simplifiez l’expérience de configuration pour les clients.
2. Introduisez une carte de destination de marque dans le catalogue des destinations Experience Platform pour simplifier la configuration et la sensibilisation des clients.
3. Être présenté comme une intégration de destination productisée avec Adobe Experience Platform et la plateforme de données clients en temps réel.

En tant que client Experience Platform, vous pouvez créer une destination personnalisée privée qui répond le mieux à vos besoins d’activation.

![Diagramme visuel du SDK de destination](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## Types d’intégration pris en charge {#supported-integration-types}

Grâce au SDK de destination, Adobe Experience Platform prend en charge les intégrations en temps réel avec les destinations qui possèdent un point de terminaison API REST. L’intégration en temps réel avec Experience Platform prend en charge des fonctionnalités telles que :
* Transformation et agrégation des messages
* Renvoi de profil
* Intégration de métadonnées configurable pour initialiser la configuration de l’audience et le transfert de données
* Authentification configurable
* Suite d’API de test et de validation permettant de tester et d’itérer les configurations de destination

Découvrez les exigences techniques du côté des destinations dans l’article [Conditions préalables à l’intégration](./integration-prerequisites.md) .


## Accès au SDK de destination {#get-access}

L’accès au SDK de destination varie en fonction de votre statut de partenaire ou de client Experience Platform. Pour plus d’informations, veuillez consulter le tableau ci-dessous.


| Type de partenaire ou de client | Accès au SDK de destination |
---------|----------|
| Fournisseur de logiciels indépendant (ISV) | Rejoignez le [programme Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud.html) et demandez à un environnement de test Experience Platform d’accéder au SDK Destination. |
| Intégrateur système (SI) | Vous devez être au niveau Gold ou Platinum dans le [programme Partenaires en solution Adobe](https://solutionpartners.adobe.com/home.html). Un environnement de test Experience Platform est configuré et vous avez accès au SDK de destination. |
| Client Experience Platform sur le package d’activation | Par défaut, vous avez accès aux environnements de test Experience Platform et au SDK de destination. |
| Client Experience Platform sur le package CDP en temps réel | Vous n’avez pas accès au SDK de destination, mais vous avez accès à toutes les destinations productisées configurées par d’autres sociétés à l’aide du SDK de destination et publiées dans les organisations Experience Platform. |

{style=&quot;table-layout:auto&quot;}

## Processus de haut niveau {#process}

Le processus de configuration de votre destination en Experience Platform est décrit ci-dessous :

1. Si vous êtes un logiciel de gestion de l&#39;information (ISV) ou un logiciel de gestion de l&#39;information (SI), reportez-vous à la section relative à l&#39;obtention des informations d&#39;accès dans la section ci-dessus. [Les clients Adobe Experience Platform ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) Activation peuvent ignorer cette étape.
2. [Demande de configuration d’un ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) sandbox Experience Platform et d’activation de l’autorisation de création de destination.
3. [Créez votre ](./configure-destination-instructions.md) intégration en suivant la documentation du produit.
4. [Testez votre ](./test-destination.md) intégration en suivant la documentation du produit.
5. [Envoyez votre ](./destination-publish-api.md) intégration pour révision par Adobe (le temps de réponse standard est de 5 jours ouvrables).
6. Si vous êtes un logiciel de développement logiciel (ISV) ou si vous créez une [intégration productisée](./overview.md#productized-custom-integrations), utilisez le [processus de documentation en libre-service](./docs-framework/documentation-instructions.md) pour créer une page de documentation du produit sur l’Experience League pour votre destination.
7. Une fois approuvée par Adobe, votre intégration s’affichera dans le [catalogue Experience Platform](/help/destinations/catalog/overview.md).
8. Si vous souhaitez mettre à jour votre intégration, procédez de la même manière.

## Référence {#reference}

Adobe vous recommande de lire et de comprendre la documentation Experience Platform suivante :

* [Présentation des destinations Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [Base de la composition du schéma XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr)
* [Présentation des espaces de noms d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=fr)

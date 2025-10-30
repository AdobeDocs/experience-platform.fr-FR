---
title: Connecteur Source Adobe Commerce
description: Découvrez comment utiliser la source Adobe Commerce pour importer vos données commerciales dans Experience Platform.
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

Adobe Commerce est une plateforme commerciale B2B et B2C agile qui permet aux commerçants et aux marques d’accélérer leurs recettes grâce à des expériences commerciales numériques axées sur les clients sur des espaces en ligne et physiques.

Les sources Adobe Experience Platform prennent en charge l’intégration d’Adobe Commerce pour permettre aux commerçants d’envoyer des données de storefront et de back-office à Experience Platform Edge Network, de sorte que d’autres produits Adobe Experience Cloud tels qu’Adobe Analytics et Adobe Target puissent utiliser les données [!DNL Commerce].

* **Événements Storefront** : capturez les interactions de l’acheteur telles que les `View Page`, les `View Product` et les `Add to Cart`. Pour les commerçants B2B, les événements storefront capturent également les [listes de demandes](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html).
* **Événements Back Office** : capturez des informations sur le statut d’une commande, par exemple si une commande a été passée, annulée, remboursée, expédiée ou terminée.

>[!NOTE]
>
>Les données capturées dans Adobe Commerce n’incluent pas d’informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont strictement anonymisés.

## Conditions préalables

Pour connecter Adobe Commerce à Experience Platform, vous devez disposer des éléments suivants :

* Adobe Commerce 2.4.3 ou version ultérieure.
* Un Adobe ID et un ID d’organisation valides.
* Accès à l’extension [Adobe Client Data Layer](../../../tags/extensions/client/client-data-layer/overview.md). Cette extension est nécessaire pour collecter les données d’événement de storefront.
* Droits sur d’autres produits Adobe DX.

## Étapes d’intégration

Pour intégrer complètement votre compte source Adobe Commerce, suivez les étapes décrites ci-dessous ainsi que la documentation correspondante.

* [Installez l [!DNL Data Connection] extension](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) pour Adobe Commerce. Vous pouvez télécharger l’extension de connecteur depuis [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Une fois l’extension de connecteur installée avec succès, connectez-vous à votre compte Adobe dans Experience Cloud et [confirmez votre identifiant d’organisation](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Cet identifiant est associé à la société Experience Cloud configurée. Elle est formatée sous la forme d’une chaîne alphanumérique de 24 caractères et comprend un `@AdobeOrg` obligatoire.
* Créez ou mettez ensuite à jour votre schéma de modèle de données d’expérience (XDM) avec vos groupes de champs spécifiques à Commerce. Pour obtenir des instructions détaillées sur la manière d’ajouter des groupes de champs spécifiques à Commerce à votre schéma XDM, consultez le guide sur [l’ajout de groupes de champs à un schéma XDM](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
* Une fois votre schéma configuré, vous devez créer un jeu de données basé sur votre nouveau schéma. Ce jeu de données contiendra alors les données [!DNL Commerce] que vous envoyez. Pour obtenir des instructions détaillées sur la création d’un jeu de données pour les données [!DNL Commerce], consultez le guide sur l’[envoi de données à Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Créez ensuite un flux de données et sélectionnez le schéma XDM contenant vos groupes de champs spécifiques à Commerce. Pour plus d’informations sur les flux de données, consultez la [présentation des flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr).
* Ensuite, vous devez connecter votre instance Adobe Commerce au [connecteur de services Commerce](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Cela permet de déployer votre instance Commerce en tant que SaaS (Software as a Service).
* Une fois toutes les configurations mentionnées ci-dessus terminées, vous pouvez vous connecter à Experience Platform en configurant le connecteur de services Commerce et l’extension [!DNL Data Connection] à l’aide de l’[!DNL Commerce Admin] . Pour plus d’informations sur cette dernière étape, consultez le guide sur [la connexion des données Commerce à Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).

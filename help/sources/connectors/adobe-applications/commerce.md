---
title: Connecteur source Adobe Commerce
description: Découvrez comment utiliser la source Adobe Commerce pour importer vos données commerciales dans Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: 8249de4c78810a4cee245fa9c48b91c210aeb0a4
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 5%

---

# Adobe Commerce

Adobe Commerce est une plate-forme de commerce B2B et B2C agile qui permet aux commerçants et aux marques d’accélérer leurs recettes grâce à des expériences commerciales numériques axées sur le client sur des espaces en ligne et physiques.

Les sources Adobe Experience Platform prennent en charge l’intégration d’Adobe Commerce pour permettre aux commerçants d’envoyer des données de storefront et back-office au réseau Edge Experience Platform, de sorte que d’autres produits Adobe Experience Cloud tels qu’Adobe Analytics et Adobe Target puissent utiliser [!DNL Commerce] data.

* **Événements Storefront**: capturez les interactions d’acheteurs telles que `View Page`, `View Product`, et `Add to Cart`. Pour les commerçants B2B, les événements storefront sont également capturés [listes de demandes](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Événements de back-office**: capture des informations sur l’état d’une commande, par exemple si une commande a été passée, annulée, remboursée, expédiée ou terminée.

>[!NOTE]
>
>Les données capturées dans Adobe Commerce ne contiennent pas d’informations d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les identifiants de cookie et les adresses IP, sont strictement anonymisés.

## Conditions préalables

Pour connecter Adobe Commerce à Experience Platform, vous devez disposer des éléments suivants :

* Adobe Commerce 2.4.3 ou version ultérieure.
* Un Adobe ID et un ID d’organisation valides.
* L’accès au [Extension Adobe Client Data Layer](../../../tags/extensions/client/client-data-layer/overview.md). Cette extension est nécessaire pour collecter les données d’événement storefront.
* Droits pour d’autres produits DX d’Adobe.

## Étapes d’intégration

Pour intégrer entièrement votre compte source Adobe Commerce, suivez les étapes décrites ci-dessous avec la documentation correspondante.

* [Installation de l’extension Experience Platform Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html) pour Adobe Commerce. Vous pouvez télécharger l’extension de connecteur à partir de [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Une fois que vous avez installé l’extension de connecteur, connectez-vous à votre compte Adobe dans Experience Cloud et [confirmer votre ID d’organisation ;](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html?lang=fr#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Cet identifiant est associé à votre société d’Experience Cloud configurée. Il est formaté sous la forme d’une chaîne alphanumérique de 24 caractères et comprend un paramètre obligatoire `@AdobeOrg`.
* Ensuite, créez ou mettez à jour votre schéma de modèle de données d’expérience (XDM) avec vos groupes de champs spécifiques au commerce. Pour obtenir des instructions détaillées sur la manière d’ajouter des groupes de champs spécifiques à Commerce à votre schéma XDM, consultez le guide sur [ajout de groupes de champs à un schéma XDM](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html?lang=fr).
* Une fois votre schéma configuré, vous devez créer un jeu de données basé sur votre nouveau schéma. Ce jeu de données contiendra alors la variable [!DNL Commerce] données que vous envoyez. Pour obtenir des instructions détaillées sur la création d’un jeu de données pour [!DNL Commerce] data, lisez le guide sur [envoi de données à l’Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Créez ensuite un flux de données et sélectionnez le schéma XDM contenant vos groupes de champs spécifiques à Commerce. Pour plus d’informations sur les flux de données, consultez la section [présentation des jeux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr).
* Ensuite, vous devez connecter votre instance Adobe Commerce à l’événement [Connecteur Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Cela permet à votre instance Commerce d’être déployée en tant que SaaS (Software as a Service).
* Toutes les configurations ci-dessus étant terminées, vous pouvez désormais vous connecter à Experience Platform en configurant le connecteur Commerce Services et le connecteur Experience Platform à l’aide de l’événement [!DNL Commerce Admin]. Pour plus d’informations sur cette dernière étape, consultez le guide sur [connexion des données commerciales à l’Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html).

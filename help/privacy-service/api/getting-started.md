---
title: S’authentifier et accéder à l’API Privacy Service
description: Découvrez comment vous authentifier auprès de l’API du Privacy Service et comment interpréter des exemples d’appels API dans la documentation.
role: Developer
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 18%

---

# S’authentifier et accéder à l’API Privacy Service

Ce guide présente les concepts de base que vous devez connaître avant d’effectuer des appels vers l’API Adobe Experience Platform Privacy Service.

## Conditions préalables {#prerequisites}

Ce guide nécessite une compréhension pratique de [Privacy Service](../home.md) et de la manière dont il vous permet de gérer les requêtes d’accès et de suppression de vos sujets des données (clients) dans les applications Adobe Experience Cloud.

Afin de créer des informations d’identification d’accès pour l’API, un administrateur de votre entreprise doit avoir préalablement configuré les profils de produit pour Privacy Service dans Adobe Admin Console. Le profil de produit que vous affectez à une intégration d’API détermine les autorisations dont dispose l’intégration lors de l’accès aux fonctionnalités de Privacy Service. Pour plus d’informations, consultez le guide sur la [gestion des autorisations de Privacy Service](../permissions.md) .

## Collecter des valeurs pour les en-têtes requis {#gather-values-required-headers}

Pour passer des appels à l’API du Privacy Service, vous devez d’abord rassembler vos informations d’identification d’accès à utiliser dans les en-têtes requis :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Ces valeurs sont générées à l’aide de [Adobe Developer Console](https://developer.adobe.com/console). Vos `{ORG_ID}` et `{API_KEY}` n’ont besoin d’être générés qu’une seule fois et peuvent être réutilisés dans les prochains appels API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes de génération de ces valeurs sont décrites en détail ci-dessous.

### Configuration ponctuelle {#one-time-setup}

Accédez à [Adobe Developer Console](https://developer.adobe.com/console) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création d’un projet vide](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) dans la documentation de Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajouter au projet]** et **[!UICONTROL API]** dans le menu déroulant.

![L’option API sélectionnée dans la liste déroulante [!UICONTROL Ajouter au projet] de la page des détails du projet dans Developer Console](../images/api/getting-started/add-api-button.png)

#### Sélection de l’API du Privacy Service {#select-privacy-service-api}

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionnez **[!UICONTROL Experience Cloud]** pour réduire la liste des API disponibles, puis sélectionnez la carte de l’ **[!UICONTROL API Privacy Service]** avant de sélectionner **[!UICONTROL Suivant]**.

![La carte API du Privacy Service sélectionnée dans la liste des API disponibles](../images/api/getting-started/add-privacy-service-api.png)

>[!TIP]
>
>Sélectionnez l’option **[!UICONTROL Afficher la documentation]** pour naviguer dans une fenêtre de navigateur distincte vers la [ documentation de référence sur l’API du Privacy Service ](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

Sélectionnez ensuite le type d&#39;authentification pour générer les jetons d&#39;accès et accéder à l&#39;API du Privacy Service.

>[!IMPORTANT]
>
>Sélectionnez la méthode **[!UICONTROL OAuth Server-to-Server]**, car il s’agira de la seule méthode prise en charge à l’avenir. La méthode **[!UICONTROL Service Account (JWT)]** est obsolète. Bien que les intégrations utilisant la méthode d’authentification JWT continueront à fonctionner jusqu’au 1er janvier 2025, Adobe recommande vivement de migrer les intégrations existantes vers la nouvelle méthode OAuth Server-to-Server avant cette date. Pour plus d’informations, reportez-vous à la section [!BADGE Obsolète]{type=negative}[Générer un jeton Web JSON (JWT)](/help/landing/api-authentication.md#jwt).

![Sélectionnez la méthode d&#39;authentification Oauth Server-to-Server.](/help/privacy-service/images/api/getting-started/select-oauth-authentication.png)

#### Attribution d’autorisations via les profils de produit {#product-profiles}

La dernière étape de configuration consiste à sélectionner les profils de produit à partir desquels cette intégration héritera de ses autorisations. Si vous sélectionnez plusieurs profils, leurs jeux d’autorisations seront combinés pour l’intégration.

>[!NOTE]
>
Les profils de produit et les autorisations granulaires qu’ils fournissent sont créés et gérés par les administrateurs via Adobe Admin Console. Pour plus d’informations, consultez le guide sur les [autorisations de Privacy Service](../permissions.md) .

Lorsque vous avez terminé, sélectionnez **[!UICONTROL Enregistrer l’API configurée]**.

![Un profil de produit unique sélectionné dans la liste avant d’enregistrer la configuration](../images/api/getting-started/select-product-profiles.png)

Une fois que l’API a été ajoutée au projet, la page **[!UICONTROL API Privacy Service]** du projet affiche les informations d’identification suivantes requises dans tous les appels aux API Privacy Service :

* `{API_KEY}` ([!UICONTROL ID client])
* `{ORG_ID}` ([!UICONTROL ID d’organisation])

![ Informations d’intégration après l’ajout d’une API dans Developer Console.](/help/privacy-service/images/api/getting-started/api-integration-information.png)

### Authentification pour chaque session {#authentication-each-session}

Les dernières informations d’identification requises que vous devez rassembler sont votre `{ACCESS_TOKEN}`, qui est utilisé dans l’en-tête d’autorisation. Contrairement aux valeurs de `{API_KEY}` et `{ORG_ID}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser l’API.

En règle générale, il existe deux méthodes pour générer un jeton d’accès :

* [Générez le jeton manuellement](#manual-token) pour le test et le développement.
* [Automatiser la génération de jetons](#auto-token) pour les intégrations API.

#### Génération manuelle d’un jeton {#manual-token}

Pour générer manuellement un nouveau `{ACCESS_TOKEN}`, accédez à **[!UICONTROL Credentials]** > **[!UICONTROL OAuth Server-to-Server]** et sélectionnez **[!UICONTROL Generate access token]**, comme illustré ci-dessous.

![Enregistrement d’écran de la génération d’un jeton d’accès dans l’interface utilisateur de Developer Console.](/help/privacy-service/images/api/getting-started/generate-access-token.gif)

Un nouveau jeton d’accès est généré et un bouton permettant de copier le jeton dans le presse-papiers est fourni. Cette valeur est utilisée pour l’en-tête [!DNL Authorization] requis et doit être fournie au format `Bearer {ACCESS_TOKEN}`.

#### Automatiser la génération des jetons {#auto-token}

Vous pouvez également utiliser un environnement et une collection Postman pour générer des jetons d’accès. Pour plus d’informations, lisez la section [ sur l’utilisation de Postman pour authentifier et tester les appels API](/help/landing/api-authentication.md#use-postman) dans le guide d’authentification de l’API Experience Platform.

## Lecture d’exemples d’appels API {#read-sample-api-calls}

Chaque guide de point de terminaison fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/api-guide.md#sample-api) dans le guide de prise en main des API Platform.

## Étapes suivantes {#next-steps}

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Privacy Service. Sélectionnez l’un des guides de point d’entrée pour commencer :

* [Tâches de confidentialité](./privacy-jobs.md)
* [Consentement](./consent.md)

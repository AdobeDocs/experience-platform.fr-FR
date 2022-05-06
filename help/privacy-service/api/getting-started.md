---
title: Prise en main de l’API du Privacy Service
description: Découvrez comment vous authentifier auprès de l’API du Privacy Service et comment interpréter des exemples d’appels API dans la documentation.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 26%

---

# Prise en main de l’API du Privacy Service

Ce guide présente les concepts de base que vous devez connaître avant d’effectuer des appels vers l’API du Privacy Service.

## Conditions préalables

Ce guide nécessite une compréhension pratique des fonctionnalités suivantes :

* [Adobe Experience Platform Privacy Service](../home.md): Fournit une API RESTful et une interface utilisateur qui vous permettent de gérer les requêtes d’accès et de suppression de vos sujets des données (clients) dans les applications Adobe Experience Cloud.

## Collecte des valeurs des en-têtes requis

Pour passer des appels à l’API du Privacy Service, vous devez d’abord rassembler vos informations d’identification d’accès à utiliser dans les en-têtes requis :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Cela implique d’obtenir les autorisations des développeurs pour Adobe Experience Platform dans Adobe Admin Console, puis de générer les informations d’identification dans la console Adobe Developer.

### Obtenir l’accès développeur à  Experience Platform

Pour permettre aux développeurs d’accéder à [!DNL Platform], suivez les étapes initiales de la section [Tutoriel sur l’authentification des Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Une fois que vous êtes arrivé à l’étape &quot;Générer les informations d’identification d’accès dans la console Adobe Developer&quot;, revenez à ce tutoriel pour générer les informations d’identification spécifiques à Privacy Service.

### Génération des informations d’identification d’accès

À l’aide d’Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Votre `{ORG_ID}` et `{API_KEY}` ne doit être généré qu’une seule fois et peut être réutilisé dans les prochains appels API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes de génération de ces valeurs sont décrites en détail ci-dessous.

#### Configuration ponctuelle

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création dʼun projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) disponible dans la documentation dʼAdobe Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajout d’une API]** sur le **[!UICONTROL Présentation du projet]** écran.

![](../images/api/getting-started/add-api-button.png)

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionner **[!UICONTROL API Privacy Service]** dans la liste des API disponibles avant de sélectionner **[!UICONTROL Suivant]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Le **[!UICONTROL Configuration de l’API]** s’affiche. Sélectionnez l’option pour **[!UICONTROL Générer une paire de clés]**, puis sélectionnez **[!UICONTROL Générer une paire de clés]** dans le coin inférieur droit.

![](../images/api/getting-started/generate-key-pair.png)

La paire de clés est automatiquement générée et un fichier ZIP contenant une clé privée et un certificat public est téléchargé sur votre ordinateur local (pour être utilisé ultérieurement). Sélectionner **[!UICONTROL Enregistrer l’API configurée]** pour terminer la configuration.

![](../images/api/getting-started/key-pair-generated.png)

Une fois l’API ajoutée au projet, la page du projet réapparaît sur la page **API Privacy Service - Aperçu** page. À partir de là, faites défiler l’écran jusqu’au **[!UICONTROL Compte de service (JWT)]** , qui fournit les informations d’identification d’accès suivantes requises dans tous les appels à l’API du Privacy Service :

* **[!UICONTROL ID CLIENT]**: L’identifiant du client est obligatoire. `{API_KEY}` pour cela doit être fourni dans l’en-tête x-api-key .
* **[!UICONTROL ID D’ORGANISATION]**: L’ID d’organisation est la valeur `{ORG_ID}` qui doit être utilisée dans l’en-tête x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez recueillir sont vos `{ACCESS_TOKEN}`, qui est utilisé dans l’en-tête d’autorisation. Contrairement aux valeurs de `{API_KEY}` et `{ORG_ID}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser [!DNL Platform] API.

Pour générer un nouveau `{ACCESS_TOKEN}`, ouvrez la clé privée précédemment téléchargée et collez son contenu dans la zone de texte située à côté. **[!UICONTROL Générer un jeton d’accès]** avant de sélectionner **[!UICONTROL Générer un jeton]**.

![](../images/api/getting-started/paste-private-key.png)

Un nouveau jeton d’accès est généré et un bouton permettant de copier le jeton dans le presse-papiers est fourni. Cette valeur est utilisée pour l’en-tête d’autorisation requis et doit être fournie au format . `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur [lecture d’exemples d’appels API](../../landing/api-guide.md#sample-api) dans le guide de prise en main des API Platform.

## Étapes suivantes

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Privacy Service. Sélectionnez l’un des guides de point d’entrée pour commencer :

* [Tâches de confidentialité](./privacy-jobs.md)
* [Consentement](./consent.md)

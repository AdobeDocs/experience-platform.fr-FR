---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de Privacy Service
description: Utilisez l’API RESTful pour gérer les données personnelles des propriétaires de données dans les applications Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 27%

---


# [!DNL Privacy Service] guide du développeur

Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface that allow you to manage (access and delete) the personal data of your data subjects (customers) across Adobe Experience Cloud applications. [!DNL Privacy Service] fournit aussi un mécanisme central d’audit et de connexion qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications [!DNL Experience Cloud]

This guide covers how to use the [!DNL Privacy Service] API. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la [présentation de l’interface utilisateur de Privacy Service](../ui/overview.md). For a comprehensive list of all available endpoints in the [!DNL Privacy Service] API, please see the [API reference](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html).

## Prise en main {#getting-started}

This guide requires a working understanding the following [!DNL Experience Platform] features:

* [!DNL Privacy Service](../home.md) : fournit une API RESTful et une interface utilisateur permettant de gérer l’accès et de supprimer les requêtes des propriétaires des données (les clients) dans les applications Adobe Experience Cloud.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à l’API Privacy Service.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. For information on the conventions used in documentation for sample API calls, see the section on [how to read example API calls](../../landing/troubleshooting.md) in the [!DNL Experience Platform] troubleshooting guide.

## Collecte des valeurs des en-têtes requis

Pour appeler l’ [!DNL Privacy Service] API, vous devez d’abord rassembler vos informations d’identification d’accès pour les utiliser dans les en-têtes requis :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Cela implique d’obtenir les autorisations de développeur pour [!DNL Experience Platform] dans Adobe Admin Console, puis de générer les informations d’identification dans Adobe Developer Console.

### Accédez à [!DNL Experience Platform]

Pour permettre aux développeurs d’accéder à [!DNL Platform], suivez les premières étapes du didacticiel [d’authentification des](../../tutorials/authentication.md)Experience Platform. Une fois que vous êtes arrivé à l&#39;étape &quot;Générer les informations d&#39;identification d&#39;accès dans la Console développeur d&#39;Adobe&quot;, revenez à ce didacticiel pour générer les informations d&#39;identification spécifiques à [!DNL Privacy Service].

### Générer des informations d’identification d’accès

A l’aide d’Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Vous `{IMS_ORG}` `{API_KEY}` devez générer votre fichier une seule fois et vous pouvez le réutiliser dans les prochains appels d’API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes de génération de ces valeurs sont décrites en détail ci-dessous.

#### Configuration ponctuelle

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) and sign in with your Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation de la Console développeur d&#39;Adobes.

Une fois que vous avez créé un nouveau projet, cliquez sur **[!UICONTROL Ajouter l’API]** dans l’écran Présentation _[!UICONTROL du]_projet.

![](../images/api/getting-started/add-api-button.png)

L’écran _[!UICONTROL Ajouter une API]_s’affiche. Sélectionnez API****Privacy Service dans la liste des API disponibles avant de cliquer sur**[!UICONTROL  Suivant ]**.

![](../images/api/getting-started/add-privacy-service-api.png)

The _[!UICONTROL Configure API]_screen appears. Sélectionnez l’option**[!UICONTROL  Générer une paire ]**de clés, puis cliquez sur**[!UICONTROL  Générer une paire de clés ]**dans le coin inférieur droit.

![](../images/api/getting-started/generate-key-pair.png)

La paire de clés est générée automatiquement et un fichier ZIP contenant une clé privée et un certificat public est téléchargé sur votre ordinateur local (à utiliser ultérieurement). Sélectionnez **[!UICONTROL Enregistrer l’API]** configurée pour terminer la configuration.

![](../images/api/getting-started/key-pair-generated.png)

Une fois l&#39;API ajoutée au projet, la page du projet réapparaît sur la page d&#39;aperçu _de l&#39;API du_ Privacy Service. À partir de là, faites défiler l’écran jusqu’à la section Compte de _[!UICONTROL service (JWT)]_, qui fournit les informations d’identification d’accès suivantes requises dans tous les appels à l’[!DNL Privacy Service]API :

* **[!UICONTROL ID]** CLIENT : L’ID client est requis `{API_KEY}` pour cela et doit être fourni dans l’en-tête x-api-key.
* **[!UICONTROL ID]** D&#39;ORGANISATION : L’ID d’organisation est la `{IMS_ORG}` valeur qui doit être utilisée dans l’en-tête x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez rassembler sont les vôtres `{ACCESS_TOKEN}`, qui sont utilisées dans l’en-tête Autorisation. Contrairement aux valeurs pour `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser [!DNL Platform] les API.

Pour générer un nouveau fichier `{ACCESS_TOKEN}`, ouvrez la clé privée précédemment téléchargée et collez son contenu dans la zone de texte en regard de _[!UICONTROL Générer un jeton d&#39;accès]_avant de cliquer sur**[!UICONTROL  Générer un jeton ]**.

![](../images/api/getting-started/paste-private-key.png)

Un nouveau jeton d&#39;accès est généré et un bouton permettant de copier le jeton dans le Presse-papiers est fourni. Cette valeur est utilisée pour l’en-tête Autorisation requis et doit être fournie au format `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Étapes suivantes

Now that you understand what headers to use, you are ready to begin making calls to the [!DNL Privacy Service] API. Le document sur les [tâches liées à la confidentialité](privacy-jobs.md) décrit les différents appels API que vous pouvez lancer à l’aide de l’API [!DNL Privacy Service] Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guide de développement de Privacy Service
description: Utilisez l’API RESTful pour gérer les données personnelles des propriétaires de données dans les applications Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: b45fdfff70ce4ba857f23e7116812a07825871bc
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 42%

---


# Guide de développement de Privacy Service

Privacy Service d’Adobe Experience Platform fournit une API RESTful et une interface utilisateur permettant de gérer les données personnelles (d’y accéder et de les supprimer) des propriétaires de données (clients) dans les applications Adobe Experience Cloud. Privacy Service fournit aussi un mécanisme central d’audit et de connexion qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications Experience Cloud.

Ce guide explique comment utiliser l’API Privacy Service. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la [présentation de l’interface utilisateur de Privacy Service](../ui/overview.md). Pour obtenir la liste complète de tous les points de terminaison disponibles dans l’API Privacy Service, consultez [Référence d’API](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html).

## Prise en main {#getting-started}

Ce guide nécessite une bonne compréhension des fonctionnalités d’Experience Platform suivantes :

* [Privacy Service](../home.md) : fournit une API RESTful et une interface utilisateur permettant de gérer l’accès et de supprimer les requêtes des propriétaires des données (les clients) dans les applications Adobe Experience Cloud.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à l’API Privacy Service.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels API, consultez la section sur la [lecture d’exemples d’appels API](../../landing/troubleshooting.md) dans le guide de dépannage d’Experience Platform.

## Collecte des valeurs des en-têtes requis

Pour appeler l’API du Privacy Service, vous devez d’abord rassembler vos informations d’identification d’accès pour les utiliser dans les en-têtes requis :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Cela implique d&#39;obtenir des autorisations de développeur pour un Experience Platform dans Adobe Admin Console, puis de générer les informations d&#39;identification dans Adobe Developer Console.

### Obtenir l&#39;accès des développeurs aux Experience Platform

Pour permettre aux développeurs d’accéder à Platform, suivez les premières étapes du didacticiel [sur l’authentification des](../../tutorials/authentication.md)Experience Platform. Une fois que vous êtes arrivé à l’étape &quot;Générer les informations d’identification d’accès dans Adobe Developer Console&quot;, revenez à ce didacticiel pour générer les informations d’identification spécifiques au Privacy Service.

### Générer des informations d’identification d’accès

A l’aide de Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Vous `{IMS_ORG}` `{API_KEY}` devez générer votre fichier une seule fois et vous pouvez le réutiliser dans les prochains appels d’API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes de génération de ces valeurs sont décrites en détail ci-dessous.

#### Configuration ponctuelle

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) and sign in with your Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d’un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation de Adobe Developer Console.

Une fois que vous avez créé un nouveau projet, cliquez sur **[!UICONTROL Ajouter l’API]** dans l’écran Présentation _[!UICONTROL du]_projet.

![](../images/api/getting-started/add-api-button.png)

L’écran _[!UICONTROL Ajouter une API]_s’affiche. Sélectionnez API****Privacy Service dans la liste des API disponibles avant de cliquer sur**[!UICONTROL  Suivant ]**.

![](../images/api/getting-started/add-privacy-service-api.png)

The _[!UICONTROL Configure API]_screen appears. Sélectionnez l’option**[!UICONTROL  Générer une paire ]**de clés, puis cliquez sur**[!UICONTROL  Générer une paire de clés ]**dans le coin inférieur droit.

![](../images/api/getting-started/generate-key-pair.png)

La paire de clés est générée automatiquement et un fichier ZIP contenant une clé privée et un certificat public est téléchargé sur votre ordinateur local (à utiliser ultérieurement). Sélectionnez **[!UICONTROL Enregistrer l’API]** configurée pour terminer la configuration.

![](../images/api/getting-started/key-pair-generated.png)

Une fois l&#39;API ajoutée au projet, la page du projet réapparaît sur la page d&#39;aperçu _de l&#39;API du_ Privacy Service. A partir de là, faites défiler l’écran jusqu’à la section Compte _[!UICONTROL de service (JWT)]_, qui fournit les informations d’identification d’accès suivantes requises dans tous les appels à l’API du Privacy Service :

* **[!UICONTROL ID]** CLIENT : L’ID client est requis `{API_KEY}` pour cela et doit être fourni dans l’en-tête x-api-key.
* **[!UICONTROL ID]** D&#39;ORGANISATION : L’ID d’organisation est la `{IMS_ORG}` valeur qui doit être utilisée dans l’en-tête x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez rassembler sont les vôtres `{ACCESS_TOKEN}`, qui sont utilisées dans l’en-tête Autorisation. Contrairement aux valeurs pour `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API Platform.

Pour générer un nouveau fichier `{ACCESS_TOKEN}`, ouvrez la clé privée précédemment téléchargée et collez son contenu dans la zone de texte en regard de _[!UICONTROL Générer un jeton d&#39;accès]_avant de cliquer sur**[!UICONTROL  Générer un jeton ]**.

![](../images/api/getting-started/paste-private-key.png)

Un nouveau jeton d&#39;accès est généré et un bouton permettant de copier le jeton dans le Presse-papiers est fourni. Cette valeur est utilisée pour l’en-tête Autorisation requis et doit être fournie au format `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Étapes suivantes

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API Privacy Service. Le document sur les [tâches liées à la confidentialité](privacy-jobs.md) décrit les différents appels API que vous pouvez lancer à l’aide de l’API Privacy Service. Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

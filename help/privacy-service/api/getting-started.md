---
keywords: Experience Platform ; accueil ; rubriques populaires
solution: Experience Platform
title: Guide de l’API Privacy Service
description: L’API du Privacy Service permet aux développeurs de créer et de gérer les demandes de clients d’accéder à leurs données personnelles ou de les supprimer dans des applications Experience Cloud, conformément aux règles légales de confidentialité. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 27%

---

# [!DNL Privacy Service] Guide des API

Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur qui vous permettent de gérer (d&#39;accéder et de supprimer) les données personnelles de vos personnes de données (clients) à travers les applications Adobe Experience Cloud. [!DNL Privacy Service] fournit aussi un mécanisme central d’audit et de connexion qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications [!DNL Experience Cloud]

Ce guide explique comment utiliser l&#39;API [!DNL Privacy Service]. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la [présentation de l’interface utilisateur de Privacy Service](../ui/overview.md). Pour obtenir une liste complète de tous les points de terminaison disponibles dans l&#39;API [!DNL Privacy Service], consultez la [référence API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml).

## Prise en main {#getting-started}

Ce guide nécessite une bonne compréhension des fonctionnalités [!DNL Experience Platform] suivantes :

* [[!DNL Privacy Service]](../home.md) : fournit une API RESTful et une interface utilisateur permettant de gérer l’accès et de supprimer les requêtes des propriétaires des données (les clients) dans les applications Adobe Experience Cloud.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à l’API Privacy Service.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L’exemple JSON renvoyé dans les réponses de l’API est également fourni. Pour plus d’informations sur les conventions utilisées dans la documentation pour les exemples d’appels d’API, voir la section concernant la [lecture d’exemples d’appels d’API](../../landing/troubleshooting.md) dans le guide de dépannage[!DNL Experience Platform].

## Collecter des valeurs pour les en-têtes requis

Pour appeler l&#39;API [!DNL Privacy Service], vous devez d&#39;abord rassembler vos informations d&#39;identification d&#39;accès à utiliser dans les en-têtes requis :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Cela implique d&#39;obtenir des autorisations de développeur pour [!DNL Experience Platform] dans Adobe Admin Console, puis de générer les informations d&#39;identification dans Adobe Developer Console.

### Accédez à [!DNL Experience Platform] pour les développeurs

Pour permettre aux développeurs d&#39;accéder à [!DNL Platform], suivez les premières étapes du [didacticiel d&#39;authentification des Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Une fois que vous êtes arrivé à l&#39;étape &quot;Générer les informations d&#39;identification d&#39;accès dans Adobe Developer Console&quot;, revenez à ce didacticiel pour générer les informations d&#39;identification spécifiques à [!DNL Privacy Service].

### Générer des informations d’identification d’accès

A l’aide d’Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Vos `{IMS_ORG}` et `{API_KEY}` n&#39;ont besoin d&#39;être générés qu&#39;une seule fois et peuvent être réutilisés dans les prochains appels d&#39;API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes de génération de ces valeurs sont décrites en détail ci-dessous.

#### Configuration ponctuelle

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) dans la documentation de la Console développeur de l&#39;Adobe.

Après avoir créé un nouveau projet, sélectionnez **[!UICONTROL Ajouter l&#39;API]** dans l&#39;écran **[!UICONTROL Présentation du projet]**.

![](../images/api/getting-started/add-api-button.png)

L&#39;écran **[!UICONTROL Ajouter une API]** s&#39;affiche. Sélectionnez **[!UICONTROL API du Privacy Service]** dans la liste des API disponibles avant de sélectionner **[!UICONTROL Suivant]**.

![](../images/api/getting-started/add-privacy-service-api.png)

L&#39;écran **[!UICONTROL Configurer l&#39;API]** s&#39;affiche. Sélectionnez l’option **[!UICONTROL Générer une paire de clés]**, puis sélectionnez **[!UICONTROL Générer une paire de clés]** dans le coin inférieur droit.

![](../images/api/getting-started/generate-key-pair.png)

La paire de clés est générée automatiquement et un fichier ZIP contenant une clé privée et un certificat public est téléchargé sur votre ordinateur local (à utiliser ultérieurement). Sélectionnez **[!UICONTROL Enregistrer l&#39;API configurée]** pour terminer la configuration.

![](../images/api/getting-started/key-pair-generated.png)

Une fois l&#39;API ajoutée au projet, la page du projet réapparaît sur la page **Aperçu de l&#39;API du Privacy Service**. À partir de là, faites défiler l&#39;écran jusqu&#39;à la section **[!UICONTROL Compte de service (JWT)]**, qui fournit les informations d&#39;identification d&#39;accès suivantes requises dans tous les appels à l&#39;API [!DNL Privacy Service] :

* **[!UICONTROL ID]** CLIENT : L’ID client est requis  `{API_KEY}` pour cela et doit être fourni dans l’en-tête x-api-key.
* **[!UICONTROL ID]** D&#39;ORGANISATION : L’ID d’organisation est la  `{IMS_ORG}` valeur qui doit être utilisée dans l’en-tête x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez rassembler sont votre `{ACCESS_TOKEN}`, qui est utilisé dans l’en-tête Autorisation. Contrairement aux valeurs de `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API [!DNL Platform].

Pour générer un nouveau `{ACCESS_TOKEN}`, ouvrez la clé privée précédemment téléchargée et collez son contenu dans la zone de texte située en regard de **[!UICONTROL Générer le jeton d&#39;accès]** avant de sélectionner **[!UICONTROL Générer le jeton]**.

![](../images/api/getting-started/paste-private-key.png)

Un nouveau jeton d&#39;accès est généré et un bouton permettant de copier le jeton dans le Presse-papiers est fourni. Cette valeur est utilisée pour l&#39;en-tête Autorisation requis et doit être fournie au format `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Étapes suivantes

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l&#39;API [!DNL Privacy Service]. Le document sur les [tâches liées à la confidentialité](privacy-jobs.md) décrit les différents appels API que vous pouvez lancer à l’aide de l’API [!DNL Privacy Service] Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

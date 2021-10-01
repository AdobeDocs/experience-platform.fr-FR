---
keywords: Experience Platform;accueil;rubriques populaires
solution: Experience Platform
title: Guide de l’API Privacy Service
description: L’API du Privacy Service permet aux développeurs de créer et de gérer des demandes de clients pour accéder à leurs données personnelles ou les supprimer dans des applications Experience Cloud, conformément aux réglementations légales en matière de confidentialité. Suivez ce guide pour savoir comment effectuer des opérations clés à l’aide de l’API.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 44%

---

# Guide de l’API [!DNL Privacy Service]

Adobe Experience Platform [!DNL Privacy Service] fournit une API RESTful et une interface utilisateur qui vous permettent de gérer (d’accéder et de supprimer) les données personnelles de vos sujets des données (clients) dans les applications Adobe Experience Cloud. [!DNL Privacy Service] fournit aussi un mécanisme central d’audit et de connexion qui vous permet d’accéder à l’état et aux résultats des tâches impliquant des applications [!DNL Experience Cloud]

Ce guide explique comment utiliser l’API [!DNL Privacy Service]. Pour plus d’informations sur l’utilisation de l’interface utilisateur, consultez la [présentation de l’interface utilisateur de Privacy Service](../ui/overview.md). Pour obtenir la liste complète de tous les points de terminaison disponibles dans l’API [!DNL Privacy Service], consultez la [référence API](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Prise en main {#getting-started}

Ce guide nécessite une compréhension pratique des fonctionnalités [!DNL Experience Platform] suivantes :

* [[!DNL Privacy Service]](../home.md) : fournit une API RESTful et une interface utilisateur permettant de gérer l’accès et de supprimer les requêtes des propriétaires des données (les clients) dans les applications Adobe Experience Cloud.

Les sections suivantes apportent des informations supplémentaires dont vous aurez besoin pour passer avec succès des appels à l’API Privacy Service.

### Lecture d’exemples d’appels API

Ce tutoriel fournit des exemples d’appels API pour démontrer comment formater vos requêtes. Il s’agit notamment de chemins d’accès, d’en-têtes requis et de payloads de requêtes correctement formatés. L&#39;exemple JSON renvoyé dans les réponses de l&#39;API est également fourni. Pour plus d&#39;informations sur les conventions utilisées dans la documentation pour les exemples d&#39;appels d&#39;API, voir la section concernant la [lecture d&#39;exemples d&#39;appels d&#39;API](../../landing/troubleshooting.md) dans le guide de dépannage[!DNL Experience Platform].

## Collecte des valeurs des en-têtes requis

Pour passer des appels à l’API [!DNL Privacy Service], vous devez d’abord rassembler vos informations d’identification d’accès à utiliser dans les en-têtes requis :

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Cela implique d’obtenir les autorisations des développeurs pour [!DNL Experience Platform] dans Adobe Admin Console, puis de générer les informations d’identification dans Adobe Developer Console.

### Accédez à [!DNL Experience Platform] pour les développeurs.

Pour permettre aux développeurs d’accéder à [!DNL Platform], suivez les étapes initiales du [tutoriel sur l’authentification Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#platform-apis). Une fois que vous êtes arrivé à l’étape &quot;Générer les informations d’identification d’accès dans Adobe Developer Console&quot;, revenez à ce tutoriel pour générer les informations d’identification spécifiques à [!DNL Privacy Service].

### Génération des informations d’identification d’accès

À l’aide d’Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Vos `{IMS_ORG}` et `{API_KEY}` ne doivent être générés qu’une seule fois et peuvent être réutilisés dans les futurs appels API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes de génération de ces valeurs sont décrites en détail ci-dessous.

#### Configuration ponctuelle

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création dʼun projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) disponible dans la documentation dʼAdobe Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajouter l’API]** dans l’écran **[!UICONTROL Aperçu du projet]**.

![](../images/api/getting-started/add-api-button.png)

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionnez **[!UICONTROL API Privacy Service]** dans la liste des API disponibles avant de sélectionner **[!UICONTROL Suivant]**.

![](../images/api/getting-started/add-privacy-service-api.png)

L’écran **[!UICONTROL Configurer l’API]** s’affiche. Sélectionnez l’option **[!UICONTROL Générer une paire de clés]**, puis sélectionnez **[!UICONTROL Générer la paire de clés]** dans le coin inférieur droit.

![](../images/api/getting-started/generate-key-pair.png)

La paire de clés est automatiquement générée et un fichier ZIP contenant une clé privée et un certificat public est téléchargé sur votre ordinateur local (pour être utilisé ultérieurement). Sélectionnez **[!UICONTROL Enregistrer l’API configurée]** pour terminer la configuration.

![](../images/api/getting-started/key-pair-generated.png)

Une fois l’API ajoutée au projet, la page du projet réapparaît sur la page **Aperçu de l’API du Privacy Service**. À partir de là, faites défiler l’écran jusqu’à la section **[!UICONTROL Compte de service (JWT)]**, qui fournit les informations d’identification d’accès suivantes, requises dans tous les appels à l’API [!DNL Privacy Service]

* **[!UICONTROL ID]** CLIENT : L’identifiant du client est obligatoire  `{API_KEY}` pour qui doit être fourni dans l’en-tête x-api-key.
* **[!UICONTROL ID D’ORGANIZATION]** : L’ID d’organisation est la  `{IMS_ORG}` valeur qui doit être utilisée dans l’en-tête x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez rassembler sont votre `{ACCESS_TOKEN}`, qui est utilisé dans l’en-tête d’autorisation. Contrairement aux valeurs de `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API [!DNL Platform].

Pour générer un nouveau `{ACCESS_TOKEN}`, ouvrez la clé privée précédemment téléchargée et collez son contenu dans la zone de texte en regard de **[!UICONTROL Générer un jeton d’accès]** avant de sélectionner **[!UICONTROL Générer un jeton]**.

![](../images/api/getting-started/paste-private-key.png)

Un nouveau jeton d’accès est généré et un bouton permettant de copier le jeton dans le presse-papiers est fourni. Cette valeur est utilisée pour l’en-tête Authorization requis et doit être fournie au format `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Étapes suivantes

Maintenant que vous savez quels en-têtes utiliser, vous êtes prêt à commencer à lancer des appels à l’API [!DNL Privacy Service]. Le document sur les [tâches liées à la confidentialité](privacy-jobs.md) décrit les différents appels API que vous pouvez lancer à l’aide de l’API [!DNL Privacy Service] Chaque appel d’exemple inclut le format général de l’API, un exemple de requête présentant les en-têtes requis et un exemple de réponse.

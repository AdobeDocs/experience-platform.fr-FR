---
title: Authentification
description: Découvrez comment configurer l’authentification pour l’API Adobe Experience Platform Edge Network Server.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 20%

---

# Authentification {#authentication}

## Vue d’ensemble

La variable [!DNL Edge Network Server API] gère à la fois la collecte de données authentifiées et non authentifiées, en fonction de la source des événements et du domaine de collecte de l’API.

Pour chaque requête, la variable [!DNL Server API] vérifie le flux de données [!DNL access type] . Grâce à ce paramètre, les clients peuvent configurer un flux de données pour accepter les données authentifiées ou les données authentifiées et non authentifiées. Par défaut, les deux types de données sont acceptés.

Pour plus d’informations sur la configuration du type d’accès au flux de données, consultez la documentation sur la manière de [créer et configurer un flux de données](../datastreams/overview.md#create).

Vous trouverez ci-dessous un résumé du comportement, basé sur le flux de données [!DNL Access Type] configuration et le point de terminaison sur lequel la requête est reçue.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mixte (par défaut) | N’authentifie pas la requête | Authentifie la requête |
| authentifié | Authentifie la requête | Authentifie la requête |

Appels API provenant d’un serveur privé sur `server.adobedc.net` doit toujours être authentifié.

## Conditions préalables {#prerequisites}

Avant d’effectuer des appels à la fonction [!DNL Server API], assurez-vous de respecter les conditions préalables suivantes :

* Vous disposez d’un compte d’organisation ayant accès à Adobe Experience Platform.
* Votre compte d’Experience Platform a la variable `developer` et `user` rôles activés pour le profil de produit de l’API Adobe Experience Platform. Contactez votre [Admin Console](../access-control/home.md) pour activer ces rôles pour votre compte.
* Vous avez une Adobe ID. Si vous ne possédez pas d’Adobe ID, accédez à la [Console Adobe Developer](https://developer.adobe.com/console) et créez un compte.

## Collecte des informations d’identification {#credentials}

Pour lancer des appels aux API Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](../landing/api-authentication.md). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Les ressources d’Experience Platform peuvent être isolées dans des sandbox virtuels spécifiques. Dans les requêtes aux API Platform, vous pouvez spécifier le nom et l’identifiant du sandbox dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Experience Platform, consultez la [documentation de présentation des sandbox](../sandboxes/home.md).

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Configuration des autorisations d’écriture de jeux de données {#dataset-write-permissions}

Pour configurer les autorisations d’écriture de jeux de données, accédez au [Admin Console](https://adminconsole.adobe.com), recherchez le profil de produit associé à votre clé API, puis définissez les autorisations suivantes :

* Dans le [!UICONTROL Environnements de test] , sélectionnez l’environnement de test datastream .
* Dans le [!UICONTROL Data Management] , sélectionnez **[!UICONTROL Gestion des jeux de données]** autorisation.

## Dépannage des erreurs d’autorisation {#troubleshooting-authorization}

| Code d’erreur | Message d’erreur | Description |
| --- | --- | --- |
| `EXEG-0500-401` | Jeton d’autorisation non valide | Ce message d&#39;erreur s&#39;affiche dans l&#39;une des situations suivantes :  <ul><li>La variable `authorization` valeur d’en-tête manquante.</li><li>La variable `authorization` La valeur d’en-tête n’inclut pas la valeur requise `Bearer` jeton.</li><li>Le format du jeton d’autorisation fourni n’est pas valide.</li><li>Le flux de données nécessite une authentification, mais les en-têtes requis ne sont pas présents dans la requête.</li></ul> |
| `EXEG-0501-401` | Jeton d’autorisation d’utilisateur non valide | Ce message d&#39;erreur s&#39;affiche dans l&#39;une des situations suivantes : <ul><li>L’appel API n’a pas le paramètre requis `x-user-token` en-tête .</li><li>Le format du jeton utilisateur fourni n’est pas valide.</li></ul> |
| `EXEG-0502-401` | Jeton d’autorisation non valide | Ce message d’erreur s’affiche lorsque le jeton d’autorisation fourni a un format valide (JWT), mais que sa signature n’est pas valide. Vérifiez les [tutoriel sur l’authentification](../landing/api-authentication.md) pour savoir comment obtenir un jeton JWT valide. |
| `EXEG-0503-401` | Jeton d’autorisation non valide | Ce message d’erreur s’affiche lorsque le jeton d’autorisation fourni a expiré. Accédez au [tutoriel sur l’authentification](../landing/api-authentication.md) pour générer un nouveau jeton. |
| `EXEG-0504-401` | Le contexte de produit requis est manquant | Ce message d&#39;erreur s&#39;affiche dans l&#39;une des situations suivantes :  <ul><li>Le compte de développeur n’a pas accès au contexte du produit Adobe Experience Platform.</li><li>Le compte de la société n’est pas encore autorisé à Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | La portée du jeton d’autorisation requis est manquante | Cette erreur s’applique uniquement à l’authentification du compte de service. Le message d’erreur s’affiche lorsque le jeton d’autorisation de service inclus dans l’appel appartient à un compte de service qui n’a pas accès à la variable `acp.foundation` Portée IMS. |
| `EXEG-0506-401` | Environnement de test non accessible pour l’écriture | Ce message d’erreur s’affiche lorsque le compte de développeur n’a pas `WRITE` accès à l’environnement de test de l’Experience Platform dans lequel le flux de données est défini. |

---
title: Authentification
description: Découvrez comment configurer l’authentification pour l’API Adobe Experience Platform Edge Network Server.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 21%

---

# Authentification {#authentication}

## Vue d’ensemble

Le [!DNL Edge Network Server API] gère la collecte de données authentifiées et non authentifiées, en fonction de la source des événements et du domaine de collecte de l’API.

Pour chaque requête, le [!DNL Server API] vérifie le paramètre de [!DNL access type] du flux de données. À l’aide de ce paramètre, les clients peuvent configurer un flux de données pour accepter des données authentifiées, ou des données authentifiées et non authentifiées. Par défaut, les deux types de données sont acceptés.

Pour plus d’informations sur la configuration du type d’accès au flux de données, consultez la documentation sur la [création et configuration d’un flux de données](../datastreams/overview.md#create).

Vous trouverez ci-dessous un résumé du comportement, en fonction de la configuration de l’[!DNL Access Type] du flux de données et du point d’entrée sur lequel la requête est reçue.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mixte (par défaut) | N’authentifie pas la demande | Authentifie la demande |
| authentifié | Authentifie la demande | Authentifie la demande |

Les appels d’API provenant d’un serveur privé sur `server.adobedc.net` doivent toujours être authentifiés.

## Conditions préalables {#prerequisites}

Avant d’effectuer des appels vers le [!DNL Server API] , veillez à respecter les conditions préalables suivantes :

* Vous disposez d’un compte d’organisation avec un accès à Adobe Experience Platform.
* Les rôles `developer` et `user` sont activés pour le profil de produit API Adobe Experience Platform de votre compte Experience Platform. Contactez votre administrateur [Admin Console](../access-control/home.md) pour activer ces rôles pour votre compte.
* Vous disposez d’une Adobe ID. Si vous ne disposez pas d’un Adobe ID, accédez au [Adobe Developer Console](https://developer.adobe.com/console) et créez un compte.

## Collecter les informations d’identification {#credentials}

Pour lancer des appels aux API Experience Platform, vous devez d’abord suivre le [tutoriel sur l’authentification](../landing/api-authentication.md). Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans tous les appels API Experience Platform, comme illustré ci-dessous :

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key : `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Les ressources d’Experience Platform peuvent être isolées dans des sandbox virtuels spécifiques. Dans les requêtes aux API Experience Platform, vous pouvez spécifier le nom et l’identifiant du sandbox dans lequel l’opération aura lieu. Il s’agit de paramètres facultatifs.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Pour plus d’informations sur les sandbox dans Experience Platform, consultez la [documentation de présentation des sandbox](../sandboxes/home.md).

Toutes les requêtes qui contiennent un payload (POST, PUT, PATCH) nécessitent un en-tête de type de média supplémentaire :

* Content-Type: `application/json`

## Configuration des autorisations d’écriture de jeux de données {#dataset-write-permissions}

Pour configurer les autorisations d’écriture de jeux de données, accédez à [Admin Console](https://adminconsole.adobe.com), recherchez le profil de produit associé à votre clé API et définissez les autorisations suivantes :

* Dans la section [!UICONTROL Sandbox], sélectionnez le sandbox du flux de données.
* Dans la section [!UICONTROL Gestion des données], sélectionnez l’autorisation **[!UICONTROL Gérer les jeux de données]**.

## Résolution des erreurs d’autorisation {#troubleshooting-authorization}

| Code d’erreur | Message d’erreur | Description |
| --- | --- | --- |
| `EXEG-0500-401` | Jeton d’autorisation non valide | Ce message d’erreur s’affiche dans l’une des situations suivantes :  <ul><li>La valeur de l’en-tête `authorization` est manquante.</li><li>La valeur de l’en-tête `authorization` n’inclut pas le jeton `Bearer` requis.</li><li>Le format du jeton d’autorisation fourni n’est pas valide.</li><li>Le flux de données nécessite une authentification, mais il manque des en-têtes obligatoires dans la requête.</li></ul> |
| `EXEG-0501-401` | Jeton d’autorisation d’utilisateur non valide | Ce message d’erreur s’affiche dans l’une des situations suivantes : <ul><li>L’en-tête `x-user-token` requis est manquant dans l’appel API.</li><li>Le format du jeton d’utilisateur fourni n’est pas valide.</li></ul> |
| `EXEG-0502-401` | Jeton d’autorisation non valide | Ce message d’erreur s’affiche lorsque le jeton d’autorisation fourni a un format valide (JWT), mais sa signature n’est pas valide. Consultez le [tutoriel sur l’authentification](../landing/api-authentication.md) pour savoir comment obtenir un jeton JWT valide. |
| `EXEG-0503-401` | Jeton d’autorisation non valide | Ce message d’erreur s’affiche lorsque le jeton d’autorisation fourni expire. Suivez le [tutoriel sur l’authentification](../landing/api-authentication.md) pour générer un nouveau jeton. |
| `EXEG-0504-401` | Le contexte de produit requis est manquant. | Ce message d’erreur s’affiche dans l’une des situations suivantes :  <ul><li>Le compte de développeur n’a pas accès au contexte du produit Adobe Experience Platform.</li><li>Le compte de société n’est pas encore autorisé à accéder à Adobe Experience Experience Platform.</li></ul> |
| `EXEG-0505-401` | La portée du jeton d’autorisation obligatoire est absente. | Cette erreur s’applique uniquement à l’authentification du compte de service. Le message d’erreur s’affiche lorsque le jeton d’autorisation de service inclus dans l’appel appartient à un compte de service qui n’a pas accès à la portée IMS `acp.foundation`. |
| `EXEG-0506-401` | Sandbox non accessible en écriture | Ce message d’erreur s’affiche lorsque le compte de développeur n’a pas `WRITE` accès au sandbox Experience Platform dans lequel le flux de données est défini. |

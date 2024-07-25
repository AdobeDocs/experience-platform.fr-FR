---
description: Cette page décrit comment vous authentifier et commencer à utiliser Adobe Experience Platform Destination SDK. Vous y trouverez des instructions sur la manière d’obtenir des informations d’authentification Adobe I/O, un nom de sandbox et l’autorisation de contrôle d’accès de création de destinations.
title: Prise en main de Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: f652faac7d771b590b30f591616b53d0cd2ff1eb
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 82%

---

# Prise en main

## Présentation {#overview}

Cette page décrit comment vous authentifier et commencer à utiliser Adobe Experience Platform Destination SDK. Vous y trouverez des instructions sur la manière d’obtenir des informations d’authentification Adobe I/O, un nom de sandbox et l’autorisation de contrôle d’accès de création de destinations.

## Terminologie {#terminology}

Ce guide utilise des concepts spécifiques à Platform, tels que l’organisation et les environnements de test. Consultez le [glossaire Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html?lang=fr) pour connaître la définition de ces termes. Consultez le [glossaire des Destinations SDK](/help/destinations/destination-sdk/glossary.md) pour connaître les termes liés directement à cette fonctionnalité.

## Obtenir les informations d’authentification requises {#obtain-authentication-credentials}

Destination SDK utilise la passerelle [Adobe I/O](https://www.adobe.io/) pour l’authentification. Pour effectuer des appels API vers des points d’entrée de Destination SDK, vous devez fournir certains en-têtes dans vos appels API. Demandez à l’équipe dʼAdobe Exchange de configurer votre authentification dans [Adobe Developer Console](https://developer.adobe.com/console).

Pour réaliser des appels aux points d’entrée de l’API Destination SDK, suivez le [tutoriel sur l’authentification Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Démarrez le tutoriel à partir de l’étape &quot;[Générer une clé d’API, un ID d’organisation et un secret client](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr#api-ims-secret)&quot;. L’équipe dʼAdobe Exchange effectuera les étapes précédentes à votre place. Le tutoriel d’authentification fournit les valeurs de chacun des en-têtes requis dans les appels à l’API Destination SDK, tel qu’indiqué ci-dessous :

* `x-api-key: {API_KEY}`, également appelé identifiant client.
* `x-gw-ims-org-id: {ORG_ID}`, également appelé identifiant d’organisation.
* `Authorization: Bearer {ACCESS_TOKEN}`. Le jeton d’accès a un délai d’expiration de 24 heures, exprimé en millisecondes, vous devrez donc l’actualiser. Pour actualiser le jeton d’accès, répétez les étapes décrites dans le tutoriel sur l’authentification.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Propriété de la destination et du sandbox {#destination-ownership}

Dans Experience Platform, toutes les ressources sont isolées dans des sandbox virtuels spécifiques. Les requêtes vers Destination SDK nécessitent des en-têtes qui spécifient le nom du sandbox dans lequel l’opération a lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

L’équipe dʼAdobe Exchange fournit votre nom de sandbox, que vous devez utiliser dans les appels aux points d’entrée de l’API Destination SDK.

## Contrôle d’accès en fonction du rôle (RBAC) {#rbac}

Pour utiliser les points d’entrée de l’API Destination SDK décrits dans la section [documentation de référence](functionality/configuration-options.md), vous avez besoin de l’autorisation de contrôle d’accès de **[!UICONTROL création de destinations]**. Demandez à l’équipe dʼAdobe Exchange de vous lʼaccorder dans [Adobe Admin Console](https://adminconsole.adobe.com/).

![Autorisation de création de destinations](./assets/destination-authoring-permission.png)

Pour plus d’informations, consultez les documents suivants sur le contrôle d’accès dans Experience Platform :

* [Gérer les autorisations d’un profil de produit](/help/access-control/ui/permissions.md)
* [Autorisations disponibles pour Experience Platform](/help/access-control/home.md#permissions)
* [Documentation dʼAdobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html)

## Remarques complémentaires {#additional-considerations}

* Pour les destinations productisées/publiques, toute modification que vous apportez aux configurations de destination, que vous créiez ou modifiez une configuration de destination, doit être révisée et approuvée par Adobe. Vos modifications ne sont répercutées dans vos destinations qu’une fois la révision terminée. Cela ne s’applique pas aux destinations privées qui ne sont disponibles que pour vous.
* Seuls les utilisateurs appartenant à la même organisation et ayant accès au sandbox peuvent modifier la configuration de destination.

## Étapes suivantes {#next-steps}

En suivant les étapes décrites dans cet article, vous avez obtenu des informations d’authentification pour Adobe I/O, un nom de sandbox et l’autorisation de contrôle d’accès de création de destinations. Lʼétape suivante consiste à configurer une destination à l’aide de Destination SDK.

* Consultez les guides de configuration suivants, en fonction du type de destination :

   * [Utiliser Destination SDK pour configurer une destination de diffusion en streaming](guides/configure-destination-instructions.md)
   * [Utilisation de Destination SDK pour configurer une destination basée sur des fichiers](guides/configure-file-based-destination-instructions.md)

* Pour toutes les opérations, reportez-vous à la section [Documentation de l’API de création de destinations](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Utilisez la [Collection Postman de l’API de création de destinations](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) pour configurer votre destination à l’aide des points d’entrée de l’API Destination SDK. Pour commencer à utiliser Postman, suivez les [étapes dʼimportation des environnements et des collections](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) et consultez le [Guide vidéo de création de l’environnement Postman](https://video.tv.adobe.com/v/28832).

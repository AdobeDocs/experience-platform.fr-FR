---
description: Cette page décrit comment vous authentifier et commencer à utiliser Adobe Experience Platform Destination SDK. Elle comprend des instructions sur la manière d’obtenir des informations d’authentification d’Adobe I/O, un nom d’environnement de test et l’autorisation de contrôle d’accès de création de destination.
title: Prise en main de Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 8356c63688fc57ece2f4e549a9ed0d1cc50f04db
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 6%

---

# Prise en main

## Présentation {#overview}

Cette page décrit comment vous authentifier et commencer à utiliser Adobe Experience Platform Destination SDK. Elle comprend des instructions sur la manière d’obtenir des informations d’authentification d’Adobe I/O, un nom d’environnement de test et l’autorisation de contrôle d’accès de création de destination.

## Terminologie {#terminology}

Ce guide utilise des concepts spécifiques à Platform, tels que l’organisation IMS et les environnements de test. Consultez la [Glossaire Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) pour connaître la définition de ces termes et d’autres termes.

## Obtention des informations d’authentification requises {#obtain-authentication-credentials}

Destination SDK utilise la variable [Adobe I/O](https://www.adobe.io/) passerelle pour l’authentification. Pour effectuer des appels API vers des points de terminaison Destination SDK, vous devez fournir certains en-têtes dans vos appels API. Collaborez avec l’équipe Adobe Exchange pour configurer l’authentification pour vous au [Adobe Developer Console](http://console.adobe.io/).

Pour passer avec succès des appels aux points de terminaison de l’API Destination SDK, suivez la [Tutoriel sur l’authentification des Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Démarrez le tutoriel à partir du[Génération d’une clé API, d’un identifiant de l’organisation IMS et d’un secret client](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret)&quot;. L’équipe Adobe Exchange se chargera des étapes précédentes. Le tutoriel sur l’authentification indique les valeurs de chacun des en-têtes requis dans les appels d’API Destination SDK, comme illustré ci-dessous :

* `x-api-key: {API_KEY}`, également appelé ID client
* `x-gw-ims-org-id: {IMS_ORG}`, également appelé ID d’organisation
* `Authorization: Bearer {ACCESS_TOKEN}`. Le jeton d’accès a un délai d’expiration de 24 heures, exprimé en millisecondes, vous devrez donc l’actualiser. Pour actualiser le jeton d’accès, répétez les étapes décrites dans le tutoriel sur l’authentification.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Propriété de destination et environnements de test {#destination-ownership}

Dans Experience Platform, toutes les ressources sont isolées dans des environnements de test virtuels spécifiques. Les requêtes envoyées à Destination SDK nécessitent des en-têtes qui spécifient le nom de l’environnement de test dans lequel l’opération a lieu :

* `x-sandbox-name: {SANDBOX_NAME}`

L’équipe Adobe Exchange vous fournit votre nom d’environnement de test, que vous devez utiliser dans les appels aux points de terminaison de l’API Destination SDK.

## Contrôle d’accès en fonction du rôle (RBAC) {#rbac}

Pour utiliser les points d’entrée de l’API Destination SDK décrits dans la section [documentation de référence](./configuration-options.md), vous avez besoin de la fonction **[!UICONTROL Création de destination]** autorisation de contrôle d’accès. Collaborez avec l’équipe Adobe Exchange pour que cette autorisation vous soit affectée dans [Adobe Admin Console](https://adminconsole.adobe.com/).

![Autorisation de création de destination](./assets/destination-authoring-permission.png)

Pour plus d’informations, consultez les documents de contrôle d’accès Experience Platform suivants :

* [Gestion des autorisations d’un profil de produit](/help/access-control/ui/permissions.md)
* [Autorisations disponibles pour l’Experience Platform](/help/access-control/home.md#permissions)
* [Documentation Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/using/admin-console.html)

## Remarques complémentaires {#additional-considerations}

* Toute modification apportée aux configurations de destination, que vous créiez ou modifiez une configuration de destination, doit être examinée et approuvée par Adobe. Vos modifications ne sont répercutées dans vos destinations qu’une fois la révision terminée.
* Seuls les utilisateurs appartenant à la même organisation et ayant accès à l’environnement de test peuvent modifier la configuration de destination.

## Étapes suivantes {#next-steps}

En suivant les étapes décrites dans cet article, vous obteniez des informations d’authentification pour Adobe I/O, un nom d’environnement de test et l’autorisation de contrôle d’accès de création de destination. Vous pouvez ensuite configurer une destination à l’aide de Destination SDK.
* Lecture [Utilisation de Destination SDK pour configurer votre destination](./configure-destination-instructions.md) pour les étapes suivantes.
* Pour toutes les opérations, reportez-vous à la section [Documentation de l’API de création de destination](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Utilisez la variable [Collection Postman de l’API de création de destinations](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json) pour configurer votre destination à l’aide des points de terminaison de l’API Destination SDK. Pour commencer à utiliser Postman, reportez-vous à la section [étapes pour importer des environnements et des collections](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) et un [Guide vidéo pour la création de l’environnement Postman](https://video.tv.adobe.com/v/28832).

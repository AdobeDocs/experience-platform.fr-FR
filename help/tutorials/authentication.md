---
keywords: Experience Platform;home;popular topics;Authenticate;access
solution: Experience Platform
title: Authentification et accès aux API Experience Platform
topic: tutorial
description: 'Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform. '
translation-type: tm+mt
source-git-commit: 76e6e1a5484dce0a4640c2ce1f43cf7d84e049bf
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 43%

---


# Authenticate and access [!DNL Experience Platform] APIs

This document provides a step-by-step tutorial for gaining access to an Adobe Experience Platform developer account in order to make calls to [!DNL Experience Platform] APIs.

## Authentification pour effectuer des appels API

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les requêtes aux API Adobe I/O doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Le JWT est ensuite utilisé avec des informations spécifiques au client pour générer votre jeton d&#39;accès personnel.

Ce tutoriel décrit les étapes de l’authentification par la création d’un jeton d’accès décrit dans l’organigramme suivant :
![](images/authentication/authentication-flowchart.png)

## Conditions préalables

In order to successfully make calls to [!DNL Experience Platform] APIs, you require the following:

* Une organisation IMS ayant accès à Adobe Experience Platform
* Un compte Adobe ID enregistré
* L’administrateur Admin Console doit vous ajouter en tant que **développeur** et **utilisateur** d’un produit.

Les sections suivantes décrivent les étapes à suivre pour créer un Adobe ID et devenir développeur et utilisateur pour une organisation.

### Création d’un Adobe ID

Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un en suivant les étapes suivantes :

1. Accédez à la Console développeur [d&#39;Adobe](https://console.adobe.io)
2. Cliquez sur **[!UICONTROL Créer un compte]**
3. Suivez le processus d’inscription

## Become a developer and user for [!DNL Experience Platform] for an organization

Avant de créer des intégrations sur Adobe I/O, votre compte doit disposer des autorisations de développeur pour un produit dans une organisation IMS. Dans Admin Console, vous trouverez des informations détaillées sur les comptes de développeurs dans le [document d’assistance](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html) pour la gestion des développeurs.

**Obtenir un accès en tant que développeur**

Contact an [!DNL Admin Console] administrator in your Organization to add you as a developer for one of your Organization&#39;s products using the [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

L’administrateur doit vous affecter en tant que développeur à au moins un des profils de produits pour pouvoir continuer.

![](images/authentication/add-developer.png)

Une fois que vous avez été nommé en tant que développeur, vous disposez de droits d’accès pour créer des intégrations sur [Adobe I/O](https://www.adobe.com/go/devs_console_ui_fr). Ces intégrations constituent un pipeline allant des applications et services externes à l’API Adobe.

**Obtenir un accès en tant qu’utilisateur**

Your [!DNL Admin Console] administrator must also add you to the product as a user.

![](images/authentication/assign-users.png)

Tout comme le processus d’ajout d’un développeur, l’administrateur doit vous affecter à au moins un des profils de produits pour pouvoir continuer.

![](images/authentication/assign-user-details.png)

## Générer des informations d’identification d’accès dans la Console développeur d’Adobes

>[!NOTE]
>
>Si vous suivez ce document du guide [du développeur](../privacy-service/api/getting-started.md)Privacy Service, vous pouvez maintenant revenir à ce guide pour générer les informations d’identification d’accès uniques à [!DNL Privacy Service].

A l’aide d’Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Vous `{IMS_ORG}` devez générer votre fichier une seule fois et vous pouvez le réutiliser dans les prochains appels `{API_KEY}` [!DNL Platform] d’API. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes sont décrites en détail ci-dessous.

### Configuration ponctuelle

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr) and sign in with your Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation de la Console développeur d&#39;Adobes.

Une fois que vous avez créé un nouveau projet, cliquez sur **[!UICONTROL Ajouter l’API]** dans l’écran Présentation _du_ projet.

![](images/authentication/add-api-button.png)

L’écran _Ajouter une API_ s’affiche. Cliquez sur l’icône de produit pour Adobe Experience Platform, puis sélectionnez API **** Experience Platform avant de cliquer sur **[!UICONTROL Suivant]**.

![](images/authentication/add-platform-api.png)

Une fois que vous avez sélectionné [!DNL Experience Platform] l’API à ajouter au projet, suivez les étapes décrites dans le didacticiel sur l’ [ajout d’une API à un projet à l’aide d’un compte de service (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (à partir de l’étape &quot;Configurer l’API&quot;) pour terminer le processus.

Une fois l&#39;API ajoutée au projet, la page d&#39;aperçu _du_ projet affiche les informations d&#39;identification suivantes requises dans tous les appels aux [!DNL Experience Platform] API :

* `{API_KEY}` (ID client)
* `{IMS_ORG}` (ID d’organisation)

![](./images/authentication/api-key-ims-org.png)

### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez rassembler sont les `{ACCESS_TOKEN}`vôtres. Contrairement aux valeurs pour `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser [!DNL Platform] les API.

Pour générer un nouveau jeton `{ACCESS_TOKEN}`JWT, suivez les étapes pour [générer un jeton](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) JWT dans le guide d’informations d’identification de la Console développeur.

## Tester les informations d’accès

Une fois que vous avez rassemblé les trois informations d’identification requises, vous pouvez effectuer l’appel d’API suivant. Cet appel liste toutes les classes [!DNL Experience Data Model] (XDM) dans le `global` conteneur du registre du Schéma :

**Format d’API**

```http
GET /global/classes
```

**Requête**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Si votre réponse est similaire à celle illustrée ci-dessous, vos informations d’identification sont valides et fonctionnent. (Cette réponse a été tronquée pour l’espace.)

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Utilisation de Postman pour l’authentification JWT et les appels API

[Postman](https://www.postman.com/) est un outil populaire pour travailler avec les API RESTful. Cette [publication sur le site Medium](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) explique comment configurer Postman pour qu’il effectue automatiquement l’authentification JWT et s’en serve pour utiliser les API d’Adobe Experience Platform.

## Étapes suivantes

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’identification d’accès pour [!DNL Platform] les API. Vous pouvez désormais suivre l’exemple d’appels d’API fourni dans toute la [documentation](../landing/documentation/overview.md).

Outre les valeurs d’authentification que vous avez rassemblées dans ce didacticiel, de nombreuses [!DNL Platform] API requièrent également un élément valide `{SANDBOX_NAME}` à fournir en-tête. Pour plus d’informations, consultez la [présentation des environnements de test](../sandboxes/home.md).
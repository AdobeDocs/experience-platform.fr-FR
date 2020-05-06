---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Authentification et accès aux API des plateformes d’expérience
topic: tutorial
translation-type: tm+mt
source-git-commit: e1ba476fffc164b78decd7168192714993c791bc
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 1%

---


# Authentification et accès aux API des plateformes d’expérience

Ce document fournit un didacticiel détaillé permettant d’accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels aux API Experience Platform.

## Authentifier pour effectuer des appels d’API

Pour préserver la sécurité de vos applications et de vos utilisateurs, toutes les requêtes des API d’E/S Adobe doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Le JWT est ensuite utilisé avec des informations spécifiques au client pour générer votre jeton d&#39;accès personnel.

Ce didacticiel décrit les étapes de l&#39;authentification par la création d&#39;un jeton d&#39;accès décrit dans l&#39;organigramme suivant :
![](images/authentication/authentication-flowchart.png)

## Conditions préalables

Pour réussir à appeler les API de plateforme d’expérience, vous devez disposer des éléments suivants :

* Organisation IMS ayant accès à Adobe Experience Platform
* Un compte Adobe ID enregistré
* Administrateur de la Console d’administration chargé de vous ajouter en tant que **développeur** et **utilisateur** pour un produit.

Les sections suivantes décrivent les étapes à suivre pour créer un Adobe ID et devenir développeur et utilisateur pour une organisation.

### Création d’un Adobe ID

Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un à l’aide des étapes suivantes :

1. Accédez à [Adobe Developer Console](https://console.adobe.io)
2. Cliquez sur **créer un nouveau compte.**
3. Terminer le processus d&#39;inscription

## Devenir développeur et utilisateur d’Experience Platform pour une organisation

Avant de créer des intégrations sur les E/S Adobe, votre compte doit disposer des autorisations de développeur pour un produit dans une organisation IMS. Vous trouverez des informations détaillées sur les comptes des développeurs dans la Console d&#39;administration dans le document [d&#39;](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html) assistance pour la gestion des développeurs.

**Obtenir un accès pour les développeurs**

Contactez un administrateur de la Console d’administration de votre organisation pour vous ajouter en tant que développeur pour l’un des produits de votre organisation à l’aide de la Console [d’](https://adminconsole.adobe.com/)administration.

![](images/authentication/assign-developer.png)

L’administrateur doit vous affecter en tant que développeur à au moins un profil de produits pour continuer.

![](images/authentication/add-developer.png)

Une fois que vous êtes affecté en tant que développeur, vous disposez de privilèges d’accès pour créer des intégrations sur les E/S [](https://www.adobe.com/go/devs_console_ui)Adobe. Ces intégrations constituent un pipeline reliant les applications et services externes à l’API Adobe.

**Obtenir l&#39;accès des utilisateurs**

L’administrateur de la Console d’administration doit également vous ajouter au produit en tant qu’utilisateur.

![](images/authentication/assign-users.png)

Tout comme le processus d’ajout d’un développeur, l’administrateur doit vous affecter à au moins un profil de produit pour pouvoir continuer.

![](images/authentication/assign-user-details.png)


## Générer des informations d’identification d’accès dans Adobe Developer Console

A l’aide d’Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Votre `{IMS_ORG}` et `{API_KEY}` seulement doivent être générés une seule fois et peuvent être réutilisés dans les prochains appels d’API de plate-forme. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes sont décrites en détail ci-dessous.

### Configuration ponctuelle

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel relatif à la [création d’un projet](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vide dans la documentation d’Adobe Developer Console.

Une fois que vous avez créé un nouveau projet, cliquez sur **[!UICONTROL Ajouter API]** dans l’écran Présentation _du_ projet.

![](images/authentication/add-api-button.png)

L&#39;écran _Ajouter d&#39;une API_ s&#39;affiche. Cliquez sur l’icône de produit pour Adobe Experience Platform, puis sélectionnez API **** Experience Platform avant de cliquer sur **[!UICONTROL Suivant]**.

![](images/authentication/add-platform-api.png)

Une fois que vous avez sélectionné la plateforme Experience Platform comme API à ajouter au projet, suivez les étapes décrites dans le didacticiel sur l’ [ajout d’une API à un projet à l’aide d’un compte de service (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (à partir de l’étape &quot;Configurer l’API&quot;) pour terminer le processus.

Une fois l’API ajoutée au projet, la page d’aperçu _du_ projet affiche les informations d’identification suivantes requises dans tous les appels aux API de plateforme d’expérience :

* `{API_KEY}` (ID client)
* `{IMS_ORG}` (ID d’organisation)

![](./images/authentication/api-key-ims-org.png)

### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez rassembler sont les `{ACCESS_TOKEN}`vôtres. Contrairement aux valeurs pour `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API de plateforme.

Pour générer un nouveau jeton `{ACCESS_TOKEN}`JWT, suivez les étapes pour [générer un jeton](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) JWT dans le guide d’informations d’identification de la Console développeur.

## Tester les informations d’accès

Une fois que vous avez rassemblé les trois informations d’identification requises, vous pouvez effectuer l’appel d’API suivant. Cet appel liste toutes les classes de modèle de données d’expérience (XDM) dans le `global` conteneur du registre de Schémas :

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

Si votre réponse est similaire à celle illustrée ci-dessous, vos informations d’identification sont valides et fonctionnent. (Cette réponse a été tronquée pour l’espace.)

**Réponse**

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

## Utilisation de Postman pour l’authentification JWT et les appels d’API

[Postman](https://www.getpostman.com/) est un outil très utilisé pour travailler avec les API RESTful. Cette publication [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) moyenne décrit comment configurer postman pour qu’il effectue automatiquement l’authentification JWT et l’utilise pour consommer les API de la plate-forme Adobe Experience Platform.

## Étapes suivantes

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’identification d’accès pour les API de plateformes. Vous pouvez désormais suivre l’exemple d’appels d’API fourni dans toute la [documentation](../landing/documentation/overview.md).

Outre les valeurs d’authentification que vous avez rassemblées dans ce didacticiel, de nombreuses API de plateformes nécessitent également qu’une valeur valide `{SANDBOX_NAME}` soit fournie en tant qu’en-tête. See the [sandboxes overview](../sandboxes/home.md) for more information.
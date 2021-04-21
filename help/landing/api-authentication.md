---
keywords: Experience Platform;accueil;rubriques populaires;Authentification;accès
solution: Experience Platform
title: Authentification et accès aux API Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 41%

---

# Authentifier et accéder aux [!DNL Experience Platform] API

Ce document fournit un didacticiel détaillé permettant d’accéder à un compte de développeur Adobe Experience Platform afin d’invoquer les API [!DNL Experience Platform].

## Authentification pour effectuer des appels API

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les requêtes aux API Adobe I/O doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Le JWT est ensuite utilisé avec des informations spécifiques au client pour générer votre jeton d&#39;accès personnel.

Ce tutoriel décrit les étapes de l’authentification par la création d’un jeton d’accès décrit dans l’organigramme suivant :
![](images/api-authentication/authentication-flowchart.png)

## Conditions préalables

Pour réussir à appeler les API [!DNL Experience Platform], vous devez disposer des éléments suivants :

* Une organisation IMS ayant accès à Adobe Experience Platform
* Un compte Adobe ID enregistré
* L’administrateur Admin Console doit vous ajouter en tant que **développeur** et **utilisateur** d’un produit.

Les sections suivantes décrivent les étapes à suivre pour créer un Adobe ID et devenir développeur et utilisateur pour une organisation.

### Création d’un Adobe ID

Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un en suivant les étapes suivantes :

1. Accédez à [Adobe Developer Console](https://console.adobe.io)
2. Sélectionnez **[!UICONTROL créer un nouveau compte]**.
3. Suivez le processus d’inscription

## Devenir développeur et utilisateur pour [!DNL Experience Platform] pour une organisation

Avant de créer des intégrations sur Adobe I/O, votre compte doit disposer des autorisations de développeur pour un produit dans une organisation IMS. Dans Admin Console, vous trouverez des informations détaillées sur les comptes de développeurs dans le [document d’assistance](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html) pour la gestion des développeurs.

**Obtenir un accès en tant que développeur**

Contactez un administrateur [!DNL Admin Console] de votre organisation pour vous ajouter en tant que développeur pour l’un des produits de votre organisation en utilisant [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/api-authentication/assign-developer.png)

L’administrateur doit vous affecter en tant que développeur à au moins un des profils de produits pour pouvoir continuer.

![](images/api-authentication/add-developer.png)

Une fois que vous avez été nommé en tant que développeur, vous disposez de droits d’accès pour créer des intégrations sur [Adobe I/O](https://www.adobe.com/go/devs_console_ui_fr). Ces intégrations constituent un pipeline allant des applications et services externes à l’API Adobe.

**Obtenir un accès en tant qu’utilisateur**

Votre administrateur [!DNL Admin Console] doit également vous ajouter au produit en tant qu’utilisateur.

![](images/api-authentication/assign-users.png)

Tout comme le processus d’ajout d’un développeur, l’administrateur doit vous affecter à au moins un des profils de produits pour pouvoir continuer.

![](images/api-authentication/assign-user-details.png)

## Générer des informations d’identification d’accès dans la Console développeur d’Adobes

>[!NOTE]
>
>Si vous suivez ce document du [guide du développeur Privacy Service](../privacy-service/api/getting-started.md), vous pouvez maintenant revenir à ce guide pour générer les informations d’identification d’accès uniques à [!DNL Privacy Service].

A l’aide d’Adobe Developer Console, vous devez générer les trois informations d’identification d’accès suivantes :

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Vos `{IMS_ORG}` et `{API_KEY}` n&#39;ont besoin d&#39;être générés qu&#39;une seule fois et peuvent être réutilisés dans les prochains appels d&#39;API [!DNL Platform]. Cependant, votre `{ACCESS_TOKEN}` est temporaire et doit être régénéré toutes les 24 heures.

Les étapes sont décrites en détail ci-dessous.

### Configuration ponctuelle

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) dans la documentation de la Console développeur de l&#39;Adobe.

Après avoir créé un nouveau projet, sélectionnez **[!UICONTROL Ajouter l&#39;API]** dans l&#39;écran **Présentation du projet**.

![](images/api-authentication/add-api-button.png)

L&#39;écran **Ajouter une API** s&#39;affiche. Sélectionnez l’icône de produit pour Adobe Experience Platform, puis **[!UICONTROL API Experience Platform]** avant de sélectionner **[!UICONTROL Suivant]**.

![](images/api-authentication/add-platform-api.png)

Une fois que vous avez sélectionné [!DNL Experience Platform] comme API à ajouter au projet, suivez les étapes décrites dans le didacticiel sur [l&#39;ajout d&#39;une API à un projet à l&#39;aide d&#39;un compte de service (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (à partir de l&#39;étape &quot;Configurer l&#39;API&quot;) pour terminer le processus.

Une fois l&#39;API ajoutée au projet, la page **Présentation du projet** affiche les informations d&#39;identification suivantes requises dans tous les appels aux API [!DNL Experience Platform] :

* `{API_KEY}` (Identifiant du client)
* `{IMS_ORG}` (ID d’organisation)

![](./images/api-authentication/api-key-ims-org.png)

### Authentification pour chaque session

Les dernières informations d’identification requises que vous devez rassembler sont votre `{ACCESS_TOKEN}`. Contrairement aux valeurs de `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API [!DNL Platform].

Pour générer un nouveau `{ACCESS_TOKEN}`, suivez les étapes pour [générer un jeton JWT](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) dans le guide d&#39;identification de la Console développeur.

## Tester les informations d’accès

Une fois que vous avez rassemblé les trois informations d’identification requises, vous pouvez effectuer l’appel d’API suivant. Cet appel liste toutes les classes [!DNL Experience Data Model] (XDM) dans le conteneur `global` du registre de Schémas :

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

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’identification d’accès pour les API [!DNL Platform]. Vous pouvez désormais suivre les exemples fournis dans le guide de prise en main [des API de plateforme](api-guide.md). Ce guide contient des liens vers les guides d’API pour chaque service de plateforme et fournit des informations supplémentaires. sur les erreurs, Postman et JSON.

Outre les valeurs d&#39;authentification que vous avez rassemblées dans ce didacticiel, de nombreuses API [!DNL Platform] nécessitent également un `{SANDBOX_NAME}` valide pour être fournies en tant qu&#39;en-tête. Pour plus d’informations, consultez la [présentation des environnements de test](../sandboxes/home.md).

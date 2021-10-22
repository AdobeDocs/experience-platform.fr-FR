---
keywords: Experience Platform ; accueil ; rubriques populaires ; Authentification ; accès
solution: Experience Platform
title: Authentification et accès aux API Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 19%

---


# Authentification et accès aux API Experience Platform

Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform. À la fin de ce tutoriel, vous avez généré les informations d’identification suivantes requises pour tous les appels d’API de plate-forme :

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les requêtes aux API Adobe I/O doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Un JWT est utilisé avec des informations spécifiques au client pour générer votre jeton d&#39;accès personnel.

Ce tutoriel explique comment recueillir les informations d’identification requises pour authentifier les appels d’API de plate-forme, comme indiqué dans l’organigramme suivant :

![](./images/api-authentication/authentication-flowchart.png)

## Conditions préalables

Pour réussir à appeler des API Experience Platform, vous devez disposer des éléments suivants :

* Une organisation IMS ayant accès à Adobe Experience Platform.
* Administrateur Admin Console capable de vous ajouter en tant que développeur et utilisateur pour un profil de produit.

Vous devez également disposer d’un Adobe ID pour suivre ce tutoriel. Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un en suivant les étapes suivantes :

1. Aller à [Adobe Developer Console](https://console.adobe.io).
2. Sélectionner **[!UICONTROL Créer un compte]**.
3. Terminer le processus d’inscription.

## Bénéficier d’un accès développeur et utilisateur pour l’Experience Platform

Avant de créer des intégrations sur Adobe Developer Console, votre compte doit disposer d’autorisations de développeur et d’utilisateur pour un profil de produit Experience Platform à Adobe Admin Console.

### Obtenir un accès en tant que développeur

Contactez un [!DNL Admin Console] administrateur de votre organisation pour vous ajouter en tant que développeur à un profil de produit Experience Platform à l’aide de la [[!DNL Admin Console]](https://adminconsole.adobe.com/). Voir la section [!DNL Admin Console] documentation pour des instructions spécifiques sur la façon de procéder [gérer l’accès développeur pour les profils de produit](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Une fois que vous êtes affecté en tant que développeur, vous pouvez commencer à créer des intégrations dans [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Ces intégrations constituent un pipeline d’applications et de services externes vers des API d’Adobe.

### Obtenir un accès en tant qu’utilisateur

Votre [!DNL Admin Console] l’administrateur doit également vous ajouter en tant qu’utilisateur au même profil de produit. Consultez le guide sur [gestion des groupes d’utilisateurs dans [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) pour plus d’informations.

## Génération d’une clé d’API, d’un ID d’organisation IMS et d’un secret client {#api-ims-secret}

>[!NOTE]
>
>Si vous suivez ce document à partir de l’onglet [Guide de l’API Privacy Service](../privacy-service/api/getting-started.md), vous pouvez maintenant revenir à ce guide pour générer des informations d’identification d’accès uniques à [!DNL Privacy Service].

Une fois que vous avez reçu un accès développeur et utilisateur à la plate-forme via [!DNL Admin Console], l’étape suivante consiste à générer votre `{IMS_ORG}` et `{API_KEY}` informations d’identification dans Adobe Developer Console. Ces informations d’identification ne doivent être générées qu’une seule fois et peuvent être réutilisées dans les prochains appels d’API de plate-forme.

### Ajouter un Experience Platform à un projet

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création dʼun projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) disponible dans la documentation dʼAdobe Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajouter une API]** sur **[!UICONTROL Présentation du projet]** écran.

![](./images/api-authentication/add-api.png)

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionnez l’icône de produit pour Adobe Experience Platform, puis choisissez **[!UICONTROL API Experience Platform]** avant **[!UICONTROL Suivant]**.

![](./images/api-authentication/platform-api.png)

À partir de là, suivez les étapes décrites dans le tutoriel sur [ajout d’une API à un projet à l’aide d’un compte de service (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (à partir de l’étape &quot;Configurer l’API&quot;) pour terminer le processus.

>[!IMPORTANT]
>
>À une certaine étape du processus lié ci-dessus, votre navigateur télécharge automatiquement une clé privée et un certificat public associé. Notez que cette clé privée est stockée sur votre ordinateur, car elle est requise à une étape ultérieure de ce tutoriel.

### Collecte des informations d’identification

Une fois que l’API a été ajoutée au projet, la **[!UICONTROL API Experience Platform]** pour le projet affiche les informations d’identification suivantes requises dans tous les appels aux API Experience Platform :

* `{API_KEY}` ([!UICONTROL Identifiant du client])
* `{IMS_ORG}` ([!UICONTROL ID d’organisation])

![](././images/api-authentication/api-key-ims-org.png)

En plus des informations d’identification ci-dessus, vous avez également besoin de la **[!UICONTROL Secret client]** pour une étape future. Sélectionner **[!UICONTROL Récupérer le secret client]** pour afficher la valeur, puis copiez-la pour une utilisation ultérieure.

![](././images/api-authentication/client-secret.png)

## Génération d’un jeton Web JSON (JWT) {#jwt}

L’étape suivante consiste à générer un JSON Web Token (JWT) en fonction des informations d’identification de votre compte. Cette valeur est utilisée pour générer votre `{ACCESS_TOKEN}` informations d’identification à utiliser dans les appels d’API de plate-forme, qui doivent être régénérés toutes les 24 heures.

Sélectionner **[!UICONTROL Compte de service (JWT)]** dans la barre de navigation de gauche, puis sélectionnez **[!UICONTROL Générer JWT]**.

![](././images/api-authentication/generate-jwt.png)

Dans la zone de texte fournie sous **[!UICONTROL Générer des fichiers JWT personnalisés]**, collez le contenu de la clé privée que vous avez générée précédemment lors de l’ajout de l’API de plate-forme à votre compte de service. Ensuite, sélectionnez **[!UICONTROL Générer un jeton]**.

![](././images/api-authentication/paste-key.png)

La page est mise à jour pour afficher le JWT généré, ainsi qu’un exemple de commande cURL qui vous permet de générer un jeton d’accès. Pour les besoins de ce tutoriel, sélectionnez **[!UICONTROL Copier]** en regard de **[!UICONTROL JWT généré]** pour copier le jeton dans votre presse-papiers.

![](././images/api-authentication/copy-jwt.png)

## Génération d’un jeton d’accès

Une fois que vous avez généré un JWT, vous pouvez l’utiliser dans un appel d’API pour générer votre `{ACCESS_TOKEN}`. Contrairement aux valeurs de `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API de plate-forme.

**Requête**

La demande suivante génère une nouvelle `{ACCESS_TOKEN}` en fonction des informations d’identification fournies dans la charge. Ce point de terminaison accepte uniquement les données de formulaire comme charge utile. Il doit donc recevoir un `Content-Type` en-tête de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propriété | Description |
| --- | --- |
| `{API_KEY}` | Le `{API_KEY}` ([!UICONTROL ID client]) que vous avez récupéré dans un fichier [étape précédente](#api-ims-secret). |
| `{SECRET}` | Le secret client que vous avez récupéré dans un fichier [étape précédente](#api-ims-secret). |
| `{JWT}` | JWT que vous avez généré dans un fichier [étape précédente](#jwt). |

>[!NOTE]
>
>Vous pouvez utiliser la même clé d’API, le même secret client et JWT pour générer un nouveau jeton d’accès pour chaque session. Cela vous permet d’automatiser la génération de jetons d’accès dans vos applications.

**Réponse**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Propriété | Description |
| --- | --- |
| `token_type` | Type de jeton renvoyé. Pour les jetons d’accès, cette valeur est toujours `bearer`. |
| `access_token` | La `{ACCESS_TOKEN}`. Cette valeur, précédée du mot `Bearer`, est requis en tant que `Authentication` pour tous les appels d’API de plate-forme. |
| `expires_in` | Nombre de millisecondes restant jusqu’à l’expiration du jeton d’accès. Une fois cette valeur atteinte, un nouveau jeton d’accès doit être généré pour continuer à utiliser les API de plate-forme. |

## Test des informations d&#39;accès

Une fois que vous avez rassemblé les trois informations d’identification requises, vous pouvez essayer d’effectuer l’appel d’API suivant. Cet appel répertorie toutes les normes [!DNL Experience Data Model] (XDM) classes disponibles pour votre entreprise.

**Requête**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Réponse**

Si votre réponse est similaire à celle présentée ci-dessous, vos informations d’identification sont valides et fonctionnent. (Cette réponse a été tronquée pour l’espace.)

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

## Utiliser Postman pour authentifier et tester les appels d’API

[Postman](https://www.postman.com/) est un outil populaire qui permet aux développeurs d’explorer et de tester les API RESTful. Ceci [Publication moyenne](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) décrit comment configurer Postman pour effectuer automatiquement l&#39;authentification JWT et l&#39;utiliser pour utiliser les API de plate-forme.

## Étapes suivantes

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’accès pour les API de plate-forme. Vous pouvez désormais suivre l’exemple d’appels d’API fournis dans l’ensemble de la [documentation](../landing/documentation/overview.md).

Outre les valeurs d’authentification que vous avez rassemblées dans ce tutoriel, de nombreuses API de plate-forme nécessitent également un `{SANDBOX_NAME}` à fournir en tant qu’en-tête. Pour plus d’informations, consultez la [présentation des environnements de test](../sandboxes/home.md).
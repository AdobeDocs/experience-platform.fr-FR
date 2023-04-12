---
keywords: Experience Platform;accueil;rubriques populaires;Authentification;accès
solution: Experience Platform
title: Authentification et accès aux API Experience Platform
type: Tutorial
description: Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 16%

---


# S’authentifier et accéder aux API Experience Platform

Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform. À la fin de ce tutoriel, vous aurez généré les informations d’identification suivantes requises pour tous les appels d’API Platform :

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les requêtes aux API Adobe I/O doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Un jeton JWT est utilisé avec des informations spécifiques au client pour générer votre jeton d’accès personnel.

Ce tutoriel explique comment rassembler les informations d’identification requises pour authentifier les appels API Platform, comme indiqué dans l’organigramme suivant :

![](./images/api-authentication/authentication-flowchart.png)

## Conditions préalables

Pour passer avec succès des appels à des API Experience Platform, vous devez disposer des éléments suivants :

* Une organisation ayant accès à Adobe Experience Platform.
* Administrateur de Admin Console capable de vous ajouter en tant que développeur et utilisateur pour un profil de produit.

Vous devez également disposer d’un Adobe ID pour suivre ce tutoriel. Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un en suivant les étapes suivantes :

1. Accédez à [Console Adobe Developer](https://console.adobe.io).
2. Sélectionner **[!UICONTROL Création d’un compte]**.
3. Terminez le processus d’inscription.

## Obtenir un accès développeur et utilisateur pour les Experience Platform

Avant de créer des intégrations sur Adobe Developer Console, votre compte doit disposer des autorisations de développeur et d’utilisateur pour un profil de produit Experience Platform dans Adobe Admin Console.

### Obtenir un accès en tant que développeur

Contactez un [!DNL Admin Console] administrateur de votre entreprise pour vous ajouter en tant que développeur à un profil de produit Experience Platform à l’aide de la variable [[!DNL Admin Console]](https://adminconsole.adobe.com/). Voir [!DNL Admin Console] documentation pour obtenir des instructions spécifiques sur la manière de procéder [gérer l’accès des développeurs pour les profils de produit ;](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Une fois que vous êtes désigné en tant que développeur, vous pouvez commencer à créer des intégrations dans [Console Adobe Developer](https://www.adobe.com/go/devs_console_ui). Ces intégrations constituent un pipeline allant des applications et services externes vers les API d’Adobe.

### Obtenir un accès en tant qu’utilisateur

Votre [!DNL Admin Console] L’administrateur doit également vous ajouter en tant qu’utilisateur au même profil de produit. Consultez le guide sur la [gestion des groupes d’utilisateurs dans [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) pour plus d’informations.

## Génération d’une clé API, d’un ID d’organisation et d’un secret client {#api-ims-secret}

>[!NOTE]
>
>Si vous suivez ce document à partir de la [Guide de l’API Privacy Service](../privacy-service/api/getting-started.md), vous pouvez maintenant revenir à ce guide pour générer les informations d’identification d’accès uniques à [!DNL Privacy Service].

Une fois que vous avez reçu l’accès développeur et utilisateur à Platform via [!DNL Admin Console], l’étape suivante consiste à générer votre `{ORG_ID}` et `{API_KEY}` informations d’identification dans la console Adobe Developer. Ces informations d’identification ne doivent être générées qu’une seule fois et peuvent être réutilisées dans les futurs appels d’API Platform.

### Ajout d’un Experience Platform à un projet

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création dʼun projet vide](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) disponible dans la documentation dʼAdobe Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajout d’une API]** sur le **[!UICONTROL Présentation du projet]** écran.

![](./images/api-authentication/add-api.png)

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionnez l’icône de produit pour Adobe Experience Platform, puis choisissez **[!UICONTROL API Experience Platform]** avant de sélectionner **[!UICONTROL Suivant]**.

![](./images/api-authentication/platform-api.png)

À partir de là, suivez les étapes décrites dans le tutoriel sur [Ajout d’une API à un projet à l’aide d’un compte de service (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (à partir de l’étape &quot;Configurer l’API&quot;) pour terminer le processus.

>[!IMPORTANT]
>
>A une certaine étape du processus lié ci-dessus, votre navigateur télécharge automatiquement une clé privée et un certificat public associé. Notez où cette clé privée est stockée sur votre ordinateur, puisqu’elle est requise à une étape ultérieure de ce tutoriel.

### Collectez les informations d’identification de .

Une fois l’API ajoutée au projet, la variable **[!UICONTROL API Experience Platform]** La page du projet affiche les informations d’identification suivantes, requises dans tous les appels aux API Experience Platform :

* `{API_KEY}` ([!UICONTROL Identifiant client])
* `{ORG_ID}` ([!UICONTROL ID d’organisation])

![](././images/api-authentication/api-key-ims-org.png)

Outre les informations d’identification ci-dessus, vous avez également besoin de la variable **[!UICONTROL Secret du client]** pour une prochaine étape. Sélectionner **[!UICONTROL Récupération du secret client]** pour afficher la valeur, puis la copier pour une utilisation ultérieure.

![](././images/api-authentication/client-secret.png)

## Génération d’un jeton Web JSON (JWT) {#jwt}

L’étape suivante consiste à générer un jeton Web JSON (JWT) basé sur les informations d’identification de votre compte. Cette valeur est utilisée pour générer votre `{ACCESS_TOKEN}` informations d’identification à utiliser dans les appels API Platform, qui doivent être régénérés toutes les 24 heures.

>[!IMPORTANT]
>
>Pour les besoins de ce tutoriel, les étapes ci-dessous indiquent comment générer un jeton JWT dans Developer Console. Cependant, cette méthode de génération ne doit être utilisée qu’à des fins de test et d’évaluation.
>
>Pour une utilisation régulière, le jeton JWT doit être généré automatiquement. Pour plus d’informations sur la manière de générer des jetons JWT par programmation, reportez-vous à la section [Guide d’authentification de compte de service](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) sur Adobe Developer.

Sélectionner **[!UICONTROL Compte de service (JWT)]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Génération de JWT]**.

![](././images/api-authentication/generate-jwt.png)

Dans la zone de texte fournie sous **[!UICONTROL Génération d’un JWT personnalisé]**, collez le contenu de la clé privée que vous avez générée précédemment lors de l’ajout de l’API Platform à votre compte de service. Sélectionnez ensuite **[!UICONTROL Générer un jeton]**.

![](././images/api-authentication/paste-key.png)

La page se met à jour pour afficher le JWT généré, ainsi qu’un exemple de commande cURL qui vous permet de générer un jeton d’accès. Pour les besoins de ce tutoriel, sélectionnez **[!UICONTROL Copier]** en regard de **[!UICONTROL JWT généré]** pour copier le jeton dans le presse-papiers.

![](././images/api-authentication/copy-jwt.png)

## Génération d’un jeton d’accès

Une fois que vous avez généré un jeton JWT, vous pouvez l’utiliser dans un appel API pour générer votre `{ACCESS_TOKEN}`. Contrairement aux valeurs de `{API_KEY}` et `{ORG_ID}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API de Platform.

**Requête**

La requête suivante génère une nouvelle `{ACCESS_TOKEN}` en fonction des informations d’identification fournies dans la payload. Ce point de terminaison accepte uniquement les données de formulaire comme charge utile. Il doit donc recevoir une `Content-Type` en-tête de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propriété | Description |
| --- | --- |
| `{API_KEY}` | Le `{API_KEY}` ([!UICONTROL ID client]) que vous avez récupéré dans une [étape précédente](#api-ims-secret). |
| `{SECRET}` | Le secret client que vous avez récupéré dans une [étape précédente](#api-ims-secret). |
| `{JWT}` | Le jeton JWT que vous avez généré dans une [étape précédente](#jwt). |

>[!NOTE]
>
>Vous pouvez utiliser la même clé API, le même secret client et JWT pour générer un nouveau jeton d’accès pour chaque session. Vous pouvez ainsi automatiser la génération des jetons d’accès dans vos applications.

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
| `access_token` | La variable `{ACCESS_TOKEN}`. Cette valeur, précédée du mot `Bearer`, est requis en tant que `Authentication` en-tête de tous les appels API Platform. |
| `expires_in` | Nombre de millisecondes restantes jusqu’à l’expiration du jeton d’accès. Une fois cette valeur atteinte, un nouveau jeton d’accès doit être généré pour continuer à utiliser les API Platform. |

## Tester les informations d’accès

Une fois que vous avez rassemblé les trois informations d’identification requises, vous pouvez effectuer l’appel API suivant. Cet appel répertorie toutes les [!DNL Experience Data Model] Classes (XDM) disponibles pour votre entreprise.

**Requête**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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

## Utilisation de Postman pour authentifier et tester les appels API

[Postman](https://www.postman.com/) est un outil populaire qui permet aux développeurs d’explorer et de tester les API RESTful. Ceci [Publication moyenne](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) décrit comment configurer Postman pour effectuer automatiquement l’authentification JWT et l’utiliser pour utiliser les API Platform.

## Étapes suivantes

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’identification d’accès pour les API Platform. Vous pouvez désormais suivre les exemples d’appels API fournis dans le [documentation](../landing/documentation/overview.md).

Outre les valeurs d’authentification que vous avez collectées dans ce tutoriel, de nombreuses API Platform nécessitent également un `{SANDBOX_NAME}` à fournir en tant qu’en-tête. Pour plus d’informations, consultez la [Présentation des sandbox](../sandboxes/home.md).
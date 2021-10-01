---
keywords: Experience Platform;accueil;rubriques populaires;Authentification;accès
solution: Experience Platform
title: Authentification et accès aux API Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 19%

---


# Authentification et accès aux API Experience Platform

Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform. À la fin de ce tutoriel, vous aurez généré les informations d’identification suivantes requises pour tous les appels d’API Platform :

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les requêtes aux API Adobe I/O doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Un jeton JWT est utilisé avec des informations spécifiques au client pour générer votre jeton d’accès personnel.

Ce tutoriel explique comment rassembler les informations d’identification requises pour authentifier les appels API Platform, comme indiqué dans l’organigramme suivant :

![](./images/api-authentication/authentication-flowchart.png)

## Conditions préalables

Pour passer avec succès des appels à des API Experience Platform, vous devez disposer des éléments suivants :

* Une organisation IMS ayant accès à Adobe Experience Platform.
* Administrateur de Admin Console capable de vous ajouter en tant que développeur et utilisateur pour un profil de produit.

Vous devez également disposer d’un Adobe ID pour suivre ce tutoriel. Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un en suivant les étapes suivantes :

1. Accédez à [Adobe Developer Console](https://console.adobe.io).
2. Sélectionnez **[!UICONTROL Créer un nouveau compte]**.
3. Terminez le processus d’inscription.

## Obtenir un accès développeur et utilisateur pour les Experience Platform

Avant de créer des intégrations sur Adobe Developer Console, votre compte doit disposer des autorisations de développeur et d’utilisateur pour un profil de produit Experience Platform dans Adobe Admin Console.

### Obtenir un accès en tant que développeur

Contactez un administrateur [!DNL Admin Console] de votre entreprise pour vous ajouter en tant que développeur à un profil de produit Experience Platform à l’aide de [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consultez la [!DNL Admin Console] documentation pour obtenir des instructions spécifiques sur la façon de [gérer l’accès des développeurs pour les profils de produit](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Une fois que vous avez été affecté en tant que développeur, vous pouvez commencer à créer des intégrations dans [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Ces intégrations constituent un pipeline allant des applications et services externes vers les API d’Adobe.

### Obtenir un accès en tant qu’utilisateur

Votre administrateur [!DNL Admin Console] doit également vous ajouter en tant qu’utilisateur au même profil de produit. Pour plus d’informations, consultez le guide sur la [gestion des groupes d’utilisateurs dans [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) .

## Génération d’une clé API, d’un identifiant de l’organisation IMS et d’un secret client {#api-ims-secret}

>[!NOTE]
>
>Si vous suivez ce document à partir du [guide de développement du Privacy Service](../privacy-service/api/getting-started.md), vous pouvez désormais revenir à ce guide pour générer les informations d’identification d’accès uniques à [!DNL Privacy Service].

Une fois que vous avez reçu l’accès utilisateur et développeur à Platform via [!DNL Admin Console], l’étape suivante consiste à générer vos informations d’identification `{IMS_ORG}` et `{API_KEY}` dans Adobe Developer Console. Ces informations d’identification ne doivent être générées qu’une seule fois et peuvent être réutilisées dans les futurs appels d’API Platform.

### Ajout d’un Experience Platform à un projet

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création dʼun projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) disponible dans la documentation dʼAdobe Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajouter l’API]** dans l’écran **[!UICONTROL Aperçu du projet]**.

![](./images/api-authentication/add-api.png)

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionnez l’icône de produit pour Adobe Experience Platform, puis choisissez **[!UICONTROL API Experience Platform]** avant de sélectionner **[!UICONTROL Suivant]**.

![](./images/api-authentication/platform-api.png)

À partir de là, suivez les étapes décrites dans le tutoriel sur l’[ajout d’une API à un projet à l’aide d’un compte de service (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (à partir de l’étape &quot;Configurer l’API&quot;) pour terminer le processus.

>[!IMPORTANT]
>
>A une certaine étape du processus lié ci-dessus, votre navigateur télécharge automatiquement une clé privée et un certificat public associé. Notez où cette clé privée est stockée sur votre ordinateur, puisqu’elle est requise à une étape ultérieure de ce tutoriel.

### Collecte des informations d’identification

Une fois l’API ajoutée au projet, la page **[!UICONTROL API Experience Platform]** du projet affiche les informations d’identification suivantes, requises dans tous les appels aux API Experience Platform :

* `{API_KEY}` ([!UICONTROL Identifiant du client])
* `{IMS_ORG}` ([!UICONTROL ID d’organisation])

![](././images/api-authentication/api-key-ims-org.png)

Outre les informations d’identification ci-dessus, vous aurez également besoin du **[!UICONTROL secret client]** généré pour une prochaine étape. Sélectionnez **[!UICONTROL Récupérer le secret client]** pour afficher la valeur, puis copiez-la pour une utilisation ultérieure.

![](././images/api-authentication/client-secret.png)

## Génération d’un jeton Web JSON (JWT) {#jwt}

L’étape suivante consiste à générer un jeton Web JSON (JWT) basé sur les informations d’identification de votre compte. Cette valeur est utilisée pour générer vos informations d’identification `{ACCESS_TOKEN}` à utiliser dans les appels API Platform, qui doivent être régénérés toutes les 24 heures.

Sélectionnez **[!UICONTROL Compte de service (JWT)]** dans le volet de navigation de gauche, puis sélectionnez **[!UICONTROL Générer JWT]**.

![](././images/api-authentication/generate-jwt.png)

Dans la zone de texte fournie sous **[!UICONTROL Generate custom JWT]**, collez le contenu de la clé privée que vous avez précédemment générée lors de l’ajout de l’API Platform à votre compte de service. Sélectionnez ensuite **[!UICONTROL Générer le jeton]**.

![](././images/api-authentication/paste-key.png)

La page se met à jour pour afficher le JWT généré, ainsi qu’un exemple de commande cURL qui vous permet de générer un jeton d’accès. Pour les besoins de ce tutoriel, sélectionnez **[!UICONTROL Copier]** en regard de **[!UICONTROL JWT généré]** pour copier le jeton dans le presse-papiers.

![](././images/api-authentication/copy-jwt.png)

## Génération d’un jeton d’accès

Une fois que vous avez généré un jeton JWT, vous pouvez l’utiliser dans un appel API pour générer votre `{ACCESS_TOKEN}`. Contrairement aux valeurs de `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API de Platform.

**Requête**

La requête suivante génère un nouveau `{ACCESS_TOKEN}` en fonction des informations d’identification fournies dans la payload. Ce point de terminaison accepte uniquement les données de formulaire comme charge utile. Il doit donc se voir attribuer un en-tête `Content-Type` de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propriété | Description |
| --- | --- |
| `{API_KEY}` | `{API_KEY}` ([!UICONTROL ID client]) que vous avez récupéré à l’étape [précédente](#api-ims-secret). |
| `{SECRET}` | Secret client que vous avez récupéré à l’étape [précédente](#api-ims-secret). |
| `{JWT}` | JWT que vous avez généré dans une [étape précédente](#jwt). |

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
| `access_token` | Le `{ACCESS_TOKEN}` généré. Cette valeur, précédée du mot `Bearer`, est requise en tant qu’en-tête `Authentication` pour tous les appels d’API Platform. |
| `expires_in` | Nombre de millisecondes restantes jusqu’à l’expiration du jeton d’accès. Une fois cette valeur atteinte, un nouveau jeton d’accès doit être généré pour continuer à utiliser les API Platform. |

## Tester les informations d’accès

Une fois que vous avez rassemblé les trois informations d’identification requises, vous pouvez effectuer l’appel API suivant. Cet appel répertorie toutes les classes [!DNL Experience Data Model] (XDM) standard disponibles pour votre organisation.

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

## Utilisation de Postman pour authentifier et tester les appels API

[](https://www.postman.com/) Postmanis est un outil populaire qui permet aux développeurs d’explorer et de tester les API RESTful. Cette [publication moyenne](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) décrit comment configurer Postman pour qu’il effectue automatiquement l’authentification JWT et l’utilise pour utiliser les API de Platform.

## Étapes suivantes

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’identification d’accès pour les API Platform. Vous pouvez désormais suivre l’exemple d’appels API fourni dans la [documentation](../landing/documentation/overview.md).

Outre les valeurs d’authentification que vous avez collectées dans ce tutoriel, de nombreuses API Platform nécessitent également qu’un `{SANDBOX_NAME}` valide soit fourni en tant qu’en-tête. Pour plus d’informations, consultez la [présentation des environnements de test](../sandboxes/home.md).
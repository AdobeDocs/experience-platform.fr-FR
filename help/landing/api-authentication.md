---
keywords: Experience Platform;accueil;rubriques populaires;Authentification;accès
solution: Experience Platform
title: Authentification et accès aux API Experience Platform
topic-legacy: tutorial
type: Tutorial
description: Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 15%

---


# Authentification et accès aux API Experience Platform

Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform. À la fin de ce didacticiel, vous aurez généré les informations d’identification suivantes requises pour tous les appels d’API de plate-forme :

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les requêtes aux API Adobe I/O doivent être authentifiées et autorisées à l’aide de normes telles que OAuth et JSON Web Tokens (JWT). Un JWT est utilisé avec des informations spécifiques au client pour générer votre jeton d&#39;accès personnel.

Ce didacticiel explique comment rassembler les informations d’identification requises pour authentifier les appels d’API de plate-forme, comme indiqué dans l’organigramme suivant :

![](./images/api-authentication/authentication-flowchart.png)

## Conditions préalables  

Pour pouvoir invoquer les API Experience Platform avec succès, vous devez disposer des éléments suivants :

* Une organisation IMS ayant accès à Adobe Experience Platform.
* Administrateur Admin Console capable de vous ajouter en tant que développeur et utilisateur pour un profil de produits.

Vous devez également disposer d’une Adobe ID pour compléter ce didacticiel. Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un en suivant les étapes suivantes :

1. Accédez à [Adobe Developer Console](https://console.adobe.io).
2. Sélectionnez **[!UICONTROL Créer un nouveau compte]**.
3. Terminez le processus d&#39;inscription.

## Obtenir l&#39;accès des développeurs et des utilisateurs pour les Experience Platform

Avant de créer des intégrations sur Adobe Developer Console, votre compte doit disposer d’autorisations de développeur et d’utilisateur pour un profil de produits Experience Platform à Adobe Admin Console.

### Obtenir un accès en tant que développeur

Contactez un administrateur [!DNL Admin Console] de votre organisation pour vous ajouter en tant que développeur à un profil de produit Experience Platform en utilisant [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consultez la documentation [!DNL Admin Console] pour obtenir des instructions spécifiques sur la façon de [gérer l&#39;accès des développeurs pour les profils de produits](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Une fois que vous êtes affecté en tant que développeur, vous pouvez début à la création d&#39;intégrations dans [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_fr). Ces intégrations constituent un pipeline allant des applications et services externes aux API d’Adobe.

### Obtenir un accès en tant qu’utilisateur

Votre administrateur [!DNL Admin Console] doit également vous ajouter en tant qu&#39;utilisateur au même profil de produits. Pour plus d’informations, consultez le guide intitulé [gestion des groupes d’utilisateurs dans  [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html).

## Générer une clé d’API, un ID d’organisation IMS et un secret client {#api-ims-secret}

>[!NOTE]
>
>Si vous suivez ce document du [guide du développeur Privacy Service](../privacy-service/api/getting-started.md), vous pouvez maintenant revenir à ce guide pour générer les informations d’identification d’accès uniques à [!DNL Privacy Service].

Une fois que vous avez obtenu l&#39;accès des développeurs et des utilisateurs à la plate-forme via [!DNL Admin Console], l&#39;étape suivante consiste à générer vos `{IMS_ORG}` et `{API_KEY}` informations d&#39;identification dans Adobe Developer Console. Ces informations d’identification ne doivent être générées qu’une seule fois et peuvent être réutilisées dans les prochains appels d’API de plate-forme.

### Ajouter un Experience Platform à un projet

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le didacticiel sur la [création d&#39;un projet vide](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) dans la documentation de la Console développeur de l&#39;Adobe.

Après avoir créé un nouveau projet, sélectionnez **[!UICONTROL Ajouter l&#39;API]** dans l&#39;écran **[!UICONTROL Présentation du projet]**.

![](./images/api-authentication/add-api.png)

L&#39;écran **[!UICONTROL Ajouter une API]** s&#39;affiche. Sélectionnez l’icône de produit pour Adobe Experience Platform, puis **[!UICONTROL API Experience Platform]** avant de sélectionner **[!UICONTROL Suivant]**.

![](./images/api-authentication/platform-api.png)

À partir de là, suivez les étapes décrites dans le didacticiel sur l&#39;[ajout d&#39;une API à un projet à l&#39;aide d&#39;un compte de service (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (à partir de l&#39;étape &quot;Configurer l&#39;API&quot;) pour terminer le processus.

>[!IMPORTANT]
>
>A une certaine étape du processus lié ci-dessus, votre navigateur télécharge automatiquement une clé privée et un certificat public associé. Notez où cette clé privée est stockée sur votre ordinateur, car elle est requise à une étape ultérieure de ce didacticiel.

### Collecte des informations d’identification

Une fois l&#39;API ajoutée au projet, la page **[!UICONTROL API Experience Platform]** du projet affiche les informations d&#39;identification suivantes requises dans tous les appels aux API Experience Platform :

* `{API_KEY}` ([!UICONTROL Identifiant du client])
* `{IMS_ORG}` ([!UICONTROL ID d’organisation])

![](././images/api-authentication/api-key-ims-org.png)

Outre les informations d’identification ci-dessus, vous aurez également besoin de la **[!UICONTROL clé secrète client]** générée pour une étape ultérieure. Sélectionnez **[!UICONTROL Récupérer le secret client]** pour révéler la valeur, puis copiez-la pour une utilisation ultérieure.

![](././images/api-authentication/client-secret.png)

## Générer un jeton Web JSON (JWT) {#jwt}

L’étape suivante consiste à générer un JSON Web Token (JWT) basé sur les informations d’identification de votre compte. Cette valeur est utilisée pour générer vos informations d’identification `{ACCESS_TOKEN}` à utiliser dans les appels d’API de plate-forme, qui doivent être régénérés toutes les 24 heures.

Sélectionnez **[!UICONTROL Compte de service (JWT)]** dans le volet de navigation de gauche, puis **[!UICONTROL Générer JWT]**.

![](././images/api-authentication/generate-jwt.png)

Dans la zone de texte fournie sous **[!UICONTROL Générer un JWT personnalisé]**, collez le contenu de la clé privée que vous avez générée précédemment lors de l’ajout de l’API de plateforme à votre compte de service. Sélectionnez ensuite **[!UICONTROL Générer un jeton]**.

![](././images/api-authentication/paste-key.png)

La page se met à jour pour afficher le fichier JWT généré, ainsi qu’un exemple de commande cURL qui vous permet de générer un jeton d&#39;accès. Pour les besoins de ce didacticiel, sélectionnez **[!UICONTROL Copier]** en regard de **[!UICONTROL JWT généré]** pour copier le jeton dans le Presse-papiers.

![](././images/api-authentication/copy-jwt.png)

## Générer un jeton d&#39;accès

Une fois que vous avez généré un JWT, vous pouvez l&#39;utiliser dans un appel d&#39;API pour générer votre `{ACCESS_TOKEN}`. Contrairement aux valeurs de `{API_KEY}` et `{IMS_ORG}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API de plateforme.

**Requête**

La requête suivante génère un nouveau `{ACCESS_TOKEN}` en fonction des informations d’identification fournies dans la charge utile. Ce point de terminaison accepte uniquement les données de formulaire en tant que charge utile. Par conséquent, il doit recevoir un en-tête `Content-Type` de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propriété | Description |
| --- | --- |
| `{API_KEY}` | `{API_KEY}` ([!UICONTROL ID client]) que vous avez récupéré au cours d’une [étape précédente](#api-ims-secret). |
| `{SECRET}` | Secret client que vous avez récupéré à l&#39;étape [précédente](#api-ims-secret). |
| `{JWT}` | JWT que vous avez généré dans une étape [précédente](#jwt). |

>[!NOTE]
>
>Vous pouvez utiliser la même clé d’API, le même secret client et JWT pour générer un nouveau jeton d&#39;accès pour chaque session. Vous pouvez ainsi automatiser la génération de jetons d&#39;accès dans vos applications.

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
| `token_type` | Type de jeton renvoyé. Pour les jetons d&#39;accès, cette valeur est toujours `bearer`. |
| `access_token` | Le `{ACCESS_TOKEN}` généré. Cette valeur, précédée du mot `Bearer`, est requise en tant qu&#39;en-tête `Authentication` pour tous les appels d&#39;API de plate-forme. |
| `expires_in` | Nombre de millisecondes restantes jusqu’à l’expiration du jeton d&#39;accès. Une fois cette valeur atteinte, un nouveau jeton d&#39;accès doit être généré pour continuer à utiliser les API de plateforme. |

## Tester les informations d’accès

Une fois que vous avez rassemblé les trois informations d’identification requises, vous pouvez effectuer l’appel d’API suivant. Cet appel liste toutes les classes [!DNL Experience Data Model] (XDM) standard disponibles pour votre entreprise.

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

## Utilisez Postman pour authentifier et tester les appels d&#39;API

[](https://www.postman.com/) Postmanis est un outil populaire qui permet aux développeurs d&#39;explorer et de tester les API RESTful. Cette [publication moyenne](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) décrit comment vous pouvez configurer Postman pour qu&#39;il exécute automatiquement l&#39;authentification JWT et l&#39;utilise pour consommer les API de plateforme.

## Étapes suivantes

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’identification d’accès pour les API de plateformes. Vous pouvez désormais suivre l&#39;exemple d&#39;appels d&#39;API fourni dans la [documentation](../landing/documentation/overview.md).

Outre les valeurs d&#39;authentification que vous avez rassemblées dans ce didacticiel, de nombreuses API de plateformes nécessitent également un `{SANDBOX_NAME}` valide pour être fourni en-tête. Pour plus d’informations, consultez la [présentation des environnements de test](../sandboxes/home.md).
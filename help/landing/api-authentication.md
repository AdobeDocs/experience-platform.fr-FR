---
solution: Experience Platform
title: Authentification et accès aux API Experience Platform
type: Tutorial
description: Ce document fournit un tutoriel détaillé pour accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels API Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 2fb0da385baeb96d5665ecc25bf353c7516ef9f7
workflow-type: tm+mt
source-wordcount: '2149'
ht-degree: 7%

---


# S’authentifier et accéder aux API Experience Platform

Ce document fournit un tutoriel détaillé permettant d’accéder à un compte de développeur Adobe Experience Platform afin d’effectuer des appels vers des API Experience Platform. À la fin de ce tutoriel, vous aurez généré ou collecté les informations d’identification suivantes, requises en tant qu’en-têtes dans tous les appels d’API Platform :

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>Outre les trois informations d’identification ci-dessus, de nombreuses API Platform nécessitent également qu’un `{SANDBOX_NAME}` valide soit fourni en tant qu’en-tête. Pour plus d’informations sur les environnements de test et la documentation [sandbox management endpoint](/help/sandboxes/api/sandboxes.md#list) pour plus d’informations sur la liste des environnements de test disponibles pour votre organisation, consultez la [présentation des environnements de test](../sandboxes/home.md) .

Pour maintenir la sécurité de vos applications et de vos utilisateurs, toutes les demandes aux API Experience Platform doivent être authentifiées et autorisées à l’aide de normes telles que OAuth.

Ce tutoriel explique comment rassembler les informations d’identification requises pour authentifier les appels API Platform, comme décrit dans l’organigramme ci-dessous. Vous pouvez rassembler la plupart des informations d’identification requises dans la configuration initiale unique. Le jeton d’accès doit toutefois être actualisé toutes les 24 heures.

![](./images/api-authentication/authentication-flowchart.png)

## Conditions préalables {#prerequisites}

Pour passer avec succès des appels à des API Experience Platform, vous devez disposer des éléments suivants :

* Une organisation ayant accès à Adobe Experience Platform.
* Administrateur Admin Console capable de vous ajouter en tant que développeur et utilisateur pour un profil de produit.
* Administrateur système Experience Platform qui peut vous accorder les contrôles d’accès basés sur les attributs nécessaires pour effectuer des opérations de lecture ou d’écriture sur différentes parties de l’Experience Platform via les API.

Vous devez également disposer d’un Adobe ID pour suivre ce tutoriel. Si vous ne possédez pas d’Adobe ID, vous pouvez en créer un en suivant les étapes suivantes :

1. Accédez à [Adobe Developer Console](https://console.adobe.io).
2. Sélectionnez **[!UICONTROL Créer un compte]**.
3. Terminez le processus d’inscription.

## Obtenir un accès développeur et utilisateur pour les Experience Platform {#gain-developer-user-access}

Avant de créer des intégrations sur Adobe Developer Console, votre compte doit disposer des autorisations de développeur et d’utilisateur pour un profil de produit Experience Platform dans Adobe Admin Console.

### Obtenir un accès en tant que développeur {#gain-developer-access}

Contactez un administrateur [!DNL Admin Console] de votre entreprise pour vous ajouter en tant que développeur à un profil de produit Experience Platform à l’aide de [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consultez la documentation [!DNL Admin Console] pour obtenir des instructions spécifiques sur la [gestion de l’accès des développeurs pour les profils de produits](https://helpx.adobe.com/fr/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Une fois que vous avez été affecté en tant que développeur, vous pouvez commencer à créer des intégrations dans [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Ces intégrations constituent un pipeline allant des applications et services externes vers les API d’Adobe.

### Obtenir un accès utilisateur {#gain-user-access}

Votre administrateur [!DNL Admin Console] doit également vous ajouter en tant qu’utilisateur au même profil de produit. Avec l’accès utilisateur, vous pouvez voir dans l’interface utilisateur le résultat des opérations de l’API que vous effectuez.

Pour plus d’informations, consultez le guide sur la [gestion des groupes d’utilisateurs dans [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) .

## Génération d’une clé API (ID client) et d’un ID d’organisation {#generate-credentials}

>[!NOTE]
>
>Si vous suivez ce document à partir du [guide de l’API du Privacy Service](../privacy-service/api/getting-started.md), vous pouvez maintenant revenir à ce guide pour générer les informations d’identification d’accès uniques à [!DNL Privacy Service].

Une fois que vous avez reçu un accès utilisateur et développeur à Platform via [!DNL Admin Console], l’étape suivante consiste à générer vos informations d’identification `{ORG_ID}` et `{API_KEY}` dans Adobe Developer Console. Ces informations d’identification ne doivent être générées qu’une seule fois et peuvent être réutilisées dans les futurs appels d’API Platform.

### Ajouter un Experience Platform à un projet {#add-platform-to-project}

Accédez à [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) et connectez-vous avec votre Adobe ID. Suivez ensuite les étapes décrites dans le tutoriel sur la [création dʼun projet vide](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) disponible dans la documentation dʼAdobe Developer Console.

Une fois que vous avez créé un projet, sélectionnez **[!UICONTROL Ajouter une API]** sur l’écran **[!UICONTROL Project Overview]** (Aperçu du projet).

>[!TIP]
>
>Si vous êtes configuré pour plusieurs organisations, utilisez le sélecteur d’organisations dans le coin supérieur droit de l’interface pour vous assurer que vous êtes dans l’organisation dont vous avez besoin.

![Écran Developer Console avec l&#39;option Ajouter une API mise en surbrillance.](./images/api-authentication/add-api.png)

L’écran **[!UICONTROL Ajouter une API]** s’affiche. Sélectionnez l’icône de produit pour Adobe Experience Platform, puis **[!UICONTROL API Experience Platform]** avant de sélectionner **[!UICONTROL Suivant]**.

![Sélectionnez l’API Experience Platform.](./images/api-authentication/platform-api.png)

>[!TIP]
>
>Sélectionnez l’option **[!UICONTROL Afficher la documentation]** pour naviguer dans une fenêtre de navigateur distincte vers la [ documentation de référence de l’API Experience Platform](https://developer.adobe.com/experience-platform-apis/).

### Sélectionnez le type d&#39;authentification [!UICONTROL OAuth Server-to-Server] {#select-oauth-server-to-server}

Sélectionnez ensuite le type d&#39;authentification [!UICONTROL OAuth Server-to-Server] pour générer des jetons d&#39;accès et accéder à l&#39;API Experience Platform.

>[!IMPORTANT]
>
>La méthode **[!UICONTROL OAuth Server-to-Server]** est la seule méthode de génération de jeton prise en charge à l’avenir. La méthode **[!UICONTROL Service Account (JWT)]** précédemment prise en charge est obsolète et ne peut pas être sélectionnée pour les nouvelles intégrations. Bien que les intégrations existantes utilisant la méthode d’authentification JWT continueront à fonctionner jusqu’au 1er janvier 2025, Adobe recommande vivement de migrer les intégrations existantes vers la nouvelle méthode [!UICONTROL OAuth Server-to-Server] avant cette date. Pour plus d’informations, reportez-vous à la section [!BADGE Obsolète]{type=negative}[Générer un jeton Web JSON (JWT)](#jwt).

![Sélectionnez la méthode d&#39;authentification OAuth serveur à serveur pour l&#39;API Experience Platform.](./images/api-authentication/oauth-authentication-method.png)

### Sélection des profils de produit pour votre intégration {#select-product-profiles}

Dans l’écran **[!UICONTROL Configurer l’API]**, sélectionnez **[!UICONTROL AEP-Default-All-Users]**.

<!--
Your integration's service account will gain access to granular features through the product profiles selected here.

-->

>[!IMPORTANT]
>
Pour accéder à certaines fonctionnalités de Platform, vous avez également besoin d’un administrateur système pour vous accorder les autorisations de contrôle d’accès basées sur les attributs nécessaires. Pour en savoir plus, consultez la section [Obtention des autorisations de contrôle d’accès basées sur les attributs nécessaires](#get-abac-permissions).

![Sélectionnez les profils de produit pour votre intégration.](./images/api-authentication/select-product-profiles.png)

Sélectionnez **[!UICONTROL Enregistrer l’API configurée]** lorsque vous êtes prêt.

Une présentation des étapes décrites ci-dessus pour configurer une intégration avec l’API Experience Platform est également disponible dans le tutoriel vidéo ci-dessous :

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on)

### Collecte des informations d’identification {#gather-credentials}

Une fois que l’API a été ajoutée au projet, la page **[!UICONTROL API Experience Platform]** du projet affiche les informations d’identification suivantes requises dans tous les appels aux API Experience Platform :

![Informations sur l’intégration après l’ajout d’une API dans Developer Console.](./images/api-authentication/api-integration-information.png)

* `{API_KEY}` ([!UICONTROL ID client])
* `{ORG_ID}` ([!UICONTROL ID d’organisation])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## Générer un jeton d’accès {#generate-access-token}

L’étape suivante consiste à générer des informations d’identification `{ACCESS_TOKEN}` à utiliser dans les appels d’API Platform. Contrairement aux valeurs de `{API_KEY}` et `{ORG_ID}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API Platform. Sélectionnez **[!UICONTROL Générer un jeton d’accès]**, comme illustré ci-dessous.

![Afficher comment générer un jeton d’accès](././images/api-authentication/generate-access-token.gif)

>[!TIP]
>
Vous pouvez également utiliser un environnement et une collection Postman pour générer des jetons d’accès. Pour plus d’informations, consultez la section sur l’ [ utilisation de Postman pour authentifier et tester les appels API](#use-postman).

## [!BADGE Obsolète]{type=négatif} Générer un jeton Web JSON (JWT) {#jwt}

>[!WARNING]
>
La méthode JWT de génération des jetons d’accès a été abandonnée. Toutes les nouvelles intégrations doivent être créées à l’aide de la [méthode d’authentification OAuth de serveur à serveur](#select-oauth-server-to-server). Adobe exige également que vous migriez vos intégrations existantes vers la méthode OAuth d’ici le 1er janvier 2025 pour que vos intégrations continuent à fonctionner. Lisez la documentation importante suivante :
> 
* [Guide de migration de vos applications de JWT vers OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
* [Guide de mise en œuvre pour les nouvelles et les anciennes applications avec OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
* [Avantages de l’utilisation de la méthode d’identification OAuth serveur à serveur](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ Affichage des informations obsolètes

L’étape suivante consiste à générer un jeton Web JSON (JWT) basé sur les informations d’identification de votre compte. Cette valeur est utilisée pour générer vos informations d’identification `{ACCESS_TOKEN}` à utiliser dans les appels API Platform, qui doivent être régénérés toutes les 24 heures.

>[!IMPORTANT]
>
Pour les besoins de ce tutoriel, les étapes ci-dessous indiquent comment générer un jeton JWT dans Developer Console. Cependant, cette méthode de génération ne doit être utilisée qu’à des fins de test et d’évaluation.
>
Pour une utilisation régulière, le jeton JWT doit être généré automatiquement. Pour plus d’informations sur la génération par programmation de JWT, consultez le [guide d’authentification du compte de service](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) sur Adobe Developer.

Sélectionnez **[!UICONTROL Compte de service (JWT)]** dans le volet de navigation de gauche, puis **[!UICONTROL Générer JWT]**.

![](././images/api-authentication/generate-jwt.png)

Dans la zone de texte fournie sous **[!UICONTROL Generate custom JWT]**, collez le contenu de la clé privée que vous avez précédemment générée lors de l’ajout de l’API Platform à votre compte de service. Sélectionnez ensuite **[!UICONTROL Générer un jeton]**.

![](././images/api-authentication/paste-key.png)

La page se met à jour pour afficher le JWT généré, ainsi qu’un exemple de commande cURL qui vous permet de générer un jeton d’accès. Pour les besoins de ce tutoriel, sélectionnez **[!UICONTROL Copier]** en regard de **[!UICONTROL JWT généré]** pour copier le jeton dans votre presse-papiers.

![](././images/api-authentication/copy-jwt.png)

**Générer un jeton d’accès**

Une fois que vous avez généré un JWT, vous pouvez l’utiliser dans un appel API pour générer votre `{ACCESS_TOKEN}`. Contrairement aux valeurs de `{API_KEY}` et `{ORG_ID}`, un nouveau jeton doit être généré toutes les 24 heures pour continuer à utiliser les API Platform.

**Requête**

La requête suivante génère un nouveau `{ACCESS_TOKEN}` en fonction des informations d’identification fournies dans la payload. Ce point de terminaison accepte uniquement les données de formulaire comme charge utile. Il doit donc recevoir un en-tête `Content-Type` de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propriété | Description |
| --- | --- |
| `{API_KEY}` | `{API_KEY}` ([!UICONTROL ID client]) que vous avez récupéré dans une [étape précédente](#api-ims-secret). |
| `{SECRET}` | Le secret client que vous avez récupéré dans une [étape précédente](#api-ims-secret). |
| `{JWT}` | JWT que vous avez généré dans une [étape précédente](#jwt). |

>[!NOTE]
>
Vous pouvez utiliser la même clé API, le même secret client et JWT pour générer un nouveau jeton d’accès pour chaque session. Vous pouvez ainsi automatiser la génération des jetons d’accès dans vos applications.

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
| `token_type` | Le type of jeton en cours de renvoi. Pour les jetons d’accès, cette valeur est toujours `bearer`. |
| `access_token` | `{ACCESS_TOKEN}` généré. Cette valeur, précédée du mot `Bearer`, est requise en tant qu’en-tête `Authentication` pour tous les appels d’API Platform. |
| `expires_in` | Nombre de millisecondes restantes jusqu’à l’expiration du jeton d’accès. Une fois cette valeur atteinte, un nouveau jeton d’accès doit être généré pour continuer à utiliser les API Platform. |

+++

## Tester les informations d’accès {#test-credentials}

Une fois que vous avez rassemblé les trois informations d’identification requises - jeton d’accès, clé d’API et ID d’organisation - , vous pouvez effectuer l’appel API suivant. Cet appel répertorie toutes les classes [!DNL Experience Data Model] (XDM) standard disponibles pour votre organisation. Importez et exécutez l’appel dans [Postman](#use-postman).

>[!BEGINSHADEBOX]

**Requête**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
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

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
Bien que l’appel ci-dessus soit suffisant pour tester vos informations d’identification d’accès, sachez que vous ne pourrez pas accéder à plusieurs ressources ou les modifier sans disposer des autorisations appropriées de contrôle d’accès basées sur des attributs. Pour en savoir plus, consultez la section **Obtention des autorisations de contrôle d’accès basées sur les attributs nécessaires** ci-dessous.

## Obtention des autorisations de contrôle d’accès basées sur les attributs nécessaires {#get-abac-permissions}

Pour accéder à plusieurs ressources ou les modifier dans Experience Platform, vous devez disposer des autorisations de contrôle d’accès appropriées. Les administrateurs système peuvent vous accorder les [autorisations dont vous avez besoin](/help/access-control/ui/permissions.md). Pour plus d’informations, reportez-vous à la section sur la [gestion des informations d’identification de l’API pour un rôle](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role).

Des informations détaillées sur la manière dont un administrateur système peut accorder les autorisations requises pour accéder aux ressources Platform via l’API sont également disponibles dans le tutoriel vidéo ci-dessous :

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=159)

## Utilisation de Postman pour authentifier et tester les appels API {#use-postman}

[Postman](https://www.postman.com/) est un outil populaire qui permet aux développeurs d’explorer et de tester les API RESTful. Vous pouvez utiliser les collections et environnements Postman Experience Platform pour accélérer votre travail avec les API Experience Platform. En savoir plus sur [l’utilisation de Postman dans Experience Platform](/help/landing/postman.md) et la prise en main des collections et des environnements.

Des informations détaillées sur l’utilisation de Postman avec des collections et des environnements Experience Platform sont également disponibles dans les tutoriels vidéo ci-dessous :

**Télécharger et importer un environnement Postman à utiliser avec les API Experience Platform**

>[!VIDEO](https://video.tv.adobe.com/v/28832/?learn=on&t=106)

**Utiliser une collection Postman pour générer des jetons d’accès**

Téléchargez la [collection Postman Identity Management Service](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) et regardez la vidéo ci-dessous pour découvrir comment générer des jetons d’accès.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?learn=on)

**Télécharger des collections Postman d’API Experience Platform et interagir avec les API**

>[!VIDEO](https://video.tv.adobe.com/v/29704/?learn=on)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Platform APIs.
-->

## Administrateurs système : octroi aux développeurs et aux API d’un contrôle d’accès avec des autorisations d’Experience Platform {#grant-developer-and-api-access-control}

>[!NOTE]
>
Seuls les administrateurs système peuvent afficher et gérer les informations d’identification de l’API dans les autorisations.

Avant de créer des intégrations sur Adobe Developer Console, votre compte doit disposer des autorisations de développeur et d’utilisateur pour un profil de produit Experience Platform dans Adobe Admin Console.

### Ajout de développeurs à un profil de produit {#add-developers-to-product-profile}

Accédez à [[!DNL Admin Console]](https://adminconsole.adobe.com/) et connectez-vous avec votre Adobe ID.

Sélectionnez **[!UICONTROL Produits]**, puis **[!UICONTROL Adobe Experience Platform]** dans la liste des produits.

![Liste de produits sur Admin Console](././images/api-authentication/products.png)

Dans l’onglet **[!UICONTROL Profils de produit]**, sélectionnez **[!UICONTROL AEP-Default-All-Users]**. Vous pouvez également utiliser la barre de recherche pour rechercher le profil de produit en saisissant son nom.

![Recherchez le profil de produit](././images/api-authentication/select-product-profile.png)

Sélectionnez l’onglet **[!UICONTROL Développeurs]**, puis sélectionnez **[!UICONTROL Ajouter développeur]**.

![Ajouter un développeur à partir de l’onglet Développeurs](././images/api-authentication/add-developer1.png)

Saisissez le **[!UICONTROL Email ou nom d’utilisateur]** du développeur. Un [!UICONTROL email ou nom d’utilisateur] valide affiche les détails du développeur. Sélectionnez **[!UICONTROL Enregistrer]**.

![Ajoutez un développeur à l’aide de son email ou de son nom d’utilisateur](././images/api-authentication/add-developer-email.png)

Le développeur a été ajouté avec succès et apparaît sur l’onglet [!UICONTROL Développeurs] .

![Développeurs répertoriés dans l’onglet Développeurs](././images/api-authentication/developer-added.png)

<!--

Commenting out this part since it duplicates information from the section Add Experience Platform to a project

### Set up an API

A developer can add and configure an API within a project in the Adobe Developer Console.

Select your project, then select **[!UICONTROL Add API]**.

![Add API to a project](././images/api-authentication/add-api-project.png)

In the **[!UICONTROL Add an API]** dialog box select **[!UICONTROL Adobe Experience Platform]**, then select **[!UICONTROL Experience Platform API]**.

![Add an API in Experience Platform](././images/api-authentication/add-api-platform.png)

In the **[!UICONTROL Configure API]** screen, select **[!UICONTROL AEP-Default-All-Users]**.

-->

### Attribution d’une API à un rôle

Un administrateur système peut affecter des API aux rôles dans l’interface utilisateur de l’Experience Platform.

Sélectionnez **[!UICONTROL Permissions]** et le rôle auquel vous souhaitez ajouter l’API. Sélectionnez l’onglet **[!UICONTROL Informations d’identification de l’API]**, puis sélectionnez **[!UICONTROL Ajouter les informations d’identification de l’API]**.

![Onglet Informations d’identification de l’API dans le rôle sélectionné](././images/api-authentication/api-credentials.png)

Sélectionnez l’API que vous souhaitez ajouter au rôle, puis sélectionnez **[!UICONTROL Enregistrer]**.

![Liste des API disponibles pour la sélection](././images/api-authentication/select-api.png)

Vous revenez à l’onglet [!UICONTROL Informations d’identification de l’API], où l’API nouvellement ajoutée est répertoriée.

![ Onglet des informations d’identification de l’API avec l’API nouvellement ajoutée](././images/api-authentication/api-credentials-with-added-api.png)

## Ressources supplémentaires {#additional-resources}

Reportez-vous aux ressources supplémentaires liées ci-dessous pour plus d’informations sur la prise en main des API Experience Platform.

* Page de tutoriels vidéo [Authentification et accès aux API Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=fr)
* [Identity Management Service Postman Collection](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) pour générer des jetons d’accès
* [Collections Postman de l’API Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## Étapes suivantes {#next-steps}

En lisant ce document, vous avez rassemblé et testé avec succès vos informations d’identification d’accès pour les API Platform. Vous pouvez désormais suivre les exemples d’appels API fournis dans la [documentation](../landing/documentation/overview.md).

Outre les valeurs d’authentification que vous avez collectées dans ce tutoriel, de nombreuses API Platform nécessitent également qu’un `{SANDBOX_NAME}` valide soit fourni en tant qu’en-tête. Pour plus d’informations, consultez la [Présentation des sandbox](../sandboxes/home.md).
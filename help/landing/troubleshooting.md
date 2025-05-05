---
keywords: Experience Platform;accueil;rubriques populaires;codes d’erreur API;code d’erreur API;API code d’erreur;API codes d’erreur;erreur de requête API;dépannage API;erreur API
solution: Experience Platform
title: FAQ et guide de dépannage d’Adobe Experience Platform
description: Trouvez des réponses aux questions fréquemment posées et obtenez un guide afin de résoudre les problèmes courants dans Adobe Experience Platform.
landing-page-description: Trouvez des réponses aux questions fréquemment posées et obtenez un guide afin de résoudre les problèmes courants dans Adobe Experience Platform.
short-description: Trouvez des réponses aux questions fréquemment posées et obtenez un guide afin de résoudre les problèmes courants dans Experience Platform.
type: Documentation
role: Developer
feature: API, Audiences, Data Ingestion, Datasets, Destinations, Privacy, Queries, Schemas, Sandboxes, Sources
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 93%

---

# [!DNL Experience Platform]Questions fréquentes et guide de dépannage

Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform, ainsi qu’un guide de dépannage détaillé pour les erreurs courantes qui peuvent se produire dans n’importe quelle API [!DNL Experience Platform]. Pour obtenir un guide de dépannage concernant un service [!DNL Experience Platform] en particulier, consultez le [répertoire de dépannage des services](#service-troubleshooting-directory) ci-dessous.

## FAQ {#faq}

Vous trouverez ci-dessous une liste de réponses aux questions les plus fréquemment posées à propos d’Adobe Experience Platform.

## Que sont les API [!DNL Experience Platform] ? {#what-are-experience-platform-apis}

[!DNL Experience Platform] propose plusieurs API RESTful qui utilisent des requêtes HTTP pour accéder aux ressources de [!DNL Experience Platform]. Ces API de service présentent chacune plusieurs points d’entrée et vous permettent d’effectuer des opérations ayant pour but de répertorier (GET), de rechercher (GET), de modifier (PUT et/ou PATCH) et de supprimer (DELETE) des ressources. Pour plus d’informations sur les points d’entrée spécifiques et sur les opérations disponibles pour chaque service, consultez la [documentation de référence sur l’API](https://www.adobe.com/go/platform-api-reference-en) sur Adobe I/O.

## Comment formater une requête API ?  {#how-do-i-format-an-api-request}

Les formats de requête varient selon l’API [!DNL Experience Platform] utilisée. Le meilleur moyen d’apprendre à structurer vos appels API est de suivre les exemples fournis dans la documentation du service [!DNL Experience Platform] que vous utilisez.

Pour plus d’informations sur le formatage des requêtes API, consultez la section du guide de prise en main de l’API Experience Platform [consultez des exemples d’appels API](./api-guide.md#sample-api).

## Quelle est mon organisation ? {#what-is-my-ims-organization}

Une organisation est une représentation de clientèle pour Adobe. Toutes les solutions Adobe sous licence sont intégrées à cette organisation cliente. Lorsqu’une organisation est autorisée à utiliser [!DNL Experience Platform], elle peut attribuer un accès aux développeurs et développeuses. L’identifiant d’organisation (`x-gw-ims-org-id`) représente l’organisation pour laquelle un appel API devrait être exécuté. Il est donc nécessaire de le placer en tant qu’en-tête de toutes les requêtes API. Cet ID est accessible via [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) : dans l’onglet **Intégrations**, accédez à la section **Vue d’ensemble** pour toute intégration spécifique afin de trouver l’ID sous **Informations d’identification client**. Pour une présentation détaillée de la procédure d’authentification dans [!DNL Experience Platform], consultez le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

## Où trouver ma clé API ?  {#where-can-i-find-my-api-key}

Une clé API doit constituer l’en-tête de toutes les requêtes API. Il est accessible via [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Dans la console, sous l’onglet **Intégrations**, accédez à la section **Présentation** pour une intégration spécifique et vous trouverez la clé sous **Informations d’identification client**. Pour une présentation détaillée de la procédure d’authentification dans [!DNL Experience Platform], consultez le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

## Comment obtenir un jeton d’accès ?  {#how-do-i-get-an-access-token}

Les jetons d’accès doivent être renseignés dans l’en-tête d’autorisation de tous les appels API. Ils peuvent être générés à l’aide d’une commande CURL, à condition que vous ayez accès à une intégration pour une organisation. Les jetons d’accès ne sont valides que pendant 24 heures. Après ce délai, un nouveau jeton doit être généré pour continuer à utiliser l’API. Pour plus d’informations sur la génération des jetons d’accès, consultez le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr).

## Comment utiliser les paramètres de requête ?  {#how-do-i-user-query-parameters}

Certains points d’entrée de l’API [!DNL Experience Platform] acceptent des paramètres de requête visant à localiser des informations spécifiques et filtrer les résultats renvoyés dans la réponse. Les paramètres de requête sont ajoutés aux chemins de requête avec un point d’interrogation (`?`), suivi d’un ou plusieurs paramètres de requête sous le format `paramName=paramValue`. Lorsque vous combinez plusieurs paramètres dans un seul appel, vous devez utiliser une esperluette (`&`) pour les séparer. L’exemple suivant illustre la manière dont une requête qui utilise plusieurs paramètres de requête est représentée dans la documentation.

Voici quelques exemples de paramètres de requête fréquemment utilisés :

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Pour savoir précisément quels paramètres de requête sont disponibles pour un service ou un point d’entrée en particulier, consultez la documentation spécifique au service.

## Comment indiquer un champ JSON à mettre à jour dans une requête PATCH ?  {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

De nombreuses opérations PATCH dans les API [!DNL Experience Platform] utilisent des chaînes [JSON Pointer](https://tools.ietf.org/html/rfc6901) pour indiquer les propriétés JSON à mettre à jour. Elles sont généralement incluses dans les payloads des requêtes au format [JSON Patch](https://tools.ietf.org/html/rfc6902). Pour plus d’informations sur la syntaxe requise pour ces technologies, consultez le [guide de base de l’API](api-fundamentals.md).

## Puis-je utiliser Postman pour appeler les API [!DNL Experience Platform] ? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) est un outil utile pour visualiser les appels vers les API RESTful. Le Guide de prise en main de l’API Experience Platform [&#128279;](api-guide.md) contient une vidéo et des instructions pour l’importation de collections Postman. En outre, une liste des collections Postman pour chaque service est fournie.

## Quelle est la configuration requise pour [!DNL Experience Platform] ? {#what-are-the-system-requirements-for-platform}

Selon que vous utilisez l’interface utilisateur ou l’API, la configuration requise suivante s’applique :

**Pour les opérations basées sur l’interface utilisateur :**
- Un navigateur web standard et moderne. Bien que la dernière version de [!DNL Chrome] soit recommandée, les versions majeures actuelles et antérieures de [!DNL Firefox], [!DNL Internet Explorer], et Safari sont également prises en charge.
   - Dès qu’une nouvelle version majeure est disponible, [!DNL Experience Platform] commence à prendre en charge la version la plus récente, tandis que la prise en charge de la troisième version est abandonnée.
- Les cookies et JavaScript doivent être activés pour tous les navigateurs.

**Pour les interactions entre les développeurs et l’API :**
- Un environnement de développement à faire évoluer pour les intégrations de REST, de flux continu et de webhook.

## Erreurs et résolution des problèmes {#errors-and-troubleshooting}

Voici une liste des erreurs que vous pouvez rencontrer lorsque vous utilisez un service [!DNL Experience Platform]. Pour obtenir un guide de dépannage concernant un service [!DNL Experience Platform] spécifique, consultez le [répertoire de dépannage des services](#service-troubleshooting-directory) ci-dessous.

## Codes d’état API {#api-status-codes}

Vous pouvez rencontrer les codes d’état suivants sur n’importe quelle API [!DNL Experience Platform]. Chacun d’entre eux pouvant être causé par un grand nombre d’éléments, les explications données dans cette section sont générales. Pour plus d’informations sur les erreurs relatives à un service [!DNL Experience Platform] spécifique, consultez le [répertoire de dépannage des services](#service-troubleshooting-directory) ci-dessous.

| Code d’état | Description | Causes possibles |
|--- | --- | ---|
| 400 | Mauvaise requête | La requête a été mal construite, des informations de clé étaient absentes et/ou sa syntaxe était incorrecte. |
| 401 | Échec de l’authentification | La requête n’a pas pu être authentifiée. Votre jeton d’accès est peut-être absent ou non valide. Pour plus d’informations, reportez-vous à la section [erreurs de jeton OAuth](#oauth-token-is-missing) ci-dessous. |
| 403 | Interdit | La ressource a été trouvée, mais vous ne possédez pas les informations d’identification appropriées pour la consulter. <br>Une cause probable de cette erreur est que vous ne disposez pas des [autorisations de contrôle d’accès](/help/access-control/home.md) permettant d’accéder à la ressource ou de la modifier. Lisez comment [obtenir les autorisations de contrôle d’accès basé sur les attributs nécessaires](/help/landing/api-authentication.md#get-abac-permissions) pour utiliser les API d’Experience Platform. </p> |
| 404 | Introuvable | La ressource demandée n’a pas été trouvée sur le serveur. La ressource a peut-être été supprimée, ou le chemin d’accès demandé n’a pas été correctement saisi. |
| 500 | Erreur interne du serveur | Il s’agit d’une erreur côté serveur. Si vous effectuez de nombreux appels simultanés, vous pouvez atteindre la limite de l’API et devoir filtrer vos résultats. (Pour en savoir plus, consultez la sous-partie du guide de développement de l’API [!DNL Catalog Service] sur le [filtrage des données](../catalog/api/filter-data.md).) Patientez avant de réessayer d’exécuter votre requête et contactez votre administrateur si le problème persiste. |

## Erreurs dans l’en-tête de la requête {#request-header-errors}

Tous les appels API dans [!DNL Experience Platform] nécessitent des en-têtes de requête spécifiques. Pour connaître les en-têtes nécessaires pour un service en particulier, consultez la [documentation de référence sur l’API](https://www.adobe.com/go/platform-api-reference-en). Pour rechercher les valeurs des en-têtes d’authentification requis, consultez le [tutoriel sur l’authentification](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr). Si l’un de ces en-têtes est absent ou non valide lors d’un appel API, les erreurs suivantes peuvent se produire.

### Jeton OAuth absent {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête `Authorization` est absent d’une requête API. Assurez-vous que l’en-tête d’autorisation comprend un jeton d’accès valide avant de réessayer.

### Jeton OAuth non valide {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Ce message d’erreur s’affiche lorsque le jeton d’accès indiqué dans l’en-tête `Authorization` n’est pas valide. Assurez-vous que le jeton a été saisi correctement ou [générez un nouveau jeton](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=fr) dans la console Adobe I/O.

### Clé API requise {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête de clé API (`x-api-key`) est absent d’une requête API. Assurez-vous que l’en-tête comprend une clé API valide avant de réessayer.

### Clé API non valide {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Ce message d’erreur s’affiche lorsque la valeur de l’en-tête de clé API indiqué (`x-api-key`) n’est pas valide. Vérifiez que vous avez correctement saisi la clé avant de réessayer. Si vous ne connaissez pas votre clé API, vous pouvez la trouver dans la [console Adobe I/O](https://console.adobe.io) : dans l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique afin de trouver la clé API sous **Informations d’identification du client**.

### En-tête absent {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête d’organisation (`x-gw-ims-org-id`) est absent d’une requête API. Assurez-vous que l’en-tête comprend l’identifiant de votre organisation avant de réessayer.

### Profil non valide {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Ce message d’erreur s’affiche lorsque l’intégration de l’utilisateur ou de l’utilisatrice ou d’Adobe I/O (identifiée par le [jeton d’accès](#how-do-i-get-an-access-token) dans l’en-tête `Authorization`) n’est pas autorisée à effectuer des appels vers les API [!DNL Experience Platform] pour l’organisation indiquée dans l’en-tête `x-gw-ims-org-id`. Vérifiez que vous avez indiqué le bon identifiant pour votre organisation dans l’en-tête avant de réessayer. Si vous ne connaissez pas l’identifiant de votre organisation, vous pouvez le trouver dans la [Console Adobe I/O](https://console.adobe.io) : dans l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique afin de trouver l’identifiant sous **Informations d’identification du client**.

### Erreur d’actualisation de l’etag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

Vous pouvez recevoir une erreur d’etag si une modification a été apportée à une entité source ou une entité de destination comme un flux, une connexion, un connecteur source ou une connexion cible par un autre appelant de l’API. En raison de l’incohérence de la version, la modification que vous essayez d’apporter ne sera pas appliquée à la dernière version de l’entité.

Pour résoudre ce problème, vous devez récupérer à nouveau l’entité, vous assurer que vos modifications sont compatibles avec la nouvelle version de l’entité, puis placer le nouvel etag dans l’en-tête `If-Match` et effectuez l’appel API.

### Type de contenu valide non spécifié {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Ce message d’erreur s’affiche lorsqu’une requête POST, PUT ou PATCH comporte un en-tête `Content-Type` non valide ou n’en comporte pas. Assurez-vous que l’en-tête est inclus dans la requête et que sa valeur est bien `application/json`.

### La région de l’utilisateur est manquante {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Ce message d’erreur s’affiche dans l’un des deux cas ci-dessous :
- Lorsqu’un en-tête d’organisation incorrect ou malformé (`x-gw-ims-org-id`) est transmis dans une requête API. Assurez-vous que l’identifiant correct de votre organisation est inclus avant de réessayer.
- Lorsque votre compte (tel que représenté par les informations d’authentification fournies) n’est pas associé à un profil de produit pour Experience Platform. Suivez les étapes de la [génération des informations d’accès](./api-authentication.md#authentication-for-each-session) dans le tutoriel sur l’authentification de l’API Experience Platform pour ajouter Experience Platform à votre compte et mettre à jour vos informations d’authentification en conséquence.

## Répertoire de dépannage des services {#service-troubleshooting-directory}

Voici une liste de guides de dépannage et de documentation de référence sur les API pour les API [!DNL Experience Platform]. Chaque guide de dépannage fournit des réponses aux questions les plus fréquemment posées ainsi que des solutions aux problèmes relatifs à un service [!DNL Experience Platform] spécifique. Les documents de référence sur l’API fournissent un guide complet de tous les points d’entrée disponibles pour chaque service et présentent des échantillons de corps de requête, de réponses et de codes d’erreur que vous pouvez recevoir.

| Service | Référence d’API | Dépannage |
| --- | --- | --- |
| Contrôle d’accès | [API Access Control](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Guide de dépannage du contrôle d’accès](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform Data Ingestion | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [Guide de dépannage de l’ingestion par lots](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Ingestion | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [Guide de dépannage de l’ingestion en flux continu](../ingestion/streaming-ingestion/troubleshooting.md) |
| Espace de travail de science des données d’Adobe Experience Platform | [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) | Guide de dépannage du [[!DNL Data Science Workspace] ](../data-science-workspace/troubleshooting-guide.md) |
| Gouvernance des données d’Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Service d’identités d’Adobe Experience Platform | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | Guide de dépannage du [[!DNL Identity Service] ](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | Guide de dépannage du [[!DNL Query Service] ](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform Segmentation | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Questions fréquentes et guide de dépannage](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] et [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | Guide de dépannage du [[!DNL Profile] ](../profile/troubleshooting.md) |
| Sandbox | [API Sandbox](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Guide de dépannage des sandbox](../sandboxes/troubleshooting-guide.md) |

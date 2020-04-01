---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: FAQ et Guide de dépannage d’Adobe Experience Platform
topic: getting started
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# FAQ sur la plateforme et guide de dépannage

Ce fournit des réponses aux questions fréquentes sur Adobe Experience Platform, ainsi qu’un guide de dépannage de haut niveau pour les erreurs courantes qui peuvent se produire dans toute API de plateforme d’expérience. Pour obtenir des guides de dépannage sur les services de plateforme individuels, consultez le répertoire [de dépannage des](#service-troubleshooting-directory) services ci-dessous.

## FAQ {#faq}

Vous trouverez ci-dessous un  de réponses aux questions fréquentes sur Adobe Experience Platform.

## Que sont les API de plateforme d’expérience ? {#what-are-experience-platform-apis}

 de la plateforme d’expérience  plusieurs API RESTful qui utilisent des requêtes HTTP pour accéder aux ressources de la plateforme. Ces API de service exposent chacun plusieurs points de fin et vous permettent d’effectuer des opérations sur des ressources de (GET), de recherche (GET), de modification (PUT et/ou PATCH) et de suppression (DELETE). Pour plus d’informations sur les points de fin et les opérations spécifiques disponibles pour chaque service, consultez la documentation [de référence sur les](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) API sur les E/S Adobe.

## Comment formater une demande d’API ? {#how-do-i-format-an-api-request}

Les formats de requête varient selon l’API de plateforme utilisée. Le meilleur moyen d’apprendre à structurer vos appels d’API est de suivre les exemples fournis dans la documentation du service de plateforme que vous utilisez.

### Lecture d’exemples d’appels d’API

La documentation de la plateforme d’expérience présente des exemples d’appels d’API de deux manières différentes. Tout d’abord, l’appel est présenté dans son format **** API, une représentation de modèle montrant uniquement l’opération (GET, POST, PUT, PATCH, DELETE) et le point de fin utilisé (par exemple `/global/classes`). Certains modèles indiquent également l’emplacement des variables pour illustrer la manière dont un appel doit être formulé, comme `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Les appels sont ensuite affichés sous forme de commandes cURL dans une **requête**, qui comprend les en-têtes nécessaires et le chemin de base complet nécessaire pour interagir avec l’API. Le chemin de base doit être prédéfini sur tous les points de fin. Par exemple, le `/global/classes` point de terminaison susmentionné devient `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Le format de l’API/modèle de requête est visible dans toute la documentation et vous devez utiliser le chemin d’accès complet illustré dans l’exemple de demande lors de vos propres appels aux API de plateforme.

### Exemple de demande d’API

Voici un exemple de requête d’API qui illustre le format que vous allez rencontrer dans la documentation.

**Format API**

Le format API affiche l’opération (GET) et le point de fin utilisé. Les variables sont indiquées par des accolades (dans ce cas, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Requête**

Dans cet exemple de requête, les variables du format API reçoivent des valeurs réelles dans le chemin de requête. Tous les en-têtes requis sont également affichés, sous la forme d’exemples de valeurs d’en-tête ou de variables dans lesquels des informations sensibles (telles que des jetons de sécurité et des ID d’accès) doivent être incluses.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Réponse**

La réponse illustre ce que vous prévoyez de recevoir après un appel réussi à l’API, en fonction de la demande qui a été envoyée. Parfois, la réponse est tronquée pour l’espace, ce qui signifie que vous pouvez voir plus d’informations ou d’informations supplémentaires à celles qui sont affichées dans l’exemple.

```json
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
    ],
    "_links": {}
}
```

Pour plus d’informations sur des points de fin spécifiques dans les API de plateformes, y compris les en-têtes et les corps de requêtes requis, consultez la documentation [de référence des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API.

## Quelle est mon organisation IMS ? {#what-is-my-ims-organization}

Une organisation IMS est une représentation Adobe d’un client. Toutes les solutions Adobe sous licence sont intégrées à cette société cliente. Lorsqu’une organisation IMS est autorisée à utiliser Experience Platform, elle peut attribuer un accès aux développeurs. L’ID d’organisation IMS (`x-gw-ims-org-id`) représente l’organisation pour laquelle un appel d’API doit être exécuté. Il est donc requis comme en-tête dans toutes les demandes d’API. Cet ID est accessible via la console [d’E/S](https://console.adobe.io/)Adobe : dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration particulière afin de trouver l’ID sous Informations d’identification **du** client. Pour une présentation détaillée de la procédure d’authentification dans Platform, consultez le didacticiel [sur l’](../tutorials/authentication.md)authentification.

## Où puis-je trouver ma clé API ? {#where-can-i-find-my-api-key}

Une clé d’API est requise en tant qu’en-tête dans toutes les requêtes d’API. Il est accessible via la console [d’E/S](https://console.adobe.io/)Adobe. Dans la console, dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration spécifique et vous trouverez la clé sous Informations d’identification **** client. Pour une présentation détaillée de la procédure d’authentification sur la plateforme, consultez le didacticiel [sur l’](../tutorials/authentication.md)authentification.

## Comment puis-je obtenir un  ? {#how-do-i-get-an-access-token}

Les  sont obligatoires dans l’en-tête d’autorisation de tous les appels d’API. Ils peuvent être générés à l’aide d’une `curl` commande, à condition que vous ayez accès à une intégration pour une organisation IMS. Les  de ne sont valides que pendant 24 heures, après quoi un nouveau jeton doit être généré pour continuer à utiliser l’API. Pour plus d’informations sur la génération de  de, consultez le didacticiel [sur l’](../tutorials/authentication.md)authentification.

## Comment utiliser les paramètres  ? {#how-do-i-user-query-parameters}

Certains points de fin d’API de plateforme acceptent des paramètres  pour localiser des informations spécifiques et filtrer les résultats renvoyés dans la réponse. Les paramètres de  sont ajoutés pour demander des chemins avec un point d’interrogation (`?`), suivi d’un ou plusieurs paramètres  de utilisant le format `paramName=paramValue`. Lorsque vous combinez plusieurs paramètres dans un appel unique, vous devez utiliser une esperluette (`&`) pour séparer des paramètres individuels. L’exemple suivant montre comment une requête qui utilise plusieurs paramètres de est représentée dans la documentation.

Voici quelques exemples de paramètres  fréquemment utilisés :

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Pour obtenir des informations détaillées sur les paramètres  du disponibles pour un service ou un point de fin spécifique, consultez la documentation spécifique du service.

## Comment indiquer un champ JSON à mettre à jour dans une requête PATCH ? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

De nombreuses opérations PATCH dans les API de plateforme utilisent des chaînes de pointeur [](https://tools.ietf.org/html/rfc6901) JSON pour indiquer les propriétés JSON à mettre à jour. Elles sont généralement incluses dans les charges de requête au format de correctif [](https://tools.ietf.org/html/rfc6902) JSON. Pour plus d’informations sur la syntaxe requise pour ces technologies, consultez le guide [de base des](api-fundamentals.md) API.

## Puis-je utiliser Postman pour appeler les API de plateformes ? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) est un outil utile pour visualiser les appels aux API RESTful. Cette publication [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) moyenne décrit comment configurer Postman pour qu’il effectue automatiquement l’authentification et l’utilise pour consommer les API de plateforme d’expérience.

## Quelle est la configuration requise pour Platform ? {#what-are-the-system-requirements-for-platform}

Selon que vous utilisez l’interface utilisateur ou l’API, la configuration requise suivante s’applique :

**Pour les opérations basées sur l’interface utilisateur :**
- Un navigateur Web moderne et standard. Bien que la dernière version de Chrome soit recommandée, les versions majeures actuelle et précédente de Firefox, d’Internet Explorer et de Safari sont également prises en charge.
   - Chaque fois qu’une nouvelle version majeure est publiée, le de plateformes prend en charge la version la plus récente et la troisième version la plus récente est supprimée.
- Les cookies et JavaScript doivent être activés pour tous les navigateurs.

**Pour les interactions API et développeurs :**
- Un de développement  à développer pour les intégrations REST, streaming et Webhook.

## Erreurs et dépannage {#errors-and-troubleshooting}

Voici un  d’erreurs que vous pouvez rencontrer lors de l’utilisation d’un service de plateforme d’expérience. Pour obtenir des guides de dépannage sur les services de plateforme individuels, consultez le répertoire [de dépannage des](#service-troubleshooting-directory) services ci-dessous.

## Codes d’état d’API {#api-status-codes}

Les codes d’état suivants peuvent être trouvés sur toute API de plateforme d’expérience. Chacun a une variété de causes, donc les explications données dans cette section sont de nature générale. Pour plus d’informations sur les erreurs spécifiques dans les services de plateforme individuels, consultez le répertoire [de dépannage des](#service-troubleshooting-directory) services ci-dessous.

| Code d’état | Description | Causes possibles |
--- | --- | ---
| 400 | Requête incorrecte | La requête a été mal construite, les informations de clé manquantes et/ou contenait une syntaxe incorrecte. |
| 401 | Échec de l&#39;authentification | La requête n’a pas réussi une vérification d’authentification. Votre est peut-être manquant ou non valide. Pour plus d’informations, voir la section Erreurs [de jeton](#oauth-token-is-missing) OAuth ci-dessous. |
| 403 | Interdit | La ressource a été trouvée, mais vous n’avez pas les informations d’identification appropriées pour la . |
| 404 | Introuvable | La ressource demandée est introuvable sur le serveur. La ressource a peut-être été supprimée ou le chemin d&#39;accès demandé a été entré incorrectement. |
| 500 | Erreur du serveur interne | Il s’agit d’une erreur côté serveur. Si vous effectuez de nombreux appels simultanés, vous pouvez atteindre la limite de l’API et vous devez filtrer vos résultats. (Pour en savoir plus, consultez le sous-guide du développeur de l’API du service de catalogue sur le [filtrage des données](../catalog/api/filter-data.md) .) Patientez quelques instants avant de réessayer votre requête et contactez votre administrateur si le problème persiste. |

## Erreurs d’en-tête de demande {#request-header-errors}

Tous les appels d’API dans la plateforme nécessitent des en-têtes de requête spécifiques. Pour connaître les en-têtes requis pour les services individuels, consultez la documentation [de référence sur les](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API. Pour rechercher les valeurs des en-têtes d’authentification requis, consultez le didacticiel [sur l’](../tutorials/authentication.md)authentification. Si l’un de ces en-têtes est manquant ou non valide lors d’un appel d’API, les erreurs suivantes peuvent se produire.

### Jeton OAuth manquant {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Ce message d’erreur s’affiche lorsqu’un `Authorization` en-tête est manquant dans une requête d’API. Assurez-vous que l’en-tête d’autorisation est inclus dans un  valide avant de réessayer.

### Jeton OAuth non valide

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Ce message d’erreur s’affiche lorsque le  fourni dans l’ `Authorization` en-tête n’est pas valide. Assurez-vous que le jeton a été saisi correctement ou [générez un nouveau jeton](../tutorials/authentication.md) dans la console d’E/S Adobe.

### La clé d&#39;API est requise

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête de clé d’API (`x-api-key`) est manquant dans une requête d’API. Assurez-vous que l’en-tête est inclus avec une clé d’API valide avant de réessayer.

### La clé d&#39;API n&#39;est pas valide

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Ce message d’erreur s’affiche lorsque la valeur de l’en-tête de clé d’API fourni (`x-api-key`) n’est pas valide. Vérifiez que vous avez saisi la clé correctement avant de réessayer. Si vous ne connaissez pas votre clé d’API, vous pouvez la trouver dans la console [d’E/S](https://console.adobe.io)Adobe : dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration spécifique afin de trouver la clé API sous Informations d’identification **du** client.


### En-tête manquant

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête d’organisation IMS (`x-gw-ims-org-id`) est absent d’une requête d’API. Assurez-vous que l’en-tête est inclus avec l’ID de votre organisation IMS avant de réessayer.

###  non valide

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Ce message d’erreur s’affiche lorsque l’utilisateur ou l’intégration d’E/S Adobe (identifiée par le [](#how-do-i-get-an-access-token) dans l’ `Authorization` en-tête) n’est pas autorisé à effectuer des appels aux API de plateforme d’expérience pour l’organisation IMS fournie dans l’ `x-gw-ims-org-id` en-tête. Vérifiez que vous avez fourni l’ID correct pour votre organisation IMS dans l’en-tête avant de réessayer. Si vous ne connaissez pas l’ID de votre organisation, vous pouvez le trouver dans la console [d’E/S](https://console.adobe.io)Adobe : dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration spécifique afin de trouver l’ID sous Informations d’identification **du** client.

### Type de contenu valide non spécifié

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Ce message d’erreur s’affiche lorsqu’une requête POST, PUT ou PATCH comporte un `Content-Type` en-tête non valide ou manquant. Assurez-vous que l’en-tête est inclus dans la requête et que sa valeur est `application/json`.


## Répertoire de dépannage du service {#service-troubleshooting-directory}

Voici un de guides de dépannage et de documentation de référence API pour les API de plateformes d’expérience. Chaque guide de dépannage fournit des réponses aux questions fréquentes et des solutions aux problèmes spécifiques aux services de plateforme individuels. Le de référence API fournit un guide complet de tous les points de fin disponibles pour chaque service et présente des exemples de corps de requête, de réponses et de codes d’erreur que vous pouvez recevoir.

| Service | Référence d’API | Résolution des problèmes |
--- | --- | ---
| Access Control | [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guide de dépannage des](../access-control/troubleshooting-guide.md) |
| Catalog (Catalogue) | [API du service de catalogue](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Ingestion des données (lot) | [API d&#39;insertion de données](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guide de dépannage d&#39;assimilation de lot](../ingestion/batch-ingestion/troubleshooting.md) |
| Ingestion des données (diffusion en continu) | [API d&#39;insertion de données](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guide de dépannage de l&#39;assimilation en flux continu](../ingestion/streaming-ingestion/troubleshooting.md) |
| Espace de travail Data Science | [API d’apprentissage automatique Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Guide de dépannage de Data Science Workspace](../data-science-workspace/troubleshooting-guide.md) |
| Étiquetage et application de l’utilisation des données (DULE) | [API du service de stratégie DUL](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Modèle de données d’expérience (XDM) | [API de registre des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [FAQ sur le système XDM et guide de dépannage](../xdm/troubleshooting-guide.md) |
| Identity Service | [API du service d’identité](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Guide de dépannage du service Identity Service](../identity-service/troubleshooting-guide.md) |
| Service  | [API du service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Guide de dépannage du service](../query-service/troubleshooting-guide.md) |
| Profil client en temps réel | [API de client en temps réel](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) |  |
| Environnements de test | [API Sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guide de dépannage des sandbox](../sandboxes/troubleshooting-guide.md) |
| Segmentation | [API de segmentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
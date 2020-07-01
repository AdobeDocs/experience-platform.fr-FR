---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: FAQ sur l'Adobe Experience Platform et Guide de dépannage
topic: getting started
translation-type: tm+mt
source-git-commit: 2e5668a8b1d5fb831188fbd4e453b9f4aa7474df
workflow-type: tm+mt
source-wordcount: '1959'
ht-degree: 3%

---


# [!DNL Platform] FAQ et guide de dépannage

Ce document fournit des réponses aux questions fréquentes sur l’Adobe Experience Platform, ainsi qu’un guide de dépannage de haut niveau pour les erreurs courantes susceptibles d’être rencontrées dans toute [!DNL Experience Platform] API. Pour obtenir des guides de dépannage sur [!DNL Platform] les services individuels, consultez le répertoire [de dépannage des](#service-troubleshooting-directory) services ci-dessous.

## FAQ {#faq}

Vous trouverez ci-dessous une liste de réponses aux questions fréquemment posées sur l&#39;Adobe Experience Platform.

## Que sont [!DNL Experience Platform] les API ? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre plusieurs API RESTful qui utilisent des requêtes HTTP pour accéder aux [!DNL Platform] ressources. Ces API de service exposent chacun plusieurs points de terminaison et vous permettent d’effectuer des opérations sur des ressources de liste (GET), de recherche (GET), de modification (PUT et/ou PATCH) et de suppression (DELETE). Pour plus d&#39;informations sur les points de terminaison et les opérations spécifiques disponibles pour chaque service, consultez la documentation [Référence](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) API sur les E/S Adobe.

## Comment formater une demande d’API ? {#how-do-i-format-an-api-request}

Les formats de requête varient en fonction de l’ [!DNL Platform] API utilisée. La meilleure façon de structurer vos appels d’API consiste à suivre les exemples fournis dans la documentation du service particulier que vous utilisez. [!DNL Platform]

### Exemples d’appels d’API lus

La documentation de [!DNL Experience Platform] montre des exemples d&#39;appels d&#39;API de deux manières différentes. Tout d’abord, l’appel est présenté dans son format **d’** API, une représentation de modèle montrant uniquement l’opération (GET, POST, PUT, PATCH, DELETE) et le point de terminaison utilisé (par exemple, `/global/classes`). Certains modèles indiquent également l’emplacement des variables pour illustrer comment un appel doit être formulé, par exemple `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

Les appels sont ensuite affichés sous forme de commandes cURL dans une **requête**, qui comprend les en-têtes nécessaires et le &quot;chemin de base&quot; complet nécessaires pour interagir avec l’API. Le chemin de base doit être préfixé à tous les points de terminaison. Par exemple, le `/global/classes` point de terminaison susmentionné devient `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. Le format de l’API / modèle de requête est visible dans toute la documentation et vous devez utiliser le chemin d’accès complet illustré dans l’exemple de demande lors de vos propres appels aux API Platform.

### Exemple de demande d’API

Voici un exemple de demande d’API qui illustre le format que vous allez rencontrer dans la documentation.

**Format d’API**

Le format d’API affiche l’opération (GET) et le point de terminaison utilisé. Les variables sont indiquées par des accolades (dans ce cas, `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Requête**

Dans cet exemple de requête, les variables du format API reçoivent des valeurs réelles dans le chemin de la requête. Tous les en-têtes requis sont également affichés, sous forme d’exemples de valeurs d’en-tête ou de variables dans lesquels des informations sensibles (telles que des jetons de sécurité et des ID d’accès) doivent être incluses.

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

La réponse illustre ce que vous prévoyez de recevoir après un appel réussi à l’API, en fonction de la demande qui a été envoyée. Parfois, la réponse est tronquée pour l’espace, ce qui signifie que vous pouvez voir plus d’informations ou d’informations supplémentaires sur celles qui sont affichées dans l’exemple.

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

Pour plus d’informations sur des points de terminaison spécifiques dans les API Platform, y compris les en-têtes et les corps de requêtes requis, consultez la documentation [de référence des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API.

## Quelle est mon organisation IMS ? {#what-is-my-ims-organization}

Une organisation IMS est une représentation Adobe d&#39;un client. Toutes les solutions Adobe sous licence sont intégrées à cette organisation cliente. Lorsqu&#39;une organisation IMS a le droit d&#39; [!DNL Experience Platform]accéder à, elle peut attribuer un accès aux développeurs. L’ID d’organisation IMS (`x-gw-ims-org-id`) représente l’organisation pour laquelle un appel d’API doit être exécuté et est donc requis comme en-tête dans toutes les demandes d’API. Cet identifiant est accessible via la Console [développeur](https://www.adobe.com/go/devs_console_ui_fr)Adobe : dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration particulière afin de trouver l’identifiant sous Informations d’identification **du** client. Pour une présentation détaillée de la procédure d’authentification [!DNL Platform], consultez le didacticiel [](../tutorials/authentication.md)d’authentification.

## Où puis-je trouver ma clé d&#39;API ? {#where-can-i-find-my-api-key}

Une clé d&#39;API est requise en tant qu&#39;en-tête dans toutes les requêtes d&#39;API. Il est accessible via la Console [développeur](https://www.adobe.com/go/devs_console_ui_fr)Adobe. Dans la console, dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration spécifique et vous trouverez la clé sous Informations d’identification **du** client. Pour une présentation détaillée de la procédure d’authentification, consultez le didacticiel [!DNL Platform][](../tutorials/authentication.md)d’authentification.

## Comment puis-je obtenir un jeton d&#39;accès ? {#how-do-i-get-an-access-token}

Les Jetons d&#39;accès sont requis dans l&#39;en-tête Autorisation de tous les appels d&#39;API. Ils peuvent être générés à l’aide d’une `curl` commande, à condition que vous ayez accès à une intégration pour une organisation IMS. Les Jetons d&#39;accès ne sont valides que pendant 24 heures, après quoi un nouveau jeton doit être généré pour continuer à utiliser l’API. Pour plus d&#39;informations sur la génération de jetons d&#39;accès, consultez le didacticiel [sur l&#39;](../tutorials/authentication.md)authentification.

## Comment utiliser les paramètres de requête ? {#how-do-i-user-query-parameters}

Certains points de terminaison [!DNL Platform] API acceptent des paramètres de requête pour localiser des informations spécifiques et filtrer les résultats renvoyés dans la réponse. Les paramètres de Requête sont ajoutés aux chemins de requête avec un point d’interrogation (`?`), suivi d’un ou plusieurs paramètres de requête utilisant le format `paramName=paramValue`. Lorsque vous combinez plusieurs paramètres dans un seul appel, vous devez utiliser une esperluette (`&`) pour séparer des paramètres individuels. L’exemple suivant montre comment une requête utilisant plusieurs paramètres de requête est représentée dans la documentation.

Voici quelques exemples de paramètres de requête couramment utilisés :

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Pour obtenir des informations détaillées sur les paramètres de requête disponibles pour un service ou un point de terminaison spécifique, consultez la documentation spécifique au service.

## Comment puis-je indiquer un champ JSON à mettre à jour dans une requête PATCH ? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

De nombreuses opérations PATCH dans [!DNL Platform] les API utilisent des chaînes de pointeur [](https://tools.ietf.org/html/rfc6901) JSON pour indiquer les propriétés JSON à mettre à jour. Elles sont généralement incluses dans les charges utiles de requête au format Patch [](https://tools.ietf.org/html/rfc6902) JSON. Pour obtenir des informations détaillées sur la syntaxe requise pour ces technologies, reportez-vous au guide [](api-fundamentals.md) API fundamentals guide.

## Puis-je utiliser Postman pour appeler des [!DNL Platform] API ? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) est un outil utile pour visualiser les appels aux API RESTful. Cette publication [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) moyenne décrit comment configurer Postman pour qu&#39;il effectue automatiquement l&#39;authentification et l&#39;utilise pour consommer [!DNL Experience Platform] des API.

## Quelle est la configuration requise pour [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Selon que vous utilisez l’interface utilisateur ou l’API, la configuration système requise suivante s’applique :

**Pour les opérations basées sur l’interface utilisateur :**
- Un navigateur Web moderne et standard. Bien que la dernière version de [!DNL Chrome] soit recommandée, les versions majeures actuelles et précédentes de [!DNL Firefox], [!DNL Internet Explorer]et Safari sont également prises en charge.
   - Chaque fois qu&#39;une nouvelle version majeure est publiée, [!DNL Platform] les débuts prenant en charge la version la plus récente sont ignorés, tandis que la prise en charge de la troisième version la plus récente est supprimée.
- Les cookies et JavaScript doivent être activés dans tous les navigateurs.

**Pour les interactions API et développeurs :**
- environnement de développement à développer pour les intégrations REST, streaming et Webhook.

## Erreurs et dépannage {#errors-and-troubleshooting}

Voici une liste d&#39;erreurs que vous pouvez rencontrer lors de l&#39;utilisation d&#39;un [!DNL Experience Platform] service. Pour obtenir des guides de dépannage sur [!DNL Platform] les services individuels, consultez le répertoire [de dépannage des](#service-troubleshooting-directory) services ci-dessous.

## Codes d’état d’API {#api-status-codes}

Les codes d&#39;état suivants peuvent être rencontrés sur toute [!DNL Experience Platform] API. Chacun a une variété de causes, donc les explications données dans cette section sont de nature générale. Pour plus d’informations sur les erreurs spécifiques dans les différents [!DNL Platform] services, consultez le répertoire [de dépannage des](#service-troubleshooting-directory) services ci-dessous.

| Code de statut | Description | Causes possibles |
--- | --- | ---
| 400 | Requête incorrecte | La requête a été mal construite, les informations de clé manquantes et/ou contenait une syntaxe incorrecte. |
| 401 | Échec de l&#39;authentification | La demande n&#39;a pas réussi une vérification d&#39;authentification. Votre jeton d&#39;accès est peut-être absent ou non valide. Pour plus d’informations, voir la section Erreurs [de jeton](#oauth-token-is-missing) OAuth ci-dessous. |
| 403 | Interdit | La ressource a été trouvée, mais vous ne disposez pas des informations d&#39;identification appropriées pour la vue. |
| 404 | Non trouvé | Impossible de trouver la ressource demandée sur le serveur. La ressource a peut-être été supprimée ou le chemin d&#39;accès demandé a été saisi incorrectement. |
| 500 | Erreur interne du serveur | Il s’agit d’une erreur côté serveur. Si vous effectuez de nombreux appels simultanés, il se peut que vous atteigniez la limite de l’API et que vous deviez filtrer vos résultats. (Voir le sous-guide du développeur [!DNL Catalog Service] d’API sur le [filtrage des données](../catalog/api/filter-data.md) pour en savoir plus.) Patientez quelques instants avant de réessayer votre requête et contactez votre administrateur si le problème persiste. |

## Erreurs d’en-tête de demande {#request-header-errors}

Tous les appels d&#39;API dans [!DNL Platform] nécessitent des en-têtes de requête spécifiques. Pour savoir quels en-têtes sont requis pour les services individuels, consultez la documentation [de référence des](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)API. Pour trouver les valeurs des en-têtes d’authentification requis, consultez le didacticiel [](../tutorials/authentication.md)Authentification. Si l&#39;un de ces en-têtes est absent ou non valide lors d&#39;un appel d&#39;API, les erreurs suivantes peuvent se produire.

### Jeton OAuth manquant {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Ce message d’erreur s’affiche lorsqu’un `Authorization` en-tête est absent d’une requête d’API. Assurez-vous que l’en-tête Autorisation est inclus avec un jeton d&#39;accès valide avant de réessayer.

### Jeton OAuth non valide

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Ce message d’erreur s’affiche lorsque le jeton d&#39;accès fourni dans l’ `Authorization` en-tête n’est pas valide. Assurez-vous que le jeton a été saisi correctement ou [générez un nouveau jeton](../tutorials/authentication.md) dans la console d&#39;E/S Adobe.

### La clé d&#39;API est requise

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête de clé d’API (`x-api-key`) est absent d’une requête d’API. Assurez-vous que l’en-tête est inclus avec une clé d’API valide avant de réessayer.

### La clé d&#39;API n&#39;est pas valide

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Ce message d’erreur s’affiche lorsque la valeur de l’en-tête de clé d’API fourni (`x-api-key`) n’est pas valide. Vérifiez que vous avez saisi la clé correctement avant de réessayer. Si vous ne connaissez pas votre clé d&#39;API, vous pouvez la trouver dans la console [d&#39;E/S](https://console.adobe.io)Adobe : dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration spécifique afin de trouver la clé d’API sous Informations d’identification **du** client.


### En-tête manquant

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête d’organisation IMS (`x-gw-ims-org-id`) est absent d’une requête d’API. Assurez-vous que l’en-tête est inclus avec l’ID de votre organisation IMS avant de réessayer.

### Profil non valide

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Ce message d’erreur s’affiche lorsque l’utilisateur ou l’intégration d’E/S Adobe (identifiée par le [jeton d&#39;accès](#how-do-i-get-an-access-token) dans l’ `Authorization` en-tête) n’est pas autorisé à invoquer [!DNL Experience Platform] les API pour l’organisation IMS fournie dans l’ `x-gw-ims-org-id` en-tête. Assurez-vous d’avoir fourni l’ID correct pour votre organisation IMS dans l’en-tête avant de réessayer. Si vous ne connaissez pas votre ID d’organisation, vous pouvez le trouver dans la console [d’E/S](https://console.adobe.io)Adobe : dans l’onglet **Intégrations** , accédez à la section **Aperçu** pour une intégration spécifique afin de trouver l’identifiant sous Informations d’identification **du** client.

### Type de contenu valide non spécifié

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Ce message d’erreur s’affiche lorsqu’une requête POST, PUT ou PATCH comporte un en-tête non valide ou manquant. `Content-Type` Assurez-vous que l’en-tête est inclus dans la requête et que sa valeur est `application/json`indiquée.


## Répertoire de dépannage du service {#service-troubleshooting-directory}

Vous trouverez ci-dessous une liste de guides de dépannage et de documentation de référence d’API pour [!DNL Experience Platform] les API. Chaque guide de dépannage fournit des réponses aux questions fréquentes et des solutions aux problèmes spécifiques à chaque [!DNL Platform] service. Les documents de référence d’API fournissent un guide complet de tous les points de terminaison disponibles pour chaque service et montrent des exemples de corps de requêtes, de réponses et de codes d’erreur que vous pouvez recevoir.

| Service | Référence d’API | Résolution des problèmes |
--- | --- | ---
| Contrôle d’accès | [API Contrôle d&#39;accès](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guide de dépannage des Contrôles d&#39;accès](../access-control/troubleshooting-guide.md) |
| Catalog (Catalogue) | [API du service de catalogue](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Ingestion des données (lot) | [API d&#39;importation de données](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guide de dépannage de l&#39;assimilation par lot](../ingestion/batch-ingestion/troubleshooting.md) |
| Ingestion des données (diffusion en continu) | [API d&#39;importation de données](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guide de dépannage de l&#39;assimilation en flux continu](../ingestion/streaming-ingestion/troubleshooting.md) |
| Espace de travail Data Science | [API d&#39;apprentissage automatique Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Guide de dépannage de Data Science Workspace](../data-science-workspace/troubleshooting-guide.md) |
| Étiquetage et application de l’utilisation des données (DULE) | [API DUL Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Modèle de données d’expérience (XDM) | [API de registre Schéma](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [FAQ sur XDM System et guide de dépannage](../xdm/troubleshooting-guide.md) |
| Identity Service | [API du service d&#39;identité](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Guide de dépannage d’Identity Service](../identity-service/troubleshooting-guide.md) |
| Requête Service | [API Requête Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Guide de dépannage de Requête Service](../query-service/troubleshooting-guide.md) |
| Profil client en temps réel | [API de Profil client en temps réel](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) |  |
| Environnements de test | [API Sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guide de dépannage des sandbox](../sandboxes/troubleshooting-guide.md) |
| Segmentation | [API de segmentation](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
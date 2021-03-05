---
keywords: Experience Platform ; accueil ; rubriques populaires ; codes d’erreur d’API ; code d’erreur d’API ; API de code d’erreur ; API de codes d’erreur ; erreur de demande d’API ; résolution des problèmes d’API ; erreur d’API
solution: Experience Platform
title: FAQ et guide de dépannage d’Adobe Experience Platform
description: Trouvez des réponses aux questions fréquemment posées et obtenez un guide afin de résoudre les problèmes courants dans Experience Platform.
landing-page-description: Trouvez des réponses aux questions fréquemment posées et obtenez un guide afin de résoudre les problèmes courants dans Experience Platform.
topic: démarrage
type: Documentation
translation-type: tm+mt
source-git-commit: 83cc3ddbf067f413cb524a3a685d985d5853eafd
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 68%

---


# [!DNL Platform] FAQ et guide de dépannage

Ce document fournit des réponses aux questions fréquentes sur Adobe Experience Platform, ainsi qu’un guide de dépannage de haut niveau pour les erreurs courantes qui peuvent se produire dans toute API [!DNL Experience Platform]. Pour obtenir des guides de dépannage sur les services [!DNL Platform] individuels, consultez le [répertoire de dépannage du service](#service-troubleshooting-directory) ci-dessous.

## FAQ {#faq}

Vous trouverez ci-dessous une liste de réponses aux questions les plus fréquemment posées à propos d’Adobe Experience Platform.

## Que sont les [!DNL Experience Platform] API ? {#what-are-experience-platform-apis}

[!DNL Experience Platform] offre plusieurs API RESTful qui utilisent des requêtes HTTP pour accéder aux  [!DNL Platform] ressources. Ces API de service présentent chacune plusieurs points de terminaison et vous permettent d’effectuer des opérations ayant pour but de répertorier (GET), de rechercher (GET), de modifier (PUT et/ou PATCH) et de supprimer (DELETE) des ressources. Pour plus d’informations sur les points de terminaison spécifiques et sur les opérations disponibles pour chaque service, consultez la [documentation de référence sur l’API](http://www.adobe.com/go/platform-api-reference-en) sur Adobe I/O.

## Comment formater une requête API ? {#how-do-i-format-an-api-request}

Les formats de requête varient en fonction de l’API [!DNL Platform] utilisée. La meilleure façon de structurer vos appels d&#39;API est de suivre les exemples fournis dans la documentation du service [!DNL Platform] particulier que vous utilisez.

Pour plus d&#39;informations sur le formatage des demandes d&#39;API, consultez le guide de prise en main de l&#39;API de plate-forme [lecture des exemples d&#39;appels d&#39;API](./api-guide.md#sample-api).

## Quelle est mon organisation IMS ? {#what-is-my-ims-organization}

Une organisation IMS est une représentation Adobe d’un client. Toutes les solutions Adobe sous licence intègrent cette organisation client. Lorsqu&#39;une organisation IMS est autorisée à [!DNL Experience Platform], elle peut attribuer un accès aux développeurs. L’identifiant d’organisation IMS (`x-gw-ims-org-id`) représente l’organisation pour laquelle un appel API devrait être exécuté. Il est donc nécessaire de le place en tant qu’en-tête de toutes les requêtes API. Cet identifiant est accessible via la [Console développeur d&#39;Adobes](https://www.adobe.com/go/devs_console_ui_fr) : dans l&#39;onglet **Intégrations**, accédez à la section **Aperçu** pour toute intégration particulière afin de trouver l&#39;identifiant sous **Informations d&#39;identification du client**. Pour une présentation détaillée de la procédure d’authentification dans [!DNL Platform], consultez le [didacticiel d’authentification](https://www.adobe.com/go/platform-api-authentication-en).

## Où trouver ma clé API ? {#where-can-i-find-my-api-key}

Une clé API doit constituer l’en-tête de toutes les requêtes API. Il est accessible via la [Console développeur d&#39;Adobes](https://www.adobe.com/go/devs_console_ui). Dans la console, sous l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique et vous trouverez la clé sous **Informations d’identification client**. Pour une présentation détaillée de la procédure d’authentification de [!DNL Platform], consultez le [didacticiel d’authentification](https://www.adobe.com/go/platform-api-authentication-en).

## Comment obtenir un jeton d’accès ? {#how-do-i-get-an-access-token}

Les jetons d’accès doivent être renseignés dans l’en-tête d’autorisation de tous les appels API. Ils peuvent être générés à l’aide d’une commande `curl`, à condition que vous ayez accès à une intégration pour une organisation IMS. Les jetons d’accès ne sont valides que pendant 24 heures. Après ce délai, un nouveau jeton doit être généré pour continuer à utiliser l’API. Pour plus d’informations sur la génération des jetons d’accès, consultez le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en).

## Comment utiliser les paramètres de requête ? {#how-do-i-user-query-parameters}

Certains points de terminaison de l&#39;API [!DNL Platform] acceptent des paramètres de requête pour localiser des informations spécifiques et filtrer les résultats renvoyés dans la réponse. Les paramètres de requête sont ajoutés aux chemins de requête avec un point d’interrogation (`?`), suivi d’un ou plusieurs paramètres de requête sous le format `paramName=paramValue`. Lorsque vous combinez plusieurs paramètres dans un seul appel, vous devez utiliser une esperluette (`&`) pour les séparer. L’exemple suivant illustre la manière dont une requête qui utilise plusieurs paramètres de requête est représentée dans la documentation.

Voici quelques exemples de paramètres de requête fréquemment utilisés :

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Pour savoir précisément quels paramètres de requête sont disponibles pour un service ou un point de terminaison en particulier, consultez la documentation spécifique au service.

## Comment indiquer un champ JSON à mettre à jour dans une requête PATCH ? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

De nombreuses opérations de PATCH dans les API [!DNL Platform] utilisent des chaînes [Pointeur JSON](https://tools.ietf.org/html/rfc6901) pour indiquer les propriétés JSON à mettre à jour. Elles sont généralement incluses dans les payloads des requêtes au format [JSON Patch](https://tools.ietf.org/html/rfc6902). Pour plus d’informations sur la syntaxe requise pour ces technologies, consultez le [guide de base de l’API](api-fundamentals.md).

## Puis-je utiliser Postman pour appeler les API [!DNL Platform] ? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) est un outil utile pour visualiser les appels vers les API RESTful. Le guide de prise en main de l&#39;API de plateforme [](api-guide.md) contient une vidéo et des instructions sur l&#39;importation de collections Postman. De plus, une liste de collections Postman pour chaque service est fournie.

## Quelle est la configuration requise pour [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Selon que vous utilisez l’interface utilisateur ou l’API, la configuration suivante est nécessaire :

**Pour les opérations basées sur l’interface utilisateur :**
- Un navigateur web standard et moderne. Bien que la dernière version de [!DNL Chrome] soit recommandée, les versions majeures actuelles et précédentes de [!DNL Firefox], [!DNL Internet Explorer] et Safari sont également prises en charge.
   - Chaque fois qu&#39;une nouvelle version majeure est publiée, [!DNL Platform] débuts prenant en charge la version la plus récente tandis que la prise en charge de la troisième version la plus récente est supprimée.
- Les cookies et JavaScript doivent être activés pour tous les navigateurs.

**Pour les interactions entre les développeurs et l’API :**
- Un environnement de développement à faire évoluer pour les intégrations de REST, de flux continu et de webhook.

## Erreurs et dépannage {#errors-and-troubleshooting}

Voici une liste d&#39;erreurs que vous pouvez rencontrer lors de l&#39;utilisation d&#39;un service [!DNL Experience Platform]. Pour obtenir des guides de dépannage sur les services [!DNL Platform] individuels, consultez le [répertoire de dépannage du service](#service-troubleshooting-directory) ci-dessous.

## Codes d’état API {#api-status-codes}

Les codes d&#39;état suivants peuvent être rencontrés sur toute API [!DNL Experience Platform]. Chacun d’entre eux pouvant être causé par un grand nombre d’éléments, les explications données dans cette section sont générales. Pour plus d&#39;informations sur les erreurs spécifiques dans les services [!DNL Platform] individuels, consultez le [répertoire de dépannage du service](#service-troubleshooting-directory) ci-dessous.

| Code d’état | Description | Causes possibles |
--- | --- | ---
| 400 | Mauvaise requête | La requête a été mal construite, des informations de clé étaient absentes et/ou sa syntaxe était incorrecte. |
| 401 | Échec de l’authentification | La requête n’a pas pu être authentifiée. Votre jeton d’accès est peut-être absent ou non valide. Pour plus d’informations, reportez-vous à la section [erreurs de jeton OAuth](#oauth-token-is-missing) ci-dessous. |
| 403 | Interdit | La ressource a été trouvée, mais vous ne possédez pas les informations d’identification appropriées pour la consulter. |
| 404 | Introuvable | La ressource demandée n’a pas été trouvée sur le serveur. La ressource a peut-être été supprimée, ou le chemin d’accès demandé n’a pas été correctement saisi. |
| 500 | Erreur interne du serveur | Il s’agit d’une erreur côté serveur. Si vous effectuez de nombreux appels simultanés, vous pouvez atteindre la limite de l’API et devoir filtrer vos résultats. (Voir le sous-guide du développeur d&#39;API [!DNL Catalog Service] sur le [filtrage des données](../catalog/api/filter-data.md) pour en savoir plus.) Patientez avant de réessayer votre requête et contactez votre administrateur si le problème persiste. |

## Erreurs dans l’en-tête de la requête {#request-header-errors}

Tous les appels d&#39;API dans [!DNL Platform] nécessitent des en-têtes de requête spécifiques. Pour connaître les en-têtes nécessaires pour un service en particulier, consultez la [documentation de référence sur l’API](http://www.adobe.com/go/platform-api-reference-en). Pour rechercher les valeurs des en-têtes d’authentification requis, consultez le [tutoriel sur l’authentification](https://www.adobe.com/go/platform-api-authentication-en). Si l’un de ces en-têtes est absent ou non valide lors d’un appel API, les erreurs suivantes peuvent se produire.

### Jeton OAuth absent {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête `Authorization` est absent d’une requête API. Assurez-vous que l’en-tête d’autorisation comprend un jeton d’accès valide avant de réessayer.

### Jeton OAuth non valide

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Ce message d’erreur s’affiche lorsque le jeton d’accès indiqué dans l’en-tête `Authorization` n’est pas valide. Assurez-vous que le jeton a été saisi correctement ou [générez un nouveau jeton](https://www.adobe.com/go/platform-api-authentication-en) dans la console Adobe I/O.

### Clé API requise

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête de clé API (`x-api-key`) est absent d’une requête API. Assurez-vous que l’en-tête comprend une clé API valide avant de réessayer.

### Clé API non valide

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Ce message d’erreur s’affiche lorsque la valeur de l’en-tête de clé API indiqué (`x-api-key`) n’est pas valide. Vérifiez que vous avez correctement saisi la clé avant de réessayer. Si vous ne connaissez pas votre clé API, vous pouvez la trouver dans la [console Adobe I/O](https://console.adobe.io) : dans l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique afin de trouver la clé API sous **Informations d’identification du client**.


### En-tête absent

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Ce message d’erreur s’affiche lorsqu’un en-tête d’organisation IMS (`x-gw-ims-org-id`) est absent d’une requête API. Assurez-vous que l’en-tête comprend l’identifiant de votre organisation IMS avant de réessayer.

### Profil non valide

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Ce message d’erreur s’affiche lorsque l’intégration d’utilisateur ou d’Adobe I/O (identifiée par le [jeton d&#39;accès](#how-do-i-get-an-access-token) dans l’en-tête `Authorization`) n’est pas autorisée à invoquer les API [!DNL Experience Platform] pour l’organisation IMS fournie dans l’en-tête `x-gw-ims-org-id`. Vérifiez que vous avez indiqué le bon identifiant pour votre organisation IMS dans l’en-tête avant de réessayer. Si vous ne connaissez pas l’identifiant de votre organisation, vous pouvez le trouver dans la [console Adobe I/O](https://console.adobe.io) : dans l’onglet **Intégrations**, accédez à la section **Aperçu** pour une intégration spécifique afin de trouver l’identifiant sous **Informations d’identification du client**.

### Type de contenu valide non spécifié

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Ce message d’erreur s’affiche lorsqu’une requête POST, PUT ou PATCH comporte un en-tête `Content-Type` non valide ou n’en comporte pas. Assurez-vous que l’en-tête est inclus dans la requête et que sa valeur est bien `application/json`.


## Répertoire de dépannage des services {#service-troubleshooting-directory}

Voici une liste de guides de dépannage et de documentation de référence d&#39;API pour les API [!DNL Experience Platform]. Chaque guide de dépannage fournit des réponses aux questions fréquentes et des solutions aux problèmes spécifiques à des services [!DNL Platform] individuels. Les documents de référence sur l’API fournissent un guide complet de tous les points de terminaison disponibles pour chaque service et présentent des échantillons de corps de requête, de réponses et de codes d’erreur que vous pouvez recevoir.

| Service | Référence d’API | Dépannage |
| --- | --- | --- |
| Contrôle d’accès | [API Access Control](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Guide de dépannage du contrôle d’accès](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform Data Ingestion | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Guide de dépannage de l&#39;assimilation par lots ](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Guide de dépannage de l&#39;assimilation en flux continu](../ingestion/streaming-ingestion/troubleshooting.md) |
| Espace de travail des données Adobe Experience Platform | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] guide de dépannage](../data-science-workspace/troubleshooting-guide.md) |
| Gouvernance des données d’Adobe Experience Platform | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] guide de dépannage](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] guide de dépannage](../query-service/troubleshooting-guide.md) |
|  de segmentation d’Adobe Experience Platform | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] FAQ et guide de dépannage](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] et [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] guide de dépannage](../profile/troubleshooting.md) |
| Environnements de test | [API Sandbox](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Guide de dépannage des environnements de test](../sandboxes/troubleshooting-guide.md) |


---
title: Secrets dans l’API Reactor
description: Découvrez les principes de base de la configuration des secrets dans l’API Reactor en vue d’une utilisation dans le transfert d’événements.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 88%

---

# Secrets dans l’API Reactor

Dans l’API Reactor, un secret est une ressource qui représente des informations d’authentification. Les secrets sont utilisés dans le transfert d’événements pour s’authentifier auprès d’un autre système afin d’échanger des données en toute sécurité. Par conséquent, les secrets ne peuvent être créés que dans les propriétés de transfert d’événements (propriétés dont le nom du champ `platform` est défini sur `edge`).

Actuellement, trois types de secrets pris en charge sont identifiés dans le nom du champ `type_of` :

| Type de secret | Description |
| --- | --- |
| `token` | Chaîne unique de caractères représentant une valeur de jeton dʼauthentification connue et comprise par les deux systèmes. |
| `simple-http` | Contient deux attributs de chaîne pour un nom dʼutilisateur et un mot de passe, respectivement. |
| `oauth2-client_credentials` | Contient plusieurs attributs pour la prise en charge de la spécification d’authentification [OAuth](https://datatracker.ietf.org/doc/html/rfc6749). Le transfert d’événements vous demande les informations requises, puis gère le renouvellement de ces jetons pour vous selon un intervalle spécifié. |

{style="table-layout:auto"}

Ce guide fournit un aperçu général de la configuration des secrets pour une utilisation dans le transfert d’événements. Pour obtenir des instructions détaillées sur la gestion des secrets dans l’API Reactor, et notamment un exemple JSON de la structure d’un secret, reportez-vous au [guide des points d’entrée des secrets](../endpoints/secrets.md).

## Informations d’identification

Chaque secret contient un attribut `credentials` qui rassemble ses valeurs d’identification respectives. Lors de la [création d’un secret dans l’API](../endpoints/secrets.md#create), chaque type de secret dispose d’attributs requis différents, comme indiqué dans les sections ci-dessous :

* [`token`](#token)
* [`simple-http`](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [`oauth2-google`](#oauth2-google)

### `token` {#token}

Les secrets disposant d’une valeur `type_of` de `token` ne requièrent qu’un seul attribut sous `credentials` :

| Attribut Credential | Type de données | Description |
| --- | --- | --- |
| `token` | Chaîne | Jeton secret compris par le système de destination. |

{style="table-layout:auto"}

Le jeton est stocké en tant que valeur statique, et par conséquent les propriétés `expires_at` et `refresh_at` du secret sont définies sur `null` lorsque le secret est créé.

### `simple-http` {#simple-http}

Les secrets disposant d’une valeur `type_of` de `simple-http` nécessitent les attributs suivants sous `credentials` :

| Attribut Credential | Type de données | Description |
| --- | --- | --- |
| `username` | Chaîne | Nom d’utilisateur. |
| `password` | Chaîne | Mot de passe. Cette valeur n’est pas incluse dans la réponse de l’API. |

{style="table-layout:auto"}

Lorsque le secret est créé, les deux attributs sont échangés avec un encodage BASE64 de `username:password`. Après l’échange, les propriétés `expires_at` et `refresh_at` du secret sont définies sur `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Les secrets disposant d’une valeur `type_of` de `oauth2-client_credentials` nécessitent les attributs suivants sous `credentials` :

| Attribut Credential | Type de données | Description |
| --- | --- | --- |
| `client_id` | Chaîne | Identifiant client de l’intégration OAuth. |
| `client_secret` | Chaîne | Secret client pour l’intégration OAuth. Cette valeur n’est pas incluse dans la réponse de l’API. |
| `token_url` | Chaîne | URL d’autorisation de l’intégration OAuth. |
| `refresh_offset` | Entier | *(Facultatif)* Valeur, en secondes, pour le décalage de l’opération d’actualisation. Si cet attribut est omis lors de la création du secret, la valeur est définie sur `14400` (quatre heures) par défaut. |
| `options` | Objet | *(Facultatif)* Spécifie les options supplémentaires pour l’intégration OAuth :<ul><li>`scope` : une chaîne qui représente la portée [OAuth 2.0](https://oauth.net/2/scope/) pour les informations d’identification.</li><li>`audience` : une chaîne qui représente un [jeton d’accès Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Lorsqu’un secret `oauth2-client_credentials` est créé ou mis à jour, `client_id` et `client_secret` (et éventuellement `options`) sont échangés dans une requête POST contre `token_url`, selon le flux d’informations d’identification du client du protocole OAuth.

>[!NOTE]
>
>Le corps de la réponse du service d’autorisation doit être compatible avec le protocole OAuth.

Si le service d’autorisation répond par `200 OK` et un corps de réponse JSON, le corps est analysé et `access_token` est placé dans l’environnement Edge et `expires_in` est utilisé pour calculer les attributs `expires_at` et `refresh_at` pour le secret. S’il n’existe aucune association d’environnement sur le secret, `access_token` est ignoré.

Un échange d’informations d’identification est considéré comme réussi dans les conditions suivantes :

* `expires_in` est supérieur à `28800` (huit heures).
* `refresh_offset` est inférieur à la valeur de `expires_in` moins `14400` (quatre heures). Par exemple, si `expires_in` est `36000` (dix heures) et que `refresh_offset` est `28800` (huit heures), l’échange est considéré comme ayant échoué, car `28800` est supérieur à `36000` - `14400` (`21600`).

Si l’échange réussit, l’attribut status du secret est défini sur `succeeded` et les valeurs de `expires_at` et `refresh_at` sont définies :

* `expires_at` est l’heure UTC actuelle plus la valeur de `expires_in`.
* `refresh_at` est l’heure UTC actuelle plus la valeur de `expires_in`, moins la valeur de `refresh_offset`. Par exemple, si `expires_in` est `43200` (douze heures) et que `refresh_offset` est `14400` (quatre heures), la propriété `refresh_at` est définie sur `28800` (huit heures) après l’heure UTC actuelle.

Si l’échange échoue pour une raison quelconque, l’attribut `status_details` dans l’objet `meta` est mis à jour avec les informations pertinentes.

#### Actualisation d’un secret `oauth2-client_credentials`

Si un secret `oauth2-client_credentials` a été affecté à un environnement et que son statut est `succeeded` (les informations d’identification ont été échangées avec succès), un nouvel échange est automatiquement effectué sur `refresh_at`.

Si l’échange réussit, l’attribut `refresh_status` dans l’objet `meta` est défini sur `succeeded` tandis que `expires_at`, `refresh_at` et `activated_at` sont mis à jour en conséquence.

En cas d’échec de l’échange, l’opération est tentée trois fois de plus ; la dernière tentative a lieu au plus tard deux heures avant l’expiration du jeton d’accès. Si toutes les tentatives échouent, l’attribut `refresh_status_details` de l’objet `meta` est mis à jour avec les détails pertinents.

### `oauth2-google` {#oauth2-google}

Les secrets avec une valeur `type_of` de `oauth2-google` requièrent l’attribut suivant sous `credentials` :

| Attribut Credential | Type de données | Description |
| --- | --- | --- |
| `scopes` | Tableau | Répertorie les portées du produit Google pour l’authentification. Les portées suivantes sont prises en charge :<ul><li>[Publicités Google](https://developers.google.com/google-ads/api/docs/oauth/overview) : `https://www.googleapis.com/auth/adwords`</li><li>[&#x200B; Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview) Google : `https://www.googleapis.com/auth/pubsub`</li></ul> |

Après avoir créé le secret `oauth2-google`, la réponse inclut une propriété `meta.authorization_url`. Vous devez copier et coller cette URL dans un navigateur pour terminer le flux d’authentification Google.

#### Réautoriser un secret `oauth2-google`

L’URL d’autorisation d’un secret `oauth2-google` expire une heure après la création du secret (comme indiqué par `meta.authorization_url_expires_at`). Au-delà, le secret doit être réautorisé afin de renouveler le processus d&#39;authentification.

Pour plus d’informations sur la réautorisation d’un secret `oauth2-google` en adressant une demande de PATCH à l’API Reactor, reportez-vous au [guide de point de terminaison de secrets](../endpoints/secrets.md#reauthorize) .

## Relation entre les environnements

Lorsque vous créez un secret, vous devez spécifier l’[environnement](../endpoints/environments.md) dans lequel il existera. Les secrets sont immédiatement déployés dans l’environnement dans lequel ils sont créés.

Un secret ne peut être associé qu’à un seul environnement. Une fois la relation entre un secret et un environnement établie, le secret ne peut pas être effacé de l’environnement, et il ne peut pas non plus être associé à un autre environnement.

>[!NOTE]
>
>La seule exception à cette règle est la suppression de l’environnement en question. Dans ce cas, la relation est effacée et le secret peut être affecté à un autre environnement.

Une fois les informations d’identification d’un secret échangées, pour qu’un secret soit associé à un environnement, l’artefact d’échange (la chaîne de jeton pour `token`, la chaîne codée Base64 pour `simple-http` ou le jeton d’accès pour `oauth2-client_credentials`) est enregistré en toute sécurité dans l’environnement.

Une fois l’artefact d’échange enregistré dans l’environnement, l’attribut `activated_at` du secret est défini sur l’heure UTC actuelle et peut alors être référencé à l’aide d’un élément de données. Voir la [section suivante](#referencing-secrets) pour plus d’informations sur la référence aux secrets.

## Référencer des secrets {#referencing-secrets}

Pour référencer un secret, vous devez créer un élément de données de type « [!UICONTROL Secret] » (fourni par l’extension [[!UICONTROL Core]](../../extensions/client/core/overview.md)) sur une propriété de transfert d’événements. Lors de la configuration de cet élément de données, vous êtes invité à indiquer le secret à utiliser pour chaque environnement. Vous pouvez ensuite créer des règles qui référencent un élément de données secret, comme dans l’en-tête d’un appel HTTP.

![Élément de données secret](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Pour ajouter un élément de données secret à une bibliothèque, vous devez avoir au moins un secret `succeeded` associé à l’environnement sur lequel la bibliothèque est en cours de création. Par exemple, si une bibliothèque comporte un élément de données secret qui n’a pas de secret `succeeded` configuré pour la section [!UICONTROL Secret d’évaluation], si vous tentez de créer cette bibliothèque dans l’environnement d’évaluation, une erreur se produira.

Au moment de l’exécution, l’élément de données secret est remplacé par l’artefact d’échange secret correspondant enregistré dans l’environnement.

## Étapes suivantes

Ce guide décrit les principes de base de l’utilisation des secrets dans l’API Reactor. Pour plus d’informations sur la gestion des secrets à l’aide des appels API, voir la section [guide des points d’entrée des secrets](../endpoints/secrets.md).

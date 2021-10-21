---
title: Secrets de l'API du réacteur
description: Découvrez les principes de base de la configuration des secrets dans l’API Reactor pour une utilisation dans le transfert d’événements.
source-git-commit: 6822199c3ecf4414893a8b8dfc650e3da40a6470
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 3%

---

# Secrets de l&#39;API du réacteur

Dans l’API du réacteur, un secret est une ressource qui représente des informations d’identification d’authentification. Les secrets sont utilisés dans le transfert d&#39;événements pour s&#39;authentifier auprès d&#39;un autre système afin d&#39;échanger des données en toute sécurité. Par conséquent, les secrets ne peuvent être créés que dans les propriétés de transfert d&#39;événements (propriétés dont `platform` est défini sur `edge`).

Il existe actuellement trois types de secret pris en charge signalés dans le fichier `type_of` attribut :

| Type secret | Description |
| --- | --- |
| `token` | Chaîne unique de caractères représentant une valeur de jeton d’authentification connue et comprise par les deux systèmes. |
| `simple-http` | Contient deux attributs de chaîne pour un nom d&#39;utilisateur et un mot de passe, respectivement. |
| `oauth2` | Contient plusieurs attributs pour prendre en charge le [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) spécification d&#39;authentification. Le transfert d’événements vous demande les informations requises, puis traite le renouvellement de ces jetons pour vous selon un intervalle spécifié. |

{style=&quot;table-layout:auto&quot;}

Ce guide fournit une vue d’ensemble de haut niveau sur la configuration des secrets à utiliser dans le transfert d’événements. Pour obtenir des conseils détaillés sur la gestion des secrets dans l&#39;API du réacteur, y compris l&#39;exemple JSON de la structure d&#39;un secret, consultez la rubrique [guide de point de terminaison secrets](../endpoints/secrets.md).

## Informations d’identification

Chaque secret contient une `credentials` qui contient ses valeurs d’informations d’identification respectives. Chaque type de secret possède des attributs obligatoires différents, comme indiqué dans les sections ci-dessous.

### `token`

Secrets avec un `type_of` valeur de `token` ne nécessite qu’un attribut unique sous `credentials`:

| Attribut d’informations d’identification | Type de données | Description |
| --- | --- | --- |
| `token` | Chaîne | Jeton secret compris par le système de destination. |

{style=&quot;table-layout:auto&quot;}

Le jeton est stocké en tant que valeur statique, et par conséquent le `expires_at` et `refresh_at` sont définies sur `null` lorsque le secret est créé.

### `simple-http`

Secrets avec un `type_of` valeur de `simple-http` nécessitent les attributs suivants sous `credentials`:

| Attribut d’informations d’identification | Type de données | Description |
| --- | --- | --- |
| `username` | Chaîne | Un nom d&#39;utilisateur. |
| `password` | Chaîne | Un mot de passe. Cette valeur n’est pas incluse dans la réponse API. |

{style=&quot;table-layout:auto&quot;}

Lorsque le secret est créé, les deux attributs sont échangés avec un codage BASE64 de `username:password`. Après l&#39;échange, le secret est `expires_at` et `refresh_at` sont définies sur `null`.

### `oauth2`

>[!NOTE]
>
>Actuellement, seule la [Type de subvention des informations d&#39;identification client](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) est pris en charge pour les secrets OAuth.

Secrets avec un `type_of` valeur de `oauth2` nécessitent les attributs suivants sous `credentials`:

| Attribut d’informations d’identification | Type de données | Description |
| --- | --- | --- |
| `client_id` | Chaîne | ID client de l’intégration OAuth. |
| `client_secret` | Chaîne | Le secret client de l&#39;intégration OAuth. Cette valeur n’est pas incluse dans la réponse API. |
| `authorization_url` | Chaîne | URL d’autorisation pour l’intégration OAuth. |
| `refresh_offset` | Entier | *(Facultatif)* Valeur, en secondes, de laquelle décaler l’opération d’actualisation. Si cet attribut est omis lors de la création du secret, la valeur est définie sur `14400` (quatre heures) par défaut. |
| `options` | Objet | *(Facultatif)* Spécifie des options supplémentaires pour l’intégration OAuth :<ul><li>`scope`: Une chaîne qui représente le [Portée OAuth 2.0](https://oauth.net/2/scope/) pour les informations d’identification.</li><li>`audience`: Une chaîne qui représente un [Jeton d’accès Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Lorsque `oauth2` le secret est créé ou mis à jour, le `client_id` et `client_secret` (et éventuellement `options`) sont échangés dans le cadre d’une demande POST adressée au `authorization_url`, conformément au flux d&#39;informations d&#39;identification du client du protocole OAuth.

>[!NOTE]
>
>On s&#39;attend à ce que l&#39;organisme de réponse du service d&#39;autorisation soit compatible avec le protocole OAuth.

Si le service d’autorisation répond par `200 OK` et un corps de réponse JSON, le corps est analysé et le `access_token` est poussé vers l’environnement de bord et `expires_in` est utilisé pour calculer le `expires_at` et `refresh_at` pour le secret. S&#39;il n&#39;y a pas d&#39;association environnementale sur le secret, `access_token` est ignoré.

Un échange de références est considéré comme une réussite dans les conditions suivantes :

* `expires_in` est supérieur à `28800` (huit heures).
* `refresh_offset` est inférieur à la valeur de `expires_in` moins `14400` (quatre heures). Par exemple, si `expires_in` est `36000` (dix heures) et `refresh_offset` est `28800` (huit heures), l&#39;échange est considéré comme ayant échoué parce que `28800` est supérieur à `36000` - `14400` (`21600`).

Si l&#39;échange réussit, l&#39;attribut status du secret est défini sur `succeeded` et valeurs pour `expires_at` et `refresh_at` sont définies :

* `expires_at` est l&#39;heure UTC actuelle plus la valeur de `expires_in`.
* `refresh_at` est l&#39;heure UTC actuelle plus la valeur de `expires_in`, moins la valeur de `refresh_offset`. Par exemple, si `expires_in` est `43200` (douze heures) et la `refresh_offset` est `14400` (quatre heures), la `refresh_at` serait définie sur `28800` (huit heures) après l&#39;heure UTC actuelle.

Si l’échange échoue pour une raison quelconque, la `status_details` dans la `meta` est mis à jour avec les informations pertinentes.

### Actualisation d’un `oauth2` secret

Si `oauth2` secret a été assigné à un environnement et son statut est `succeeded` (les informations d&#39;identification ont été échangées avec succès), un nouvel échange est effectué automatiquement le `refresh_at`.

Si l’échange réussit, la `refresh_status` dans la `meta` l’objet est défini sur `succeeded` pendant `expires_at`, `refresh_at`et `activated_at` sont mises à jour en conséquence.

Si l’échange échoue, l’opération est tentée trois fois de plus avec la dernière tentative au plus deux heures avant l’expiration du jeton d’accès. Si toutes les tentatives échouent, la `refresh_status_details` de `meta` est mis à jour avec les détails pertinents.

## Relations entre les environnements

Lorsque vous créez un secret, vous devez spécifier la [environnement](../endpoints/environments.md) dans laquelle il existera. Les secrets sont immédiatement déployés dans l’environnement dans lequel ils sont créés.

Un secret ne peut être associé qu&#39;à un seul environnement. Une fois que la relation entre un secret et un environnement est établie, le secret ne peut pas être effacé de l&#39;environnement, et le secret ne peut pas être associé à un autre environnement.

>[!NOTE]
>
>La seule exception à cette règle est la suppression de l&#39;environnement en question. Dans ce cas, la relation est effacée et le secret peut être assigné à un autre environnement.

Une fois que les informations d&#39;identification d&#39;un secret ont été échangées, pour qu&#39;un secret soit associé à un environnement, l&#39;artefact d&#39;échange (chaîne de jeton pour `token`, la chaîne codée Base64 pour `simple-http`ou du jeton d’accès pour `oauth2`) est sauvé en toute sécurité de l&#39;environnement.

Une fois l&#39;artefact d&#39;échange enregistré dans l&#39;environnement, le `activated_at` est défini sur l’heure UTC actuelle et peut désormais être référencé à l’aide d’un élément de données. Voir la section [section suivante](#referencing-secrets) pour plus d&#39;informations sur les secrets de référencement.

## Référence aux secrets {#referencing-secrets}

Pour référencer un secret, vous devez créer un élément de données de type &quot;[!UICONTROL Secret]&quot; (fourni par [[!UICONTROL Core] extension](../../extensions/web/core/overview.md)) sur une propriété de transfert d&#39;événement. Lors de la configuration de cet élément de données, vous êtes invité à indiquer le secret à utiliser pour chaque environnement. Vous pouvez ensuite créer des règles faisant référence à un élément de données secrètes, comme dans l’en-tête d’un appel HTTP.

![Elément de données secret](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Pour ajouter un élément de données secrètes à une bibliothèque, vous devez en avoir au moins un. `succeeded` secret associé à l&#39;environnement sur lequel la bibliothèque est construite. Par exemple, si une bibliothèque possède un élément de données secrètes qui ne possède pas de `succeeded` secret configuré pour [!UICONTROL Secret intermédiaire] , si vous tentez de créer cette bibliothèque dans l’environnement intermédiaire, une erreur s’affichera.

Au moment de l’exécution, l’élément de données secrètes est remplacé par l’artefact d’échange secret correspondant enregistré dans l’environnement.

## Étapes suivantes

Ce guide décrit les principes de base de l’utilisation des secrets dans l’API du réacteur. Pour plus d’informations sur la gestion de secrets à l’aide d’appels d’API, consultez la section [guide de point de terminaison secrets](../endpoints/secrets.md).

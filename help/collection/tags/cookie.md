---
title: cookie
description: Écrivez, modifiez ou supprimez manuellement les cookies pour la propriété de balise.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 7%

---

# `cookie`

L’objet `_satellite.cookie` contient des méthodes qui vous permettent d’écrire, de modifier ou de supprimer des cookies auxquels vos règles de balise peuvent faire référence. Il s’agit d’une copie partielle de [`js-cookie`](https://github.com/js-cookie/js-cookie), qui contient de nombreuses fonctionnalités principales de cette bibliothèque.

## `cookie.set()`

La méthode `set()` écrit un cookie que votre propriété de balise peut référencer.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

Les paramètres de méthode disponibles sont les suivants :

| Nom | Type | Obligatoire | Description |
|---|---|---|---|
| **`name`** | `string` | Oui | Nom du cookie. |
| **`value`** | `string` | Oui | Valeur du cookie |
| **`attributes`** | `object` | Non | Attributs supplémentaires que vous souhaitez attribuer au cookie. |

L’objet `attributes` prend en charge les propriétés suivantes :

| Nom de l’attribut | Type | Obligatoire | Par défaut | Description |
|---|---|---|---|---|
| **`expires`** | `number` ou [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | Non | Le cookie expire à la fin de la session du navigateur | Nombre de jours pendant lesquels vous souhaitez que le cookie expire. |
| **`path`** | `string` | Non | Cookie visible sur tout le site | Emplacement du cookie sur votre domaine. |
| **`domain`** | `string` | Non | Cookie visible pour le domaine sous lequel il a été créé | Un domaine valide (avec ou sans sous-domaine) où le cookie est visible. Si un domaine est inclus sans sous-domaine, le cookie est visible par tous les sous-domaines de ce domaine. |
| **`secure`** | `boolean` | Non | Aucun attribut défini | Détermine si le cookie nécessite un protocole sécurisé (`https://`). Si cet attribut est omis, il n’existe aucune exigence de protocole sécurisé. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | Non | Aucun attribut défini | Permet de définir l’attribut [`sameSite`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) d’un cookie. Si vous définissez `sameSite` sur `None`, vous devez également définir `secure` sur `true`. |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

L’appel de cette méthode écrit le cookie souhaité et renvoie la chaîne de cookie sérialisée qui a été écrite. Cette chaîne est principalement utilisée à des fins de débogage ou de journalisation.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>Les versions précédentes de l’objet de balise `_satellite.setCookie()` utilisées. La méthode `setCookie()` est abandonnée au profit de `_satellite.cookie.set()`.

## `cookie.get()`

La méthode `get()` renvoie une valeur de cookie.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| Nom | Type | Obligatoire | Description |
|---|---|---|---|
| **`name`** | `string` | Oui | Nom du cookie à partir duquel vous souhaitez récupérer la valeur (sensible à la casse). |

Si le nom du cookie existe, renvoie la valeur du cookie. Si le nom du cookie n’existe pas, renvoie `undefined`.

>[!TIP]
>
>Les versions précédentes de l’objet de balise `_satellite.getCookie()` utilisées. La méthode `getCookie()` est abandonnée au profit de `_satellite.cookie.get()`.

## `cookie.remove()`

La méthode `remove()` supprime un cookie que vous avez défini.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| Nom | Type | Obligatoire | Description |
|---|---|---|---|
| **`name`** | `string` | Oui | Nom du cookie à supprimer. |
| **`attributes`** | `object` | Non | Attributs associés au cookie que vous souhaitez supprimer. Si vous définissez un cookie à l’aide des attributs `path` ou `domain`, incluez ces mêmes attributs lors de la suppression du cookie. L’échec de l’inclusion de ces attributs ne supprime pas le cookie. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>Les versions précédentes de l’objet de balise `_satellite.removeCookie()` utilisées. La méthode `removeCookie()` est abandonnée au profit de `_satellite.cookie.remove()`.
